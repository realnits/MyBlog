---
author: Nithissh S
pubDatetime: 2024-10-15T15:22:00Z
modDatetime: 2024-10-15T09:12:47.400Z
title: User role controlled by request parameter
slug: ac-portswigger-lab-13
featured: false
draft: false
tags:
  - BSCP
  - Access Control
description:
  This lab has an admin panel at /admin, which identifies administrators using a forgeable cookie. Solve the lab by accessing the admin panel and using it to delete the user carlos. You can log in to your own account using the following credentials wiener:peter
---

## Introduction

This lab has an admin panel at `/admin`, which identifies administrators using a forgeable cookie.

Solve the lab by accessing the admin panel and using it to delete the user carlos.

You can log in to your own account using the following credentials: wiener:peter

## Solution

As mentioned in the lab description, we were able to login as wiener with the following credentials which is `wiener:peter`

![](../../assets/images/bscp/access-control/access-8.png)

Acccessing the `/admin` path shows that Only admin can access this interface which means we need to find a way to escalate our privilege to admin 

![](../../assets/images/bscp/access-control/access-9.png)

But the checking `Cookie:` Header shows that there is an additional attribute exists inside a cookie which is `Admin` and the value is set to `false`

![](../../assets/images/bscp/access-control/access-10.png)

Changing the `Admin` from `false` to `true` shows a new tab called `Admin panel` which didn't exists previously which means our privilege got escalated 

![](../../assets/images/bscp/access-control/access-11.png)

Access the admin panel tab, delete the user called `carlos` and lab will be solved 

![](../../assets/images/bscp/access-control/access-12.png)