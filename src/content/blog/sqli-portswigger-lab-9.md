---
author: Nithissh S
pubDatetime: 2024-09-09T15:22:00Z
modDatetime: 2024-09-09T09:12:47.400Z
title: SQL injection vulnerability in WHERE clause allowing retrieval of hidden data
slug: sqli-portswigger-lab-9
featured: false
draft: false
tags:
  - BSCP
  - SQL Injection
description:
  This lab contains a SQL injection vulnerability in the product category filter. When the user selects a category, the application carries out a SQL query like the following. To solve the lab, perform a SQL injection attack that causes the application to display one or more unreleased products.   
---

## Objective 

This lab contains a SQL injection vulnerability in the product category filter. When the user selects a category, the application carries out a SQL query like the following:

```sql
SELECT * FROM products WHERE category = 'Gifts' AND released = 1
```

To solve the lab, perform a SQL injection attack that causes the application to display one or more unreleased products. 

## Solution 

Same like the rest other SQL injection labs where we solved and this lab is also vulnerable to SQL injection through a product category filter when we pass `'` through `category` parameter resulted in `500` that's a sign right 

![](../../assets/images/bscp/sqli/sqli42.png)

Viewing the gift filter shows only 3 product and our endgoal is to make it show unreleased products as well 

![](../../assets/images/bscp/sqli/sqli43.png)

With the following payload `' OR 1=1--` where this payload will initially break out of the SQL query and then checks on true or false statement here in our its true right because of 1=1 and once the request is sent, we will able to see some unreleased products.. 

And the lab is solved 

![](../../assets/images/bscp/sqli/sqli44.png)