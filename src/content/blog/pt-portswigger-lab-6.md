---
author: Nithissh S
pubDatetime: 2024-10-13T15:22:00Z
modDatetime: 2024-10-13T09:12:47.400Z
title: File path traversal, validation of start of path
slug: pt-portswigger-lab-7
featured: false
draft: false
tags:
  - BSCP
  - Path Traversal
description:
  This lab contains a path traversal vulnerability in the display of product images. The application transmits the full file path via a request parameter, and validates that the supplied path starts with the expected folder. To solve the lab, retrieve the contents of the `/etc/passwd` file.    
---

## Objective

This lab contains a path traversal vulnerability in the display of product images.

The application transmits the full file path via a request parameter, and validates that the supplied path starts with the expected folder.

To solve the lab, retrieve the contents of the `/etc/passwd` file.

  

## Solution

  

In the previous labs, we usually saw that only filename parameter might pass along with the image filename just like `/?filename=30.png`  but in this case it is slightly different where we have `?filename=/var/www/images/40.jpg` 

  

![](../../assets/images/bscp/path-traversal/image%206.png)  

  

But In the lab description says right, there is a validation in place initial full which is `/var/www/images`  we can able bypass this by traversing afterwards like `/var/www/images/../../`  

  

Intercepted the request in caido and traversed from `/var/www/images/../`  to `/var/www/images/../../../etc/passwd`  to get the contents of `/etc/passwd` 

  

![](../../assets/images/bscp/path-traversal/image%207.png)  

  

Summary is there is path validation where it should definitely starts with `/var/www/images/`  whatever after the fullpath they don’t validate andhence we were able to traverse and get the contents of `/etc/passwd`