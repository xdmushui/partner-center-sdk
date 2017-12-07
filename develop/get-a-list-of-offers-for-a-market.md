---
title: Get a list of offers for a market
description: Gets a collection that contains all the offers for a specific market.
ms.assetid: 9251B841-498D-4B20-A90B-EB493A8FF212
ms.author: v-thpr
ms.date: 12/15/2017
ms.topic: article
ms.prod: partner-center
ms.technology: partner-center-sdk
---

# Get a list of offers for a market


**Applies To**

-   Partner Center
-   Partner Center operated by 21Vianet
-   Partner Center for Microsoft Cloud Germany
-   Partner Center for Microsoft Cloud for US Government

Gets a collection that contains all the offers for a specific market.

## <span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>Prerequisites


-   Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.

## <span id="C_"></span><span id="c_"></span>C#


To get a list of offers in a given market, use your **IAggregatePartner.Offers** collection, select the market by country, and call the **Get()** or **Get Async()** method.

```CSharp
// IAggregatePartner partnerOperations;

ResourceCollection<Offer> offers = partnerOperations.Offers.ByCountry("US").Get();
```

**Sample**: [Console test app](console-test-app.md). **Project**: PartnerSDK.FeatureSample **Class**: Offers.cs

## <span id="Request"></span><span id="request"></span><span id="REQUEST"></span>Request


**Request syntax**

| Method  | Request URI                                                                          |
|---------|--------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/offers?country={country\_id} HTTP/1.1 |

 

**URI parameter**

This table lists the required query parameters to get the offers.

| Name           | Type       | Required | Description            |
|----------------|------------|----------|------------------------|
| **country-id** | **string** | Y        | The country/region ID. |

 

**Request headers**

-   A **locale-id** formatted as a string is required.
-   See [Headers](headers.md) for more information.

**Request body**

None.

**Request example**

```
GET https://api.partnercenter.microsoft.com/v1/offers?country=<country-id> HTTP/1.1
Authorization: Bearer 
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
X-Locale: <locale-id>
```

## <span id="Response"></span><span id="response"></span><span id="RESPONSE"></span>Response


If successful, this method returns a collection of **Offer** resources in the response body.

**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Error Codes](error-codes.md).

**Response example**

```
HTTP/1.1 200 OK
Content-Length: 26584
Content-Type: application/json
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
Date: Mon, 23 Nov 2015 23:20:44 GMT

{
    "totalCount":12,"items":[{
        "id":"E60E0348-1710-484B-992A-32B294D4CDE1",
        "name":"Azure Rights Management Premium (Government Pricing)",
        "description":"Microsoft Azure Rights Management Premium helps you protect confidential documents and email with strong encryption.
                       Control the use of your information by specifying who can view, edit, print, save and share your data.
                       Simple to use and integrated with Microsoft Office, SharePoint and Exchange.",
        "minimumQuantity":1,
        "maximumQuantity":10000000,
        "rank":5,
        "uri":"/3c95518e-8c37-41e3-9627-0ca339200f53/Offers/E60E0348-1710-484B-992A-32B294D4CDE1",
        "locale":"EN-US",
        "country":"US",
        "category":{
            "id":"Government_Key",
            "name":"Government",
            "rank":40,
            "locale":"en-us",
            "country":"US",
            "attributes":{
                "objectType":"OfferCategory"
            }
        },
        "prerequisiteOffers":[],
        "isAddOn":false,
        "isAvailableForPurchase":true,
        "billing":"license",
        "isAutoRenewable":true,
        "product":{
            "id":"c52ea49f-fe5d-4e95-93ba-1de91d380f89",
            "name":"Azure Rights Management Premium",
            "unit":"Licenses"
        },
        "unitType":"Licenses",
        "links":{
            "learnMore":{
                "uri":"http://g.microsoftonline.com/0BXPS00en/0000",
                "method":"GET",
                "headers":[]
            },
            "self":{
                "uri":"/offers/E60E0348-1710-484B-992A-32B294D4CDE1",
                "method":"GET",
                "headers":[]
            }
        },
        "attributes":{
            "objectType":"Offer"
        }
    },
    "links":{
        "self":{
            "uri":"/v1/offers?country={country_id}",
            "method":"GET",
            "headers":[]
        },
        "previous":{
            "uri":"/v1/offers?country={country_id}",
            "method":"GET",
            "headers":[]
        }
    },
    "attributes":{
        "objectType":"Collection"
    }
}
```

 

 




