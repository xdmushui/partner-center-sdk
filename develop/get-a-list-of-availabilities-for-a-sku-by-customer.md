---
title: Get a list of availabilities for a SKU (by customer)
description: How to get a collection of availabilities for the specified product and SKU by customer.
ms.assetid:
ms.date: 10/07/2019
ms.localizationpriority: medium
---

# Get a list of availabilities for a SKU (by customer)

**Applies To**

- Partner Center
- Partner Center operated by 21Vianet
- Partner Center for Microsoft Cloud Germany
- Partner Center for Microsoft Cloud for US Government

Get a collection of availabilities for a specified product and SKU available to a particular customer.

## Prerequisites

- Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.
- A customer identifier (**customer-tenant-id**).
- A product ID (**product-id**).
- A SKU ID (**sku-id**).

## REST

### Rest request

#### Request syntax

| Method | Request URI                                                                                                                 |
|--------|-----------------------------------------------------------------------------------------------------------------------------|
| POST   | [*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/products/{product-id}/skus/{sku-id} HTTP/1.1 |

#### Request URI parameter

| Name               | Type | Required | Description                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| customer-tenant-id | GUID | Yes | The value is a GUID-formatted **customer-tenant-id**, which is an identifier that allows you to specify a customer. |
| product-id | string | Yes | A string that identifies the product. |
| sku-id | string | Yes | A tring that identifies the SKU. |

#### Request header

- See [Headers](headers.md) for more information.

#### Request body

None.

#### Request example

```http
GET https://api.partnercenter.microsoft.com/v1/customers/65543400-f8b0-4783-8530-6d35ab8c6801/products/DZH318Z0BPS6/skus/0001/availabilities HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 83643f5e-5dfd-4375-88ed-054412460dc8
MS-CorrelationId: b1939cb2-e83d-4fb0-989f-514fb741b734
```

### Rest response

#### Response success and error codes

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center error codes](error-codes.md).

This method returns the following error codes:

| HTTP Status Code | Error code | Description |
|------------------|------------|-------------|
| 404 | 400013 | The parent product was not found. |

#### Response example

```http
HTTP/1.1 200 OK
Content-Length: 1909
Content-Type: application/json; charset=utf-8
MS-CorrelationId: cad955c2-8efc-47fe-b112-548ff002ba18
MS-RequestId: ae7288e2-2673-4ad4-8c12-7aad818d5949
{
    "id": "0001",
    "productId": "DZH318Z0BPS6",
    "title": "Microsoft Azure Plan",
    "description": "Microsoft Azure Plan (MS-AZR-0017G)",
    "minimumQuantity": 1,
    "maximumQuantity": 1,
    "isTrial": false,
    "supportedBillingCycles": [
        "one_time"
    ],
    "purchasePrerequisites": [
        "MicrosoftCustomerAgreement"
    ],
    "inventoryVariables": [],
    "provisioningVariables": [],
    "actions": [
        "Refund"
    ],
    "dynamicAttributes": {
        "isMicrosoftProduct": true,
        "pilotProgram": "modernazurepilot"
    },
    "links": {
        "availabilities": {
            "uri": "/products/DZH318Z0BPS6/skus/0001/availabilities?country=US",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/products/DZH318Z0BPS6/skus/0001?country=US",
            "method": "GET",
            "headers": []
        }
    }
}
```
