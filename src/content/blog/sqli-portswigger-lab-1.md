---
author: Nithissh S
pubDatetime: 2024-09-06T15:22:00Z
modDatetime: 2024-09-06T09:12:47.400Z
title: SQL injection attack, querying the database type and version on MySQL and Microsoft
slug: sqli-portswigger-lab-1
featured: false
draft: false
tags:
  - BSCP
  - SQL Injection
description:
  This lab contains a SQL injection vulnerability in the product category filter. You can use a UNION attack to retrieve the results from an injected query. To solve the lab, display the database version string. 
---

## Objective 

This lab contains a SQL injection vulnerability in the product category filter. You can use a UNION attack to retrieve the results from an injected query.

To solve the lab, display the database version string. 

## Solution

Same like the other previous labs, we have potential SQLi vulnerability in the product category filter part 

![](../../assets/images/bscp/sqli/sqli27.png)

With the following payload `'+UNION+SELECT+NULL,NULL#` , we were able to determine that we have two columns and the reason I used `#` instead off `--` is due to MSSQL. because MSSQL doesn't support `--` for commenting

![](../../assets/images/bscp/sqli/sqli28.png)

We have control over both the columns and that's a good thing actually 

![](../../assets/images/bscp/sqli/sqli28.png)

Then what ?!! well we need to identify the version and type of database being used on mysql and mssql.. Looking into the cheatsheet mentioned earlier for both MSSQL and MySQL we can dump the version using this query `SELECT @@version` 

And with the following payload `'+UNION+SELECT+@@version,NULL# ` we can actually dump the database version from the response and one more thing add to remember here we had control over both the column and we chose the fiest one 

![](../../assets/images/bscp/sqli/sqli30.png)