---
title: Get a list of products (by customer)
description: You can use a customer identifier to get a collection of products by customer.
ms.assetid:
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice:  partnercenter-sdk
ms.localizationpriority: medium
---

# Get a list of products (by customer)

Applies to:

- Partner Center
- Partner Center operated by 21Vianet
- Partner Center for Microsoft Cloud Germany
- Partner Center for Microsoft Cloud for US Government

You can use the following methods to get a collection of products for an existing customer.

## Prerequisites

- Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.
- A customer identifier (**customer-tenant-id**).

## REST

### Rest request

#### Request syntax

| Method | Request URI                                                                                                              |
|--------|--------------------------------------------------------------------------------------------------------------------------|
| POST   | [*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/products?targetView={targetView} HTTP/1.1 |

#### Request URI parameters

| Name               | Type | Required | Description                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| **customer-tenant-id** | GUID | Yes | The value is a GUID-formatted **customer-tenant-id**, which is an identifier that allows you to specify a customer. |
| **targetView** | string | Yes | Identifies the target view of the catalog. The supported values are: <ul><li>**Azure**, which includes all Azure items</li><li>**AzureReservations**, which includes all Azure reservation items</li><li>**AzureReservationsVM**, which includes all virtual machine (VM) reservation items</li><li>**AzureReservationsSQL**, which includes all SQL reservation items</li><li>**AzureReservationsCosmosDb**, which includes all Cosmos database reservation items</li><li>**MicrosoftAzure**, which includes items for Microsoft Azure subscriptions (**MS-AZR-0145P**) and Azure plans</li><li>**OnlineServices**, which  includes all online service items, including commercial marketplace products</li><li>**Software**, which  includes all software items</li><li>**SoftwareSUSELinux**, which includes all software SUSE Linux items</li><li>**SoftwarePerpetual**, which includes all perpetual software items</li><li>**SoftwareSubscriptions**, which includes all software subscription items </ul> |

#### Request header

For more information, see [Headers](headers.md).

#### Request body

None.

#### Request example

Request for a list of Azure usage-based products available to a given customer. Products for both Microsoft Azure (MS-AZR-0145P) and Azure plans will be returned for customers in public cloud:

```http
GET https://api.partnercenter.microsoft.com/v1/customers/65543400-f8b0-4783-8530-6d35ab8c6801/products?targetView=MicrosoftAzure HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 83643f5e-5dfd-4375-88ed-054412460dc8
MS-CorrelationId: b1939cb2-e83d-4fb0-989f-514fb741b734
```

### Rest response

#### Response success and error codes

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center error codes](error-codes.md).

This method returns the following error codes:

| HTTP Status Code | Error code   | Description                     |
|------------------|--------------|---------------------------------|
| 403 | 400036 | Access to the requested targetView is not allowed. | 

#### Response example

```http
HTTP/1.1 200 OK
Content-Length: 1909
Content-Type: application/json; charset=utf-8
MS-CorrelationId: cad955c2-8efc-47fe-b112-548ff002ba18
MS-RequestId: ae7288e2-2673-4ad4-8c12-7aad818d5949
 
{
    "totalCount": 2,
    "items": [
        {
            "id": "MS-AZR-0145P",
            "productId": "9DEA7946-EC2C-441E-9FFD-E3B275F7E838",
            "title": "Microsoft Azure",
            "description": "Azure Cloud Solution Provider offer for Partner and Resellers",
            "minimumQuantity": 1,
            "maximumQuantity": 1,
            "isTrial": false,
            "supportedBillingCycles": [
                "monthly"
            ],
            "purchasePrerequisites": [
                "MicrosoftCloudAgreement"
            ],
            "actions": [
                "Refund"
            ],
            "dynamicAttributes": {
                "isMicrosoftProduct": true,
                "billingType": "usage",
                "category": "Enterprise",
                "isAddon": false,
                "prerequisiteSkus": [],
                "rank": 1413,
                "hasAddOns": false,
                "isAutoRenewable": false,
                "upgradeTargetOffers": null,
                "conversionTargetOffers": [],
                "unitType": "Usage-based",
                "limitUnitOfMeasure": "None",
                "limit": 0,
                "reselleeQualifications": [],
                "resellerQualifications": []
            },
            "links": {
                "availabilities": {
                    "uri": "/products/9DEA7946-EC2C-441E-9FFD-E3B275F7E838/skus/MS-AZR-0145P/availabilities?country=US&targetSegment=Commercial",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/products/9DEA7946-EC2C-441E-9FFD-E3B275F7E838/skus/MS-AZR-0145P?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        },
        {
            "id": "0001",
            "productId": "DZH318Z0BPS6",
            "title": "Microsoft Azure plan",
            "description": "Microsoft Azure plan (MS-AZR-0017G)",
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
                    "uri": "/products/DZH318Z0BPS6/skus/0001/availabilities?country=US&targetSegment=Commercial",
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
    ],
    "links": {
        "self": {
            "uri": "/customers/e2a0c0f3-0f74-4d1c-808c-dfa511481913/products/all/skus?targetView=MicrosoftAzure&targetSegment=Commercial",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
