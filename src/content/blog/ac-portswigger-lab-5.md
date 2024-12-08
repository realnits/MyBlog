---
author: Nithissh S
pubDatetime: 2024-10-15T15:22:00Z
modDatetime: 2024-10-15T09:12:47.400Z
title: Unprotected admin functionality with unpredictable URL
slug: ac-portswigger-lab-5
featured: false
draft: false
tags:
  - BSCP
  - Access Control
description:
  This lab has an unprotected admin panel. It's located at an unpredictable location, but the location is disclosed somewhere in the application. Solve the lab by accessing the admin panel, and using it to delete the user carlos.  
---

## Introduction 

This lab has an unprotected admin panel. It's located at an unpredictable location, but the location is disclosed somewhere in the application.

Solve the lab by accessing the admin panel, and using it to delete the user carlos. 

## Solution

Just looks like the previous lab, but accessing the same admin panel under `/administrator-panel` shows a `404` here means it is `Not Found`

![](../../assets/images/bscp/access-control/access-4.png)

Looking into the page source, we found a different endpoint called `/admin-8dkh40` inside a `isAdmin` javascript function 

![](../../assets/images/bscp/access-control/access-5.png)

Now accessing the following path `/admin-8dkh40` shows the complete admin panel 

![](../../assets/images/bscp/access-control/access-6.png)

Deleting the user called `carlos` will solve the lab 

![](../../assets/images/bscp/access-control/access-7.png)