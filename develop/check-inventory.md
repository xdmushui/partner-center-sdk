---
title: Check inventory
description: Check the inventory for a specific set of catalog items.
ms.assetid: 5E4160AB-6B73-4CA1-903D-7257927CA754
ms.author: v-thpr
ms.date: 03/20/2018
ms.topic: article
ms.prod: partner-center
ms.technology: partner-center-sdk
---

# Check inventory

[This information relates to pre-released product which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.] 

**Applies To**

-   Partner Center

How to check the inventory for a specific set of catalog items.

## <span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>Prerequisites


-   Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.
-   One or more product IDs. Optionally, SKU IDs can also be specified.
-   Any additional context needed for verifying the inventory of the SKU(s) referenced by the provided product/SKU id(s). These requirements may vary by type of product/SKU,  and can be determined from the SKU’s InventoryVariables property. 

## <span id="C_"></span><span id="c_"></span>C#


To check the inventory, build an [InventoryCheckRequest](products.md#inventorycheckrequest) object using an [InventoryItem](products.md#inventoryitem) object for each item to be checked. Then, use an **IAggregatePartner.Extensions** accessor, scope it down to **Product** and then select the country using the **ByCountry()** method. Finally, call the **CheckInventory()** function with your **InventoryCheckRequest** object.

```CSharp
IAggregatePartner partnerOperations;
string customerId;
string subscriptionId;
string countryCode;
string productId;

// Populate the customerId, subscriptionId, countryCode, and productId variables.
…

// Build the inventory check request details object.
var inventoryCheckRequest = new InventoryCheckRequest()
{
	TargetItems = new InventoryItem[]{ new InventoryItem { ProductId = productId } },
	InventoryContext = new Dictionary<string, string>()
	{
		{ “customerId”, customerId },
		{“azureSubscriptionId”, subscriptionId }
	}
};

// Get the inventory results.
var inventoryResults = partnerOperations.Extensions.Product.ByCountry(countryCode).CheckInventory(inventoryCheckRequest);
```

## <span id="REST_Request"></span><span id="rest_request"></span><span id="REST_REQUEST"></span>REST Request


**Request syntax**

| Method   | Request URI                                                                                                                              |
|----------|------------------------------------------------------------------------------------------------------------------------------------------|
| **POST** | [*{baseURL}*](partner-center-rest-urls.md)/v1/extensions/product/checkInventory?country={country-code} HTTP/1.1                        |

 

**URI parameter**

Use the following query parameter to check the inventory.

| Name                   | Type     | Required | Description                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| country-code           | string   | Yes      | A country/region ID.                                            |

 

**Request headers**

-   See [Headers](headers.md) for more information.

**Request body**

The inventory request details, consisting of an [InventoryCheckRequest](products.md#inventorycheckrequest) resource containing one or more [InventoryItem](products.md#inventoryitem) resources. 

**Request example**

```
POST https://api.partnercenter.microsoft-ppe.com/v1/extensions/product/checkinventory?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: d1b1981a-e088-4610-870a-eebec96d6bcd
MS-CorrelationId: 4acb26a1-3536-4081-bc7d-092869a4961a
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Content-Type: application/json

{"TargetItems":[{"ProductId":"DZH318Z0BQ3P"}],"InventoryContext":{"customerId":"d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d","subscriptionId":"3A231FBE-37FE-4410-93FD-730D3D5D4C75"}}
```

## <span id="Response"></span><span id="response"></span><span id="RESPONSE"></span>Response


If successful, the response body contains a collection of InventoryItem](products.md#inventoryitem) objects populated with the restriction details, if any apply.

**Note** If an input InventoryItem represents an item that could not be found in the catalog, it will not be included in the output collection.


**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center error codes](error-codes.md).

This method returns the following error codes:

| HTTP Status Code     | Error code   | Description                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| 400                  | 2001         | The request body is missing.                                                                              |
| 400                  | 400026       | A required inventory context item is missing.                                                             |


**Response example**

```
HTTP/1.1 200 OK
Content-Length: 1021
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 4acb26a1-3536-4081-bc7d-092869a4961a
MS-RequestId: d1b1981a-e088-4610-870a-eebec96d6bcd
X-Locale: en-US
[
    {
        "productId": "DZH318Z0BQ3P",
        "skuId": "0039",
        "isRestricted": true,
        "restrictions": [
            {
                "reasonCode": "NotAvailableForSubscription",
                "description": "Restriction identified of type 'Location' with values 'japanwest'.",
                "properties": {
                    "type": "Location",
                    "values": "japanwest"
                }
            }
        ]
    },
    {
        "productId": "DZH318Z0BQ3P",
        "skuId": "0038",
        "isRestricted": true,
        "restrictions": [
            {
                "reasonCode": "NotAvailableForSubscription",
                "description": "Restriction identified of type 'Location' with values 'japanwest'.",
                "properties": {
                    "type": "Location",
                    "values": "japanwest"
                }
            }
        ]
    },
    {
        "productId": "DZH318Z0BQ3P",
        "skuId": "000S",
        "isRestricted": false,
        "restrictions": []
    },
    {
        "productId": "DZH318Z0BQ3P",
        "skuId": "0011",
        "isRestricted": false,
        "restrictions": []
    }
]
```

 

 




