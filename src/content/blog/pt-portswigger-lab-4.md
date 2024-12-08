---
author: Nithissh S
pubDatetime: 2024-10-13T15:22:00Z
modDatetime: 2024-10-13T09:12:47.400Z
title: File path traversal, traversal sequences stripped with superfluous URL-decode
slug: pt-portswigger-lab-4
featured: false
draft: false
tags:
  - BSCP
  - Path Traversal
description:
  This lab contains a path traversal vulnerability in the display of product images. The application blocks input containing path traversal sequences. It then performs a URL-decode of the input before using it. To solve the lab, retrieve the contents of the `/etc/passwd` file.    
---

## Objective
  

This lab contains a path traversal vulnerability in the display of product images.

The application blocks input containing path traversal sequences. It then performs a URL-decode of the input before using it.

To solve the lab, retrieve the contents of the `/etc/passwd` file.

  

## Solution

  

In this lab we have the `filename`  parameter just like the other labs on what we saw 

  

![](../../assets/images/bscp/path-traversal/image%208.png)  

  

But when we can keep traversing, things don’t workout now where as the lab description whatever the input you pass and result will be URL decoded

  

![](../../assets/images/bscp/path-traversal/image%209.png)  

  

If the payload is URL encoded, then send it to the server and server will process like URL decode in our case and with the same payload in the above `../../../etc/passwd`  where we can encoded it two times and becomes `..%252F..%252F..%252Fetc%252Fpasswd`  when server process it where as it will URL decoded by server and gets the content of `/etc/passwd` 

  

![](../../assets/images/bscp/path-traversal/image%2010.png)