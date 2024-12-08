---
author: Nithissh S
pubDatetime: 2024-10-16T15:22:00Z
modDatetime: 2024-10-16T09:12:47.400Z
title: SSRF with blacklist-based input filters
slug: ssrf-portswigger-lab-4
featured: false
draft: false
tags:
  - BSCP
  - SSRF
description:
  This lab has a stock check feature which fetches data from an internal system. To solve the lab, change the stock check URL to access the admin interface at http://localhost/admin and delete the user carlos. The developer has deployed two weak anti-SSRF defenses that you will need to bypass. 
---

## Introduction

This lab has a stock check feature which fetches data from an internal system.

To solve the lab, change the stock check URL to access the admin interface at http://localhost/admin and delete the user carlos.

The developer has deployed two weak anti-SSRF defenses that you will need to bypass. 

## Solution

Like the same previous labs, there is a SSRF vulnerability exists in **Check Stock unit** and this time through `stockApi` parameter through an external URL it checks for stocks 

![](../../assets/images/bscp/ssrf/ssrf-15.png)

But when send a request to `http://localhost` via `stockApi` parameter and our request is blocked for a security reason 

![](../../assets/images/bscp/ssrf/ssrf-16.png)

What's the other way than, we can actually utilise certain filter bypass like `spoofed.<burpcollab>.com` resolving this points to `127.0.0.1` as mentioned in burp documentation and let's analyse the response of it 

Analysing the response and it says **"Invalid Host"** ?? Then I've sent a wrong payload here 

![](../../assets/images/bscp/ssrf/ssrf-17.png)

Even with `spoofed.burpcollaborator.com` which actually points to `127.0.0.1` results in status code of `500`

![](../../assets/images/bscp/ssrf/ssrf-18.png)

I've added `/admin` to the specific host but still I'm blocked 

![](../../assets/images/bscp/ssrf/ssrf-19.png)

With the following shortened localhost address which `http://127.1` is allowed and responds with `200` along with hold to an admin panel 

![](../../assets/images/bscp/ssrf/ssrf-20.png)

Now add `/admin` to access the admin panel but hey there is an restriction out there but it might be due to the naming of admin or what ?

![](../../assets/images/bscp/ssrf/ssrf-21.png)

Then it might be due to the naming restriction where 

<table border="1">
  <tr>
    <th>admin.</th>
    <th>Blocked</th>
  </tr>
  <tr>
    <td>Admin</td>
    <td>Allowed and not blacklisted.</td>
  </tr>
</table>

Changing it from `/admin` to `/Admin` it allows the access to admin panel and shows the option to delete the users.. which is awesome 

![](../../assets/images/bscp/ssrf/ssrf-22.png)

Finally send the following url `http://127.1/Admin/delete?username=carlos` as a value for `stockApi` parameter and send the request, carlos user will be deleted and lab is solved 

![](../../assets/images/bscp/ssrf/ssrf-23.png)