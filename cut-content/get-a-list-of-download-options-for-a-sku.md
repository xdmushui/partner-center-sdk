---
title: Get a list of download options for a SKU
description: Gets a collection of download options for the specified product and SKU.
ms.assetid: 5E4160AB-6B73-4CA1-903D-7257927CA754
ms.author: v-thpr
ms.date: 06/07/2018
ms.topic: article
ms.prod: partner-center
ms.technology: partner-center-sdk
---

# Get a list of download options for a SKU

>[!IMPORTANT]   
>This information relates to pre-released product which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.  

**Applies To**

-   Partner Center

Gets a collection of download options for the specified product and SKU.

## <span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>Prerequisites


-   Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.
-   A product ID.
-   A SKU ID.

## <span id="C_"></span><span id="c_"></span>C#


To get a list of download options for a [SKU](products.md#sku), start by using the steps in [Get a SKU by ID](get-a-sku-by-id.md) to get the interface for a specific SKU's operations. From the resulting interface, select the **DownloadOptions** property to obtain an interface with the operations for download options. Finally, call **Get()** or **GetAsync()** to retrieve a collection of the download options for this SKU.  

```CSharp
IAggregatePartner partnerOperations;
string countryCode;
string productId; 
string skuId;

// Get the DownloadOptions.
var downloadOptions = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.ById(skuId).DownloadOptions.Get();
```

## <span id="REST_Request"></span><span id="rest_request"></span><span id="REST_REQUEST"></span>REST Request


**Request syntax**

| Method  | Request URI                                                                                                                                    |
|---------|----------------------------------------------------------------------------------------------------------------------------------------------- |
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/products/{product-id}/skus/{sku-id}/downloadoptions?country={country-code} HTTP/1.1              |

 

**URI parameters**

Use the following path and query parameters to get a list of download options for a SKU.

| Name                   | Type     | Required | Description                                                             |
|------------------------|----------|----------|-------------------------------------------------------------------------|
| product-id             | string   | Yes      | A string that identifies the product.                                   |
| sku-id                 | string   | Yes      | A string that identifies the SKU.                                       |
| country-code           | string   | Yes      | A country/region ID.                                                    |   



**Request headers**

-   See [Headers](headers.md) for more information.

**Request body**

None.

**Request example**

```
GET https://api.partnercenter.microsoft.com/v1/products/DG7GMGF0DWTL/skus/0001/downloadoptions?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 70324727-62d8-4195-8f99-70ea25058d02
MS-CorrelationId: 83b644b5-e54a-4bdc-b354-f96c525b3c58
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Host: api.partnercenter.microsoft.com
```

## <span id="Response"></span><span id="response"></span><span id="RESPONSE"></span>Response


If successful, the response body contains a collection of [SKU](products.md#sku) download options.

**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center error codes](error-codes.md).


**Response example**

```
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 83b644b5-e54a-4bdc-b354-f96c525b3c58
MS-RequestId: 70324727-62d8-4195-8f99-70ea25058d02
X-Locale: en-US,en-US
Date: Thu, 07 Jun 2018 07:11:57 GMT
Content-Length: 76697


{
  "totalCount": 156,
  "items": [
    {
      "optionKey": "AHYNSDUIJMIgQml0LCBJU08=",
      "optionTitle": "Access 2016",
      "displayRank": 0,
      "cpUandFileType": "32 Bit, ISO",
      "languageCode": "ar-SA",
      "languageName": "Arabic (Saudi Arabia)",
      "fileSize": 465702912,
      "downloadLink": {
        "uri": "/products/DG7GMGF0DWTL/skus/0001/downloadoptions/AHYNSDUIJMIgQml0LCBJU08=/downloadlink?country=US",
        "method": "GET",
        "headers": []
      }
    },
    {
      "optionKey": "NRTSJILOXNQgQml0LCBJU08=",
      "optionTitle": "Access 2016",
      "displayRank": 0,
      "cpUandFileType": "64 Bit, ISO",
      "languageCode": "pt-BR",
      "languageName": "Portuguese (Brazil)",
      "fileSize": 552275968,
      "downloadLink": {
        "uri": "/products/DG7GMGF0DWTL/skus/0001/downloadoptions/NRTSJILOXNQgQml0LCBJU08=/downloadlink?country=US",
        "method": "GET",
        "headers": []
      }
    },
….,
….,
  ],
  "links": {
    "self": {
      "uri": "/products/DG7GMGF0DWTL/skus/0001/downloadoptions?country=US",
      "method": "GET",
      "headers": []
    }
  },
  "attributes": {
    "objectType": "Collection"
  }
}
```   


## <span id="AdditionalExample"></span><span id="additionalexample"></span>Additional Example   


**C# example**

To retrieve the actual productsku download link for a specific language and filetype, invoke the URI exposed under downloadLink.

```CSharp
ResourceCollection<SkuDownloadOptions> skuDownloadOptions = partnerOperations.Products.ByCountry(country).ById(productId).Skus.ById(skuId).DownloadOptions.Get();
var productSkuDownloadLink = skuDownloadOptions.Items.First().DownloadLink.InvokeAsync<Link>(partnerOperations).Result;
```   

**Request example**

```
GET https://api.partnercenter.microsoft.com/v1/products/DG7GMGF0DWTL/skus/0001/downloadoptions/AHYNSDUIJMIgQml0LCBJU08=/downloadlink?country=US HTTP/1.1
Authorization: Bearer <Token>
Accept: application/json
MS-RequestId: cdc428d2-035b-41c4-9a32-e643c4471cbd
MS-CorrelationId: 799eee8d-07d1-452a-a035-388259df137c
```

**Response example**

```
HTTP/1.1 200 OK
Content-Length: 219
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 799eee8d-07d1-452a-a035-388259df137c
MS-RequestId: cdc428d2-035b-41c4-9a32-e643c4471cbd
X-Locale: en-US
Date: Mon, 19 Mar 2018 07:45:14 GMT

{
  "uri": "https://download.mp.microsoft.com/pr/Access_2016_Arabic_32_X21-12345.ISO?t=e4uk89s4-e49e-41a9-a0a4-70dcec1f5e80&d=50&e=5635566218&h=12bf676fc611435eb310540123c115bd",
  "method": "GET",
  "headers": []
}
```   


 

 




