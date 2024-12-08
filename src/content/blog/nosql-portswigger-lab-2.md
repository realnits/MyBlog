---
author: Nithissh S
pubDatetime: 2024-12-01T15:22:00Z
modDatetime: 2024-12-01T09:12:47.400Z
title: Exploiting NoSQL operator injection to bypass authentication
slug: nosql-portswigger-lab-2
featured: false
draft: false
tags:
  - BSCP
  - NoSQL Injection
description:
  The login functionality for this lab is powered by a MongoDB NoSQL database. It is vulnerable to NoSQL injection using MongoDB operators. To solve the lab, log into the application as the `administrator` user. You can log in to your own account using the following credentials `wiener:peter`.  
---

## Objective 

The login functionality for this lab is powered by a MongoDB NoSQL database. It is vulnerable to NoSQL injection using MongoDB operators.

To solve the lab, log into the application as the `administrator` user.

You can log in to your own account using the following credentials: `wiener:peter`. 

## Solution 

After entering the username and password, intercepted the request in burp.. that's where we gonna begin actually 

![](../../assets/images/bscp/nosql/nosql-5.png)

Ok, now we have created the following payload where it will checks for regex against a keyword called `admin` using `$regex` and `$ne` set to empty value meaning matches all values that are not equal to a specified value

```json
{"username":{"$regex":"^admin"},"password":{"$ne":""}}
```

Sent the request and as a response we may get `302` along with session cookie 

![](../../assets/images/bscp/nosql/nosql-6.png)

Just open the response in the browser, that will solve the lab 

![](../../assets/images/bscp/nosql/nosql-7.png)