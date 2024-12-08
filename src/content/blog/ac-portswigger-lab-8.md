---
author: Nithissh S
pubDatetime: 2024-10-15T15:22:00Z
modDatetime: 2024-10-15T09:12:47.400Z
title: User ID controlled by request parameter with data leakage in redirect
slug: ac-portswigger-lab-8
featured: false
draft: false
tags:
  - BSCP
  - Access Control
description:
  This lab contains an access control vulnerability where sensitive information is leaked in the body of a redirect response. To solve the lab, obtain the API key for the user carlos and submit it as the solution. You can log in to your own account using the following credentials wiener:peter  
---

## Introduction 

This lab contains an access control vulnerability where sensitive information is leaked in the body of a redirect response.

To solve the lab, obtain the API key for the user carlos and submit it as the solution.

You can log in to your own account using the following credentials: wiener:peter 

## Solution 

With the following credentials they have provided `wiener:peter` and observe that each user may have a API key 

![](../../assets/images/bscp/access-control/access-36.png)

In the browser, if you observe closely on the parameter and their values where we have `?id=wiener` and changing it to `carlos` and redirects directly to the login page 

![](../../assets/images/bscp/access-control/access-37.png)

But the same above method reproduced in burp's repeater actually leaks the carlos API key in the and also redirects to `login page` 

![](../../assets/images/bscp/access-control/access-38.png)

We can also find the `carlos` API key in the same above response

![](../../assets/images/bscp/access-control/access-39.png)

Copy and paste the API key as a solution and lab will be solved 

![](../../assets/images/bscp/access-control/access-40.png)

This works due to the fact in the browser we have client-side checks where as through burp it is bypassed now 