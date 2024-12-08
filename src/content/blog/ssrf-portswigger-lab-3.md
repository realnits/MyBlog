---
author: Nithissh S
pubDatetime: 2024-10-16T15:22:00Z
modDatetime: 2024-10-16T09:12:47.400Z
title: Blind SSRF with out-of-band detection
slug: ssrf-portswigger-lab-3
featured: false
draft: false
tags:
  - BSCP
  - SSRF
description:
  This site uses analytics software which fetches the URL specified in the Referer header when a product page is loaded. To solve the lab, use this functionality to cause an HTTP request to the public Burp Collaborator server.  
---

## Introduction 

This site uses analytics software which fetches the URL specified in the Referer header when a product page is loaded.

To solve the lab, use this functionality to cause an HTTP request to the public Burp Collaborator server. 

## Solution 

Once after spinning the lab, you can go, visit any products available on this website and intercept the request 

![](../../assets/images/bscp/ssrf/ssrf-24.png)

Replace the actual value in `Referrer:` header with the collaborator URL and send the request 

Well, the request passes and responds with a status code of 200 

![](../../assets/images/bscp/ssrf/ssrf-25.png)

Looking into the collaborator, we have received HTTP pingback which is our endgoal to make it 

![](../../assets/images/bscp/ssrf/ssrf-26.png)


Once we got HTTP pingback and our lab is solved as well 

![](../../assets/images/bscp/ssrf/ssrf-27.png)