---
title: Get a list of availabilities for a SKU
description: Gets a collection of availabilities for the specified product and SKU.
ms.assetid: 5E4160AB-6B73-4CA1-903D-7257927CA754
ms.date: 03/20/2018
ms.localizationpriority: medium
---

# Get a list of availabilities for a SKU


**Applies To**

- Partner Center

Gets a collection of availabilities for the specified product and SKU.

## <span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>Prerequisites


- Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.
- A product ID. 
- A SKU ID. 

## <span id="C_"/><span id="c_"/>C#


To get the list of [availabilities](products.md#availability) for a [SKU](products.md#sku), start by using following the steps in [Get a SKU by ID](get-a-sku-by-id.md) to get the interface for a specific sku's operations. From the resulting interface, select the **Availabilities** property to obtain an interface with the operations for availabilities. Finally, call **Get()** or **GetAsync()** to retrieve a collection of the availabilities for this SKU. Optionally, you can use the **ByTargetSegment()** method to filter the availabilities by target segment before calling **Get()** or **GetAsync()**.

``` csharp
IAggregatePartner partnerOperations;
string countryCode;
string productId; 
string skuId;
string targetSegment;

// Get the availabilities.
var availabilities = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.ById(skuId).Availabilities.Get();

// Get the availabilities, filtered by target segment.
var availabilities = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.ById(skuId).Availabilities.BySegment(targetSegment).Get();
```

## <span id="REST_Request"/><span id="rest_request"/><span id="REST_REQUEST"/>REST Request


**Request syntax**

| Method  | Request URI                                                                                                                              |
|---------|------------------------------------------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/products/{product-id}/skus/{sku-id}/availabilities?country={country-code}&targetSegment={target-segment} HTTP/1.1     |

 

**URI parameter**

Use the following path and query parameters to get a list of availabilities for a SKU.

| Name                   | Type     | Required | Description                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| product-id             | string   | Yes      | A string that identifies the product.                           |
| sku-id                 | string   | Yes      | A string that identifies the SKU.                               |
| country-code           | string   | Yes      | A country/region ID.                                            |
| target-segment         | string   | No       | A string that identifies the target segment used for filtering. |

 

**Request headers**

- See [Headers](headers.md) for more information.

**Request body**

None.

**Request example**

```http
GET http:// api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ3Q/skus/0001/availabilities?country=US&segment=commercial HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 70324727-62d8-4195-8f99-70ea25058d02
MS-CorrelationId: 83b644b5-e54a-4bdc-b354-f96c525b3c58
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Host: api.partnercenter.microsoft.com
```

## <span id="Response"/><span id="response"/><span id="RESPONSE"/>Response


If successful, the response body contains a collection of [SKU](products.md#sku) resources.

**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center error codes](error-codes.md).

This method returns the following error codes:

| HTTP Status Code     | Error code   | Description                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| 403                  | 400030       | Access to the requested targetSegment is not allowed.                                                     |


**Response example**

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Server: Microsoft-IIS/10.0
MS-CorrelationId: 83b644b5-e54a-4bdc-b354-f96c525b3c58,83b644b5-e54a-4bdc-b354-f96c525b3c58
MS-RequestId: 70324727-62d8-4195-8f99-70ea25058d02,70324727-62d8-4195-8f99-70ea25058d02
X-Locale: en-US,en-US
X-SourceFiles: =?UTF-8?B?QzpcVXNlcnNcbWFtZW5kZVxkZXZcZHBzLXJwZVxSUEUuUGFydG5lci5TZXJ2aWNlLkNhdGFsb2dcV2ViQXBpc1xDYXRhbG9nU2VydmljZS5WMi5XZWJcdjFccHJvZHVjdHNcRFpIMzE4WjBCUTNRXHNrdXNcMDAwMVxhdmFpbGFiaWxpdGllcw==?=
X-Powered-By: ASP.NET
Date: Wed, 14 Mar 2018 22:19:37 GMT
Content-Length: 808

{
    "totalCount": 1,
    "items": [
        {
            "id": "DZH318Z0HMKQ",
            "productId": "DZH318Z0BQ3Q",
            "skuId": "0001",
            "catalogItemId": "DZH318Z0BQ3Q:0001:DZH318Z0HMKQ",
            "defaultCurrency": {
                "code": "USD",
                "symbol": "$"
            },
            "segment": "commercial",
            "country": "US",
            "links": {
                "self": {
                    "uri": "/products/DZH318Z0BQ3Q/skus/0001/availabilities/DZH318Z0HMKQ?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/products/DZH318Z0BQ3Q/skus/0001/availabilities?country=US&targetSegment=commercial",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

