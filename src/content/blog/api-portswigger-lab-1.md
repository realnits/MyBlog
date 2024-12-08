---
author: Nithissh S
pubDatetime: 2024-11-11T15:22:00Z
modDatetime: 2024-11-11T09:12:47.400Z
title: Exploiting an API endpoint using documentation
slug: api-portswigger-lab-1
featured: false
draft: false
tags:
  - BSCP
  - API
description:
  To solve the lab, find the exposed API documentation and delete carlos. You can log in to your own account using the following credentials `wiener:peter`
---

## Objective 

To solve the lab, find the exposed API documentation and delete carlos. You can log in to your own account using the following credentials: `wiener:peter`

## Solution 

Once after login with the credentials provided: `wiener:peter` accessing the path `/api` shows that there is a API documentation being available over there 

![](../../assets/images/bscp/api/api-1.png)

In order to solve the lab, we need to delete the user called `carlos` and for that, just select the `DELETE` and enter the username as `carlos` and where it will generate the following curl command 

```sh
curl -vgw "\n" -X DELETE 'https://0a4c000c03e6ddba8333d83000c800fc.web-security-academy.net/api/user/carlos' -d '{}'
```

And click on `Send Request` and API call goes through and show the `User deleted` and we solved the lab 

![](../../assets/images/bscp/api/api-2.png)