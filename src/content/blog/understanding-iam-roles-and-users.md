---
author: Nithissh S
pubDatetime: 2025-01-28T15:22:00Z
modDatetime: 2025-01-28T16:12:47.400Z
title: IAM Users vs IAM roles - Understanding the differences
slug: understand-iam-roles-and-users
featured: false
draft: false
tags:
  - CloudSec
description:
  Understanding the differences between the IAM roles and IAM uders 
---

## IAM Users
- Tied to static credentials (username/password or API keys) and static permissions, which can lead to security risks:
  - **Static credentials** are prone to leakage, theft, or exposure.
  - **Static permissions** can be overly broad, leading to unnecessary privilege escalation.
- IAM users can be used for external access to AWS resources, posing security threats if credentials are compromised.

## IAM Roles
- Provide **dynamic and temporary credentials**, solving key problems with IAM users:
  - **Temporary Credentials:** Roles issue credentials that expire after a set session, reducing the risk of long-lived keys.
  - **Dynamic Permissions:** Roles allow different permissions as needed, avoiding reliance on static user permissions.
  - **Persona Concept:** Users can switch between different "personas" (e.g., “read-only” for monitoring, “admin” for management tasks).

## Role Characteristics

### IAM Role as a Container for Permissions
- A role is a **container** holding a set of permissions, defining what actions can be performed.

### Trust Policy
- Specifies **who or what** can assume the role.
- Example: An **EC2 instance** might assume a role to access AWS services.

### Permissions Policy
- Defines **what actions** the role can perform.
- Example: A role might **grant read access** to an S3 bucket or **admin access** to a DynamoDB table.

### Temporary Session
- When a role is assumed, AWS provides **temporary credentials** for a session.
- These credentials **expire after a set duration**, reducing risk.
- The session duration is **customizable** via the **Maximum Session Duration** setting.

### Role Assumption
- To use an IAM role, a **user or service must assume the role**.
- This creates a **session with temporary credentials**, allowing controlled access.

## Switching Personas
- IAM roles allow users to **switch between different personas**, providing **context-dependent permissions**.
- Example:
  - A user might assume a **read-only** role for monitoring.
  - The same user can switch to an **admin** role for making changes.

## Instance Profiles
- **Instance Profile:** Connects an **EC2 instance** with an IAM role.
- Enables EC2 instances to **securely interact** with AWS services **without exposing credentials**.
- In the AWS Console:
  - **Instance profiles are created automatically** when assigning roles to EC2.
  - **When using the API, instance profiles must be created manually.**

## Key Points from the Lab
- **IAM Users:** Have **static credentials and permissions**, making them a security risk.
- **IAM Roles:** Provide **temporary credentials** with **flexible, context-dependent permissions**.
- **Role Components:**
  - **Trust Policy:** Defines **who or what** can assume the role.
  - **Permissions Policy:** Defines **what actions** can be performed.
  - **Temporary Session:** Uses short-lived credentials to **reduce risk**.
  - **Switching Roles:** Users can switch roles based on their tasks.
  - **Instance Profiles:** Allow **EC2 instances to assume IAM roles** securely.