---
title: Check eligibility for upgrade from Azure 145P to Azure Plan
description: How to check eligibility for a customer to upgrade from Azure 145P to Azure Plan. This would return a value indicating customer's eligibility for product upgrade.
ms.date: 10/04/2019
ms.localizationpriority: medium
---

# Check eligibility for upgrade from Azure 145P to Azure Plan

Applies To

- Partner Center

How to check eligibility for upgrade from Azure 145P to Azure Plan for the specified customer. This would return a value indicating customer's eligibility for product upgrade.

## Prerequisites

- Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with App+User credentials. Follow the [secure app model](enable-secure-app-model.md) when using App+User authentication with Partner Center APIs.
- The customer identifier.
- The product family.

## C\#

## REST request

### Request syntax

| Method   | Request URI                                                                                   |
|----------|-----------------------------------------------------------------------------------------------|
| **POST** | [*{baseURL}*](partner-center-rest-urls.md)/v1/productUpgrades/eligibility HTTP/1.1 |


### Request headers

See [Partner Center REST headers](headers.md) for more information.

### Request body

The request body must contain a [ProductUpgradeRequest](product-upgrade-resources.md#ProductUpgradeRequest) resource.

### Request example

```http
POST https://api.partnercenter.microsoft.com/v1/productupgrades HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: c245d5f2-1de3-4ae0-9e42-95e38e3cb8ff
MS-CorrelationId: e3f26e6a-044f-4371-ad52-0d91ce4200be
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 340
Expect: 100-continue
Connection: Keep-Alive
{
 {
	"customerId": "4c721420-72ad-4708-a0a7-371a2f7b0969",
	"productFamily": "azure"
  }
  "Attributes": {
  "ObjectType": "ProductUpgradeRequest"
  }
}
```

## REST response

If successful, this method returns [ProductUpgradesEligibility](product-upgrade-resources.md) resource in the body.

### Response success and error codes

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center REST error codes](error-codes.md).

### Response example

```http
HTTP/1.1 200 Ok
Content-Length: 150
MS-CorrelationId: 772871a9-399b-4f3b-b8c7-38f550e4f22a
MS-RequestId: cb82f7d6-f0d9-44d4-82f9-f6eee6e68390
MS-CV: iqOqN0FnaE2y0HcD.0
MS-ServerId: 030020525
Date: Thu, 04 Oct 2019 20:35:35 GMT

{
    "customerId": "c1958bc7-3284-4952-a257-de594ee64743",
    "isEligible": true,
    "productFamily": "azure"
}
```
