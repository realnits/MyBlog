---
author: Nithissh S
pubDatetime: 2024-10-17T15:22:00Z
modDatetime: 2024-10-17T09:12:47.400Z
title: SSRF with filter bypass via open redirection vulnerability
slug: ssrf-portswigger-lab-5
featured: false
draft: false
tags:
  - BSCP
  - SSRF
description:
  This lab has a stock check feature which fetches data from an internal system. To solve the lab, change the stock check URL to access the admin interface at http://192.168.0.12:8080/admin and delete the user carlos. The stock checker has been restricted to only access the local application, so you will need to find an open redirect affecting the application first. 
---

## Introduction

This lab has a stock check feature which fetches data from an internal system.

To solve the lab, change the stock check URL to access the admin interface at http://192.168.0.12:8080/admin and delete the user carlos.

The stock checker has been restricted to only access the local application, so you will need to find an open redirect affecting the application first. 

## Solution

In this challenge also, we have the same functionality but it is being called internally to check the stock units

![](../../assets/images/bscp/ssrf/ssrf-28.png)

if you look deep dive into the view-source,  we have a new parameter called `path` which is also reached out in other ways by clicking on next product hyperlink

![](../../assets/images/bscp/ssrf/ssrf-29.png)

Now In the intercepted request, add the `path` parameter and as an value called `http://192.168.0.12:8080/admin` to access the admin panel which is mentioned in the lab objective and send the request 

After sending the request, we found some sort of kind of open redirection issue here 

![](../../assets/images/bscp/ssrf/ssrf-30.png)


Now, take the following path from where we found the redirection issue and replace the copied path under `stockApi` parameter and sent the request and now we were able to access the admin panel 

![](../../assets/images/bscp/ssrf/ssrf-31.png)

Now again send the following request `/admin/delete?username=carlos` where as user called carlos will be deleted and lab will be solved 

![](../../assets/images/bscp/ssrf/ssrf-32.png)