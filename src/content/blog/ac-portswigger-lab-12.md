---
author: Nithissh S
pubDatetime: 2024-10-15T15:22:00Z
modDatetime: 2024-10-15T09:12:47.400Z
title: User role can be modified in user profile
slug: ac-portswigger-lab-12
featured: false
draft: false
tags:
  - BSCP
  - Access Control
description:
  This lab has an admin panel at /admin. It's only accessible to logged-in users with a roleid of 2. Solve the lab by accessing the admin panel and using it to delete the user carlos. You can log in to your own account using the following credentials wiener:peter 
---

## Introduction

This lab has an admin panel at `/admin`. It's only accessible to logged-in users with a roleid of 2.

Solve the lab by accessing the admin panel and using it to delete the user carlos.

You can log in to your own account using the following credentials: wiener:peter 

## Solution

Once after login with the credentials `wiener:peter` they provided in the lab objective and post login, we have the functionality to update the email ID 

![](../../assets/images/bscp/access-control/access-13.png)

Simply we can update the email like just say `admin@test.com` and Now the Intercept in burp, we can observe that post body goes in a JSON format and In the response, we got the exact attribute to change the role ID which is `roleid` in the reponse which sets to `1`

![](../../assets/images/bscp/access-control/access-14.png)

Now from our own request in the POST body, pass the attribute called `roleid` which sets the value to `2` , send the request and as you can observe the response, the `roleid` is changed from `1` to `2`

![](../../assets/images/bscp/access-control/access-15.png)

Now we are able to access the admin panel with the following path `/admin` which was previously blocked and delete the user called `carlos` to solve the lab 

![](../../assets/images/bscp/access-control/access-16.png)