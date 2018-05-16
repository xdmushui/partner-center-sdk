---
title: Get a list of products
description: Gets a collection of products.
ms.assetid: 5E4160AB-6B73-4CA1-903D-7257927CA754
ms.author: v-thpr
ms.date: 03/20/2018
ms.topic: article
ms.prod: partner-center
ms.technology: partner-center-sdk
---

# Get a list of products


**Applies To**

-   Partner Center

Gets a collection of products.

## <span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>Prerequisites


-   Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.

## <span id="C_"></span><span id="c_"></span>C#


To get a list of products, use your **IAggregatePartner.Products** collection, select the country by using the **ByCountry()** method, select the catalog view by using the **ByTargetView()** method, and optionally select the target segment by using the **ByTargetSegment()** method. Finally, call the **Get()** or **GetAsync()** method to return the collection. 

```CSharp
IAggregatePartner partnerOperations;

// Get the products for the specified catalog view.
ResourceCollection<Products> products = partnerOperations.Products.ByCountry("US").ByTargetView("Azure").Get();

// Get the products filtered by target view and target segment.
ResourceCollection<Products> products = partnerOperations.Products.ByCountry("US").ByTargetView("Azure").ByTargetSegment("commercial").Get();
```

## <span id="REST_Request"></span><span id="rest_request"></span><span id="REST_REQUEST"></span>REST Request


**Request syntax**

| Method  | Request URI                                                                                                                                    |
|---------|----------------------------------------------------------------------------------------------------------------------------------------------- |
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/products?country={country}&targetView={targetView}&targetSegment={targetSegment} HTTP/1.1    |

 

**URI parameters**

Use the following path and query parameters to get a list of products.

| Name                   | Type     | Required | Description                                                             |
|------------------------|----------|----------|-------------------------------------------------------------------------|
| country                | string   | Yes      | The country/region ID.                                                  |
| targetView             | string   | Yes      | Identifies the target view of the catalog. The supported values are:<br/> Azure - Includes all Azure items.<br/> OnlineServices - Includes all online service items.                      |
| targetSegment          | string   | No       | Identifies the target segment. The view for different target audiences. The supported values are: <br/> commercial<br/> education<br/> government<br/> nonprofit |

 

**Request headers**

-   See [Headers](headers.md) for more information.

**Request body**

None.

**Request example**

```
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=Azure HTTP/1.1
Authorization: Bearer 
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

## <span id="Response"></span><span id="response"></span><span id="RESPONSE"></span>Response


If successful, the response body contains a collection of [Product](products.md#product) resources.

**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center error codes](error-codes.md).

This method returns the following error codes:

| HTTP Status Code     | Error code   | Description                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| 403                  | 400030       | Access to the requested targetSegment is not allowed.                                                     |
| 403                  | 400036       | Access to the requested targetView is not allowed.                                                        | 


**Response example**

```
{
    "totalCount": 19,
    "items": [
        {
            "id": "DZH318Z0BQ3Q",
            "title": "DSv2 Series",
            "description": "Persistent storage disks are billed separately from virtual machines. To use premium storage disks, use the variant “Dsv2” virtual machines. The pricing and billing meters for Dsv2 sizes are the same as Dv2-series.  ",
            "productType": {
                “id”: "Azure",
                “displayName”: “Azure”,
            }, 
            "links": {
                "skus": {
                    "uri": "/products/DZH318Z0BQ3Q/skus?country=US",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/products/DZH318Z0BQ3Q?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        },
        …
    ],
    "links": {
        "self": {
            "uri": "/products?country=US&targetView=Azure",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

 

 




