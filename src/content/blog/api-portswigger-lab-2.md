---
author: Nithissh S
pubDatetime: 2024-11-11T15:22:00Z
modDatetime: 2024-11-11T09:12:47.400Z
title: Exploiting server-side parameter pollution in a query string
slug: api-portswigger-lab-2
featured: false
draft: false
tags:
  - BSCP
  - API
description:
  To solve the lab, exploit a hidden API endpoint to buy a Lightweight l33t Leather Jacket. You can log in to your own account using the following credentials `wiener:peter` 
---

## Objective 

To solve the lab, exploit a hidden API endpoint to buy a Lightweight l33t Leather Jacket. You can log in to your own account using the following credentials: `wiener:peter`

## Solution 

We found an API endpoint where it reveals the price of the product through the javascript file which is present in `/resources/js/api/productPrice.js` 

```js
const loadPricing = (productId) => {
    const url = new URL(location);
    fetch(`//${url.host}/api/products/${encodeURIComponent(productId)}/price`)
        .then(res => res.json())
        .then(handleResponse(getAddToCartForm()));
};
```

The API endpoint looks like this `/api/products/1/price` which will present the data in a JSON format 

![](../../assets/images/bscp/api/api-3.png)

Checking the `OPTIONS` method shows only we can send `GET` and `PATCH` and based on that, I've changed it from `GET` to `PATCH` method and updated the `Content-Type` to `application/json` with an empty json payload and it revealed that it needs `price` parameter to be passed

![](../../assets/images/bscp/api/api-4.png)

Finally, updated the parameter and set the price to `0` and request successfully passes through... responded with price of product is set to the value of `$0.00`

![](../../assets/images/bscp/api/api-5.png)

Now from UI part, Add the product and checkout.. Now we don't face the `No credits issue` since the product is at `$0.00` and we can checkout.. That solves the lab 

![](../../assets/images/bscp/api/api-6.png)