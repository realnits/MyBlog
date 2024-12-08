---
author: Nithissh S
pubDatetime: 2024-10-14T15:22:00Z
modDatetime: 2024-10-14T09:12:47.400Z
title: OS command injection, simple case
slug: os-portswigger-lab-5
featured: false
draft: false
tags:
  - BSCP
  - Command Injection
description:
  This lab contains an OS command injection vulnerability in the product stock checker. The application executes a shell command containing user-supplied product and store IDs, and returns the raw output from the command in its response. To solve the lab, execute the whoami command to determine the name of the current user.    
---

## Objective 

This lab contains an OS command injection vulnerability in the product stock checker.

The application executes a shell command containing user-supplied product and store IDs, and returns the raw output from the command in its response.

To solve the lab, execute the whoami command to determine the name of the current user. 

## Solution

In this application, each product have a functionality to check on how many number of stocks are there based on the city and here is how the request and response looks like 

![](../../assets/images/bscp/os/os-1.png) 

Assuming that some kind of bash script is running in back as mentioned in the lab objective.. I thought off why can't place `;` in both parameter.. you know in bash, it would obviously breaks that script because `;` symbol will end the script from running and whatever value after `;` will run but when placed in the `productId` it reacted differently and produced an error 

![](../../assets/images/bscp/os/os-2.png) 

Awesome, with the following payload `;id` on to the `productId` parameter resulted it in a execution of `id` in the response 

![](../../assets/images/bscp/os/os-3.png) 

Ran the `whoami` but I didn't see the output as expected but the lab is solved and in order to know what user exists.. passed the following payload `;id -un` which produces the same output as `whoami` 

![](../../assets/images/bscp/os/os-4.png) 