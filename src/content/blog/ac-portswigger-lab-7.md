---
author: Nithissh S
pubDatetime: 2024-10-15T15:22:00Z
modDatetime: 2024-10-15T09:12:47.400Z
title: URL-based access control can be circumvented
slug: ac-portswigger-lab-7
featured: false
draft: false
tags:
  - BSCP
  - Access Control
description:
  This website has an unauthenticated admin panel at /admin, but a front-end system has been configured to block external access to that path. However, the back-end application is built on a framework that supports the X-Original-URL header. To solve the lab, access the admin panel and delete the user carlos.  
---

## Introduction 

This website has an unauthenticated admin panel at /admin, but a front-end system has been configured to block external access to that path. However, the back-end application is built on a framework that supports the X-Original-URL header.

To solve the lab, access the admin panel and delete the user carlos. 

## Solution

As mentioned in the lab objective, we have exposed admin panel which can be accessible through the following path `/admin` or you can click directly on the `Admin panel` tab available in the lab itself

![](../../assets/images/bscp/access-control/access-17.png)

Accessing the admin panel, But it says `Access denied`

![](../../assets/images/bscp/access-control/access-18.png)

Intercept the request in burpsuite, send it to repeater and add the following header called `X-Original-Url:` with the value sets as `/admin` and Once after sending the request, response shows that we are now able to access the admin panel 

![](../../assets/images/bscp/access-control/access-19.png)

Now the sent the following request as shown in image below which will delete the user called the `carlos` and lab is solved 

![](../../assets/images/bscp/access-control/access-20.png)