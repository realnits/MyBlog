---
author: Nithissh S
pubDatetime: 2024-11-21T15:22:00Z
modDatetime: 2024-11-21T09:12:47.400Z
title: Exploiting XXE using external entities to retrieve files
slug: xxe-portswigger-lab-1
featured: false
draft: false
tags:
  - BSCP
  - XXE
description:
  This lab has a `"Check stock"` feature that parses XML input and returns any unexpected values in the response. The lab server is running a (simulated) EC2 metadata endpoint at the default URL, which is `http://169.254.169.254/`. This endpoint can be used to retrieve data about the instance, some of which might be sensitive. To solve the lab, exploit the XXE vulnerability to perform an SSRF attack that obtains the server's IAM secret access key from the EC2 metadata endpoint. 
---

## Objective 

This lab has a "Check stock" feature that parses XML input and returns any unexpected values in the response.

To solve the lab, inject an XML external entity to retrieve the contents of the `/etc/passwd` file. 

## Solution 

In the `check stock` functionality showcases that the request goes through `POST` method and takes an XML body as input like `storeId` and `productId` and shows how many stocks left in the particular region 

![](../../assets/images/bscp/xxe/xxe-1.png)

Now we know that it has te ability the parse the XML body and with the following payload

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE foo [ <!ENTITY xxe SYSTEM "file:///etc/passwd"> ]>
<stockCheck><productId>&xxe;1</productId><storeId>1</storeId></stockCheck>
```

where it will define the external entity `&xxe`within the `productId` and points to the contents of `/etc/passwd` as a value and now we can send the request and which will actually disclose the contents of `/etc/passwd`

![](../../assets/images/bscp/xxe/xxe-3.png)

Achieved the objective and that solves the lab 

![](../../assets/images/bscp/xxe/xxe-2.png)