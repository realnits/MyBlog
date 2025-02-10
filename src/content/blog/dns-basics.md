---
author: Nithissh S
pubDatetime: 2024-01-24T11:22:00Z
modDatetime: 2024-01-24T11:22:00Z
title: DNS 101
slug: dns-basics
featured: true
draft: false
tags:
  - DNS
description:
  Some DNS notes which I had in my archive 
--- 

## What is DNS?
- Used by **TCP/IP applications** to map **hostnames to IP addresses** and provide **email routing information**.
- Applications must **convert a hostname → IP address** before initiating **TCP/UDP connections** or sending datagrams.

### DNS Access
- Accessed through a **Resolver**, which is part of the application (not the OS).
- UNIX hosts use two key library functions:
  - `gethostname(3)`: Converts **hostname to IP address**.
  - `gethostbyaddr(3)`: Converts **IP address to hostname**.

### Most Common DNS Implementation
- **BIND (Berkeley Internet Name Domain Server)** is the most widely used DNS implementation.


## DNS Basics

### DNS Name Space
- **Hierarchical structure** where each node has a **label** (up to 63 characters).
- The **root node** has a **null label**.

### Fully Qualified Domain Name (FQDN)
- A domain name that **ends with a period (.)**.

### Top-Level Domains (TLDs)
- Divided into three categories:
  1. **`.arpa`**: Used for **address-to-name mappings**.
  2. **Generic Domains**: 3-character domains (e.g., **.com, .org**).
  3. **Country/Geographical Domains**: 2-character domains **based on country codes**.

#### TLD Restrictions
- **`.gov` and `.mil`** are **restricted to the United States**.


## DNS Delegation
- No single entity **manages the entire DNS tree**.
- Different entities **maintain different portions**, delegating authority for **specific zones**.

### Zones
- A **zone** is a **sub-tree** administered by a **specific entity**.
- A common zone is the **second-level domain**.
- Zones can be **subdivided into smaller zones**.

### Name Servers
- Each **zone** must have:
  - **Primary name server** (loads info from disk).
  - **One or more secondary name servers** (obtain info via **zone transfer**).

### Zone Transfer
- The process of **copying data from the primary server** to secondary servers.
- **Usually occurs every 3 hours**.

### Name Caching
- **Speeds up** subsequent queries by reducing additional server lookups.


## DNS Message Format

### Header (12-byte fixed)
- Contains **identifiers** for the client-server transaction.
- **Flags (16 bits):**
  - **QR**: `0` for query, `1` for response.
  - **Opcode**: Query type (Standard, Inverse, Server Status).
  - **AA**: **Authoritative Answer**.
  - **TC**: **Truncated Response** (exceeds 512 bytes in UDP).
  - **RD**: **Recursion Desired**.
  - **RA**: **Recursion Available**.
  - **Rcode**: **Return Code** (e.g., `0` for no error).

### Question Section
- Contains:
  - **Query Name** (hostname).
  - **Query Type** (e.g., `A`, `PTR`).
  - **Query Class** (usually `1` for Internet).


## Resource Records (RR) in DNS

### Common RR Types:
- **A**: Maps hostname to **IPv4 address**.
- **PTR**: Maps **IP address → hostname** (**Reverse DNS lookup**).
- **CNAME**: **Alias** for another domain name.
- **HINFO**: **Host information** (CPU, OS details).
- **MX**: **Mail exchange records** for email routing.
- **NS**: **Name server record** specifying authoritative servers for a domain.


## Pointer Queries (Reverse DNS Lookup)
- **Reverse DNS lookup** maps **IP addresses → hostnames** using **PTR records** under `.in-addr.arpa`.
- **Example:**
  - **IP:** `140.252.13.33`
  - **PTR Record:** `33.13.252.140.in-addr.arpa`
  - **IP is written in reverse order** in the PTR query.

### Hostname Spoofing Check
- **Servers verify** that the IP address of incoming requests matches the DNS record.
- Example:
  - **Rlogin** requires that the **hostname → IP address** mapping is valid and verified.


## Caching in DNS
- **Caching Strategy**: Reduces DNS traffic by caching answers to queries.
- **Unix Systems**: Caching is done on the **name server side**, not the **client side**.
- **Cache Expiry**: Each record has a **Time-To-Live (TTL)** value defining how long it can be cached.


## UDP vs TCP in DNS
- **UDP** is the **default transport** for DNS queries.
- **Truncated Responses**: If a response exceeds **512 bytes**, it is **truncated and sent via UDP**.
- A **subsequent query** is made using **TCP** to handle the larger response.
- **TCP is used for:**
  - **Zone transfers** (transferring DNS records between servers).
  - **Handling responses exceeding UDP's limits**.


## DNS Query/Response Workflow
1. **Client requests IP address** from **DNS resolver** (`A` record query).
2. **Root server** responds with the **name servers** for the domain.
3. **Client sends `A` record query** to the domain’s name server.
4. **Name server** responds with the **IP address**.
5. **Client establishes a TCP connection** to the server.
6. **Server checks the client’s IP address** using a **PTR query**.
7. **Root server responds** with **name servers** for the client’s domain.
8. **Server sends PTR query** to the **client’s name server**.
9. **Client’s name server responds** with the **hostname (FQDN)**.
10. **Server queries the client’s name server** for the **IP address (`A` record)**.
11. **Server verifies the response** matches the incoming connection’s **IP address**.