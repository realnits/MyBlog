---
author: Nithissh S
pubDatetime: 2024-10-15T15:22:00Z
modDatetime: 2024-10-15T09:12:47.400Z
title: Insecure direct object references
slug: ac-portswigger-lab-1
featured: false
draft: false
tags:
  - BSCP
  - Access Control
description:
  This lab stores user chat logs directly on the server's file system, and retrieves them using static URLs. Solve the lab by finding the password for the user carlos, and logging into their account.   
---

# Introduction

This lab stores user chat logs directly on the server's file system, and retrieves them using static URLs.

Solve the lab by finding the password for the user carlos, and logging into their account. 

## Solution

Once after login, we have a functionality to do a `live chat` and Clicking on `View transcript` it will actually download the transcript 

![](../../assets/images/bscp/access-control/access-46.png)

Now change it from `4.txt` to `1.txt` actually reveals other users transcript and observing the transcript carefully we have password of `carlos` 

![](../../assets/images/bscp/access-control/access-48.png)

Login in with the found password and solves the lab 

![](../../assets/images/bscp/access-control/access-49.png)