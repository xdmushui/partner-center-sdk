---
title: Gets a list of current promotions for a give segment and market
description: Gets a list of current promotions for a give segment and market.
ms.date: 02/23/2021
ms.service: partner-dashboard
ms.subservice:  partnercenter-sdk
author: BrentSerbus
ms.author: brserbus
---

# Get promotions

**Applies To**

- Partner Center

**Appropriate roles**

- Global admin
- Admin agent

> [!Note] 
> New Commerce changes are currently available only to partners who are part of the Microsoft 365 and Dynamics 365 new commerce experience technical preview.

Partners can get a list of active new commerce promotions for a given market (country) and segment. This method returns available current promotions based on the promotions available start and end dates.

## Prerequisites

- Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.

- Segment represents the type of customer the promotions are enabled for. Currently supports only commercial.

- Country represents the customer country promotions are available for. Country is represented by a two character country code.

## REST request
[GET] /v1/productpromotions?country={country-code};segment={segment}
### Request syntax

| Method   | Request URI                                                                                                                         |
|----------|-------------------------------------------------------------------------------------------------------------------------------------|
| **GET**  | [*{baseURL}*](partner-center-rest-urls.md)/v1/productpromotions?country={country-code};segment={segment} HTTP/1.1 |

### URI parameter

Use the following query parameters to return available promotions.

| Name                    | Type     | Required | Description                                       |
|-------------------------|----------|----------|---------------------------------------------------|
| **segment**  | **string** | Y        | A string that determines which promotions are available for a given segment.             |
| **country** | **guid** | Y        | A two letter country code determining which customer country promotions are available for. |

### Request headers

For more information, see [Partner Center REST headers](headers.md).

### Request body

None

### Request example

```http
GET https://api.partnercenter.microsoft.com/v1/productpromotions?country=UK;segment=commercial HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
X-Locale: en-US
```

## REST response

If successful, this method returns a list of promotions.

### Response success and error codes

Each response comes with an HTTP status code that indicates success or failure and more debugging information. Use a network trace tool to read this code, error type, and more parameters. For the full list, see [Error Codes](error-codes.md).

### Response example

```http
HTTP/1.1 200 OK
Content-Length: 138
Content-Type: application/json
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
Date: Fri, 26 Feb 2021 20:42:26 GMT


   {
    "totalCount": 33,
    "items": [
        {
            "id": "CFQ7TTC0HL8W;0001;CFQ7TTC0K59M",
            "name": "Promotion discount at 25% E5 1Y term",
            "description": "Promotion discount for E5.",
            "segment": "commercial",
            "requiredProducts": [
                {
                    "productId": "CFQ7TTC0LHQZ",
                    "skuId":"0001",
                    "term": {
                       "duration": "P3Y",
                       "billingCycle": "Annual"
                    },
                    "pricingPolicies": [
                        {
                            "type": "PercentDiscount",
                            "value": "0.25"
                        }]
                }
            ],
            "properties": {
                    "startDate": "2021-06-05T00:00:00Z",
                    "endDate": "2021-06-12T23:59:59Z",
                    "tag": "HashOfProductSku"
            }
        }…
  }
```
