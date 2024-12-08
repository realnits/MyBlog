---
author: Nithissh S
pubDatetime: 2024-10-24T15:22:00Z
modDatetime: 2024-10-24T09:12:47.400Z
title: Password reset poisoning via middleware
slug: auth-portswigger-lab-11
featured: false
draft: false
tags:
  - BSCP
  - Authentication
description:
  This lab's password change functionality makes it vulnerable to brute-force attacks. To solve the lab, use the list of candidate passwords to brute-force Carlos's account and access his "My account" page. 
---

## Objective 

This lab's password change functionality makes it vulnerable to brute-force attacks. To solve the lab, use the list of candidate passwords to brute-force Carlos's account and access his "My account" page. 

## Solution 

If we enter the wrong password, the response says that the current password is incorrect 

![](../../assets/images/bscp/auth/auth-51.png)

So when we enter the correct password, the new password, and the confirmed password (if it's different). The response is different. 

![](../../assets/images/bscp/auth/auth-52.png)

Let's bruteforce the current password field through intruder... but based on response filter where we saw initially on `new password` and `confirm new password` and as it makes a error like `New password is incorrect` 

Now after bruteforce is completed and we found that the password for carlos user is `george` 

![](../../assets/images/bscp/auth/auth-53.png)

Log in as `carlos` user with password as `george` and that solves the lab 

![](../../assets/images/bscp/auth/auth-54.png)