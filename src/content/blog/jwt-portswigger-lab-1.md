---
author: Nithissh S
pubDatetime: 2024-12-09T02:29:00Z
modDatetime: 2024-12-09T02:29:47.400Z
title: JWT authentication bypass via weak signing key
slug: jwt-portswigger-lab-1
featured: false
draft: false
tags:
  - BSCP
  - JWT Attacks
description:
    This lab uses a JWT-based mechanism for handling sessions. It uses an extremely weak secret key to both sign and verify tokens. This can be easily brute-forced using a wordlist of common secrets. To solve the lab, first brute-force the website's secret key. Once you've obtained this, use it to sign a modified session token that gives you access to the admin panel at /admin, then delete the user carlos. You can log in to your own account using the following credentials wiener:peter   
---

## Objective 

This lab uses a JWT-based mechanism for handling sessions. It uses an extremely weak secret key to both sign and verify tokens. This can be easily brute-forced using a wordlist of common secrets.

To solve the lab, first brute-force the website's secret key. Once you've obtained this, use it to sign a modified session token that gives you access to the admin panel at `/admin`, then delete the user `carlos`.

You can log in to your own account using the following credentials: `wiener:peter` 

## Solution 

After logging in as wiener user with the credentials provided from the lab objective and on suuccessful authentication.. we will have a token in the format of `base64` 

![](../../assets/images/bscp/jwt/jwt-1.png)

Decoding the jwt token, we can see that it uses `HS256` Algorithm... 

![](../../assets/images/bscp/jwt/jwt-2.png)

If we have to change the value like from `wiener` to `administrator` you need a valid signature to change it or you will face an error called `Invalid Signature` and accessing `/admin` path also results in `401`

Now we need to crack the signature value via bruteforce attack and for that we need two things:

1. [JWT Tool to fuzz and tamper](https://github.com/ticarpi/jwt_tool)
2. [Wordlist mentioned in lab objective](https://raw.githubusercontent.com/wallarm/jwt-secrets/refs/heads/master/jwt.secrets.list)

Once after everything, we can run the following command by taking JWT token and the wordlist that we gonna use for bruteforce.. Found that `secret1` is the correct signature value 

```sh
nits@FWS-CHE-LT-8869 jwt_tool % python3 jwt_tool.py eyJraWQiOiJlNWI0ZWIzYi0wZjRkLTRkYTktYTI2Yy1lYTVhNWJlMzg5MDMiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJwb3J0c3dpZ2dlciIsImV4cCI6MTczMzc0MjM5MCwic3ViIjoid2llbmVyIn0.oC57WdP43l4mPnQjW-ymMmfoOifkfwsL9x7GEN765Xc -C -d jwt.secrets.list    

Original JWT: 

[+] secret1 is the CORRECT key!
```

We can tamper the jwt token using `jwt.io`

![](../../assets/images/bscp/jwt/jwt-3.png)

Utilise the tampered jwt token to access the `/admin` and yeah, we were able to access the admin panel 

![](../../assets/images/bscp/jwt/jwt-4.png)

Now we can just the delete the user called `carlos` and the lab is solved

![](../../assets/images/bscp/jwt/jwt-5.png)