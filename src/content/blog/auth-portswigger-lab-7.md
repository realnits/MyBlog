---
author: Nithissh S
pubDatetime: 2024-10-18T15:22:00Z
modDatetime: 2024-10-18T09:12:47.400Z
title: 2FA broken logic
slug: auth-portswigger-lab-7
featured: false
draft: false
tags:
  - BSCP
  - Authentication
description:
  This lab's two-factor authentication is vulnerable due to its flawed logic. To solve the lab, access Carlos's account page. 
---

## Objective 

<body>
  <p>
    This lab's two-factor authentication is vulnerable due to its flawed logic. To solve the lab, access Carlos's account page.  
  </p>
  <ul>
    <li>Your credentials: wiener:peter</li>
    <li>Victim's username: carlos</li>
  </ul>
  <p>You also have access to the email server to receive your 2FA verification code.</p>
</body>

## Solution

Once after login with the `wiener` user... It says us to enter the 4 digit code which we recieved through our email client 

![](../../assets/images/bscp/auth/auth-35.png)

Checking the email client, we can confirm that we have received our 4 digit code 

![](../../assets/images/bscp/auth/auth-36.png)

Now entered some random code on to OTP page and intercepted the request.. Then after changed value inside the cookie from `verify=wiener` to `verify=carlos` because our target is to get logged in as `carlos` and started the bruteforce attack for the four digit pin 

And placeholder is set to `mfa=$$` and then payload type is `numbers` from `0000 to 9999` 

![](../../assets/images/bscp/auth/auth-36.png)

Once after identifying the code with `302` and opening the response on to the browser that solves the lab 