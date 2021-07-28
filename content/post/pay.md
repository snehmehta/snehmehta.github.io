---
draft: false
title: "Monetizing Flutter app with Google and Apple Pay"
date: 2021-05-19T11:02:33+05:30
author: Sneh Mehta
image_webp: images/blog/pay.png
image: images/blog/pay.png
description : "Monetizing Flutter app with Google and Apple Pay"
---

At Google I/O, Flutter team announce Flutter 2.2. Major focus areas are :-
- Null safety by default
- Monetize via ads, in-app-purchase and pay plugin.

We'll be focusing on the new payment plugin **Pay**

Why specific pay instead of any other payment gateway reason being both Google pay and specifically Apple pay both are native payment gateway most of iPhones and Android phones has pre-installed



- Sign up to the business console and create an account. [Business Account Link](https://pay.google.com/business/console/ "Google Pay Business")

## 1. Android

### 1.1. Adding app/build.gradle dependency
   
```gradle
dependencies {
    implementation 'com.google.android.gms:play-services-wallet:18.1.2'
    implementation 'com.android.support:appcompat-v7:24.1.1'
}
```

### 1.2. Google pay meta data to AndroidManifest

```xml
<meta-data
  android:name="com.google.android.gms.wallet.api.enabled"
  android:value="true" />
```

### 1.3. Adding Payment profile

This can be added in assets folder or called dynamically via api.

```json
{
    "provider": "google_pay",
    "data": {
      "environment": "TEST",
      "apiVersion": 2,
      "apiVersionMinor": 0,
      "allowedPaymentMethods": [
        {
          "type": "CARD",
          "tokenizationSpecification": {
            "type": "PAYMENT_GATEWAY",
            "parameters": {
              "gateway": "example",
              "gatewayMerchantId": "gatewayMerchantId"
            }
          },
          "parameters": {
            "allowedCardNetworks": ["VISA", "MASTERCARD"],
            "allowedAuthMethods": ["PAN_ONLY", "CRYPTOGRAM_3DS"],
            "billingAddressRequired": true,
            "billingAddressParameters": {
              "format": "FULL",
              "phoneNumberRequired": true
            }
          }
        }
      ],
      "merchantInfo": {
        "merchantId": "BCRxxxxxxxxxxQYU",
        "merchantName": "Webvoke"
      },
      "transactionInfo": {
        "countryCode": "IN",
        "currencyCode": "INR"
      }
    }
}
```
