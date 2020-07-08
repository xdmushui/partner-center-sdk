---
title: Get a list of offer categories by market
description: How to get a collection that contains all the offer categories in a given country/region and locale.
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice:  partnercenter-sdk
author: amitravat
ms.author: amrava
---

# Get a list of offer categories by market

**Applies to:**

- Partner Center
- Partner Center operated by 21Vianet
- Partner Center for Microsoft Cloud Germany
- Partner Center for Microsoft Cloud for US Government

This article describes how to get a collection that contains all the offer categories in a given country/region and locale.

## Prerequisites

- Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.

## C\#

To get a list of offer categories in a given country/region and locale:

1. Use your [**IAggregatePartner.Operations**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.iaggregatepartner) collection to call the [**With()**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.iaggregatepartner.with) method on a given context.

2. Inspect the [**OfferCategories**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.ipartner.offercategories) property of the resulting object.

``` csharp
// IAggregatePartner partnerOperations;

ResourceCollection<OfferCategory> offerCategoryResults = partnerOperations.With(RequestContextFactory.Instance.Create()).OfferCategories.ByCountry("US").Get();
```

For an example, see the following:

- Sample: [Console test app](console-test-app.md)
- Project: **PartnerSDK.FeatureSample**
- Class: **PartnerSDK.FeatureSample**

## REST request

### Request syntax

| Method  | Request URI                                                                                  |
|---------|----------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/offercategories?country={country-id} HTTP/1.1 |

#### URI parameter

This table lists the required query parameters to get the offer categories.

| Name           | Type       | Required | Description            |
|----------------|------------|----------|------------------------|
| **country-id** | **string** | Y        | The country/region ID. |

### Request headers

A **locale-id** formatted as a string is required.

For more information, see [Partner Center REST headers](headers.md).

### Request body

None.

### Request example

```http
GET https://api.partnercenter.microsoft.com/v1/offercategories?country=<country-id> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4fb54bd5-a4c3-4fac-955f-9b6e3436d606
MS-CorrelationId: 47882653-eaed-4a2e-a552-1070a3fa1089
X-Locale: <locale-id>
Connection: Keep-Alive
```

## REST response

If successful, this method returns a collection of **OfferCategory** resources in the response body.

### Response success and error codes

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For a full list, see [Error Codes](error-codes.md).

### Response example

```http
HTTP/1.1 200 OK
Content-Length: 1184
Content-Type: application/json
MS-CorrelationId: 47882653-eaed-4a2e-a552-1070a3fa1089
MS-RequestId: 4fb54bd5-a4c3-4fac-955f-9b6e3436d606
Date: Thu, 26 Nov 2015 00:07:10 GMT

{
    "totalCount": 4,
    "items": [{
        "id": "Enterprise_Key",
        "name": "Enterprise",
        "rank": 20,
        "locale": "en-us",
        "country": "US",
        "attributes": {
            "objectType": "OfferCategory"
        }
    },
    {
        "id": "SmallBusiness_Key",
        "name": "SmallBusiness",
        "rank": 30,
        "locale": "en-us",
        "country": "US",
        "attributes": {
            "objectType": "OfferCategory"
        }
    },
    {
        "id": "Government_Key",
        "name": "Government",
        "rank": 40,
        "locale": "en-us",
        "country": "US",
        "attributes": {
            "objectType": "OfferCategory"
        }
    },
    {
        "id": "Internal_Key",
        "name": "Internal",
        "rank": 100,
        "locale": "en-us",
        "country": "US",
        "attributes": {
            "objectType": "OfferCategory"
        }
    }],
    "attributes": {
        "objectType": "Collection"
    }
}
```
