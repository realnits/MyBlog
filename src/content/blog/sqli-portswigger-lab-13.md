---
author: Nithissh S
pubDatetime: 2024-09-10T15:22:00Z
modDatetime: 2024-09-10T09:12:47.400Z
title: Blind SQL injection with time delays
slug: sqli-portswigger-lab-13
featured: false
draft: false
tags:
  - BSCP
  - SQL Injection
description:
  This lab contains a blind SQL injection vulnerability. The application uses a tracking cookie for analytics, and performs a SQL query containing the value of the submitted cookie. The results of the SQL query are not returned, and the application does not respond any differently based on whether the query returns any rows or causes an error. However, since the query is executed synchronously, it is possible to trigger conditional time delays to infer information. To solve the lab, exploit the SQL injection vulnerability to cause a 10 second delay.   
---

## Objective 

This lab contains a blind SQL injection vulnerability. The application uses a tracking cookie for analytics, and performs a SQL query containing the value of the submitted cookie.

The results of the SQL query are not returned, and the application does not respond any differently based on whether the query returns any rows or causes an error. However, since the query is executed synchronously, it is possible to trigger conditional time delays to infer information.

To solve the lab, exploit the SQL injection vulnerability to cause a 10 second delay. 

## Solution 

This lab is just like previous lab where we saw about exploiting time based sql injection through `TrackingId` inside the cookie and utilize the `PostgreSQL` database 

Now In order to cause the time delay of 10 seconds we can enter the following payload `n' || pg_sleep(10)--` where it will concatenate and sleep is executed and then ignores rest of the sql query 

As you can see in the below image, it caused a 10 seconds delay 

![](../../assets/images/bscp/sqli/sqli51.png)

Our objective is achieved and the lab is solved 

![](../../assets/images/bscp/sqli/sqli52.png)