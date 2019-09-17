---
title: Get resource usage records for a subscription of a customer
description: How to get resource usage records of a customer for specific Azure service or resource during the current billing period.
ms.assetid: 58FA3CBD-27CF-46C5-9EB2-188D83896F7D
ms.date: 09/17/2019
ms.localizationpriority: medium
---

# Get resource usage records for a subscription of a customer

Applies to:

- Partner Center
- Partner Center for Microsoft Cloud Germany
- Partner Center for Microsoft Cloud for US Government

This topic describes how to get the **ResourceUsageRecord** resource. This resource represents the customer's usage of a specific Azure service or resource during the current billing period.

## Prerequisites

- Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with App+User credentials only.
- A customer ID (**customer-tenant-id**). If you do not have a customer's ID, you can look up the ID in Partner Center by choosing the customer from the customers list, selecting Account, then saving their Microsoft ID.
- A subscription ID

## C\#

To get a usage summary for all of a customer's subscriptions:

1. Use your **IAggregatePartner.Customers** collection to call the **ById()** method.
2. Then call the Subscriptions property, as well as **UsageRecords**, then the **Resources** property. Finish by calling the Get() or GetAsync() methods.

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;
	// var selectedSubscriptionId as string;

    var usageRecords = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).UsageRecords.Resources.Get();
    ```

For an example, see the following:

- Sample: [Console test app](console-test-app.md)
- Project: **PartnerSDK.FeatureSamples**
- Class: **GetSubscriptionUsageRecordsByResource.cs**

## REST request

### Request syntax

| Method  | Request URI                                                                                         |
|---------|-----------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/subscriptions/{subscription-id}/resourceusagerecords HTTP/1.1 |

#### URI parameter

This table lists the required query parameter to get the customer's rated usage information.

| Name                   | Type     | Required | Description                           |
|------------------------|----------|----------|---------------------------------------|
| **customer-tenant-id** | **guid** | Y        | A GUID corresponding to the customer. |
| **subscription-id**    | **guid** | Y        | A GUID corresponding to the subscription or azure plan. |

### Request headers

See [Headers](headers.md) for more information.

### Request body

None.

### Request example

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/resourceusagerecords HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## REST response

If successful, this method returns a **PagedResourceCollection<ResourceUsageRecord>** resource in the response body.

### Response success and error codes

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, the error type, and additional parameters. For a full list, see [Error Codes](error-codes.md).

### Response example

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "totalCount": 3,
    "items": [
        {
            "subscriptionId": "5a2a03c7-846e-ba03-c946-dee8841e2b94",
            "resourceUri": "/subscriptions/fa334fc9-1c6f-45d1-839f-a006b9cbeaab/resourceGroups/TESTRG1/providers/Microsoft.Compute/disks/testVM1_OsDisk_1_531d3c99534b4649ae025d485370143e",
            "resourceType": "Microsoft.Compute",
            "entitlementId": "fa334fc9-1c6f-45d1-839f-a006b9cbeaab",
            "entitlementName": "Partner Subscription",
            "resourceGroupName": "TESTRG1",
            "name": "testVM1_OsDisk_1_531d3c99534b4649ae025d485370143e",
            "resourceName": "testVM1_OsDisk_1_531d3c99534b4649ae025d485370143e",
            "totalCost": 2.0211938955034572,
            "currencyCode": "GBP",
            "usdTotalCost": 2.4700000000000001,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "ResourceUsageRecord"
            }
        },
        {
            "subscriptionId": "5a2a03c7-846e-ba03-c946-dee8841e2b94",
            "resourceUri": "/subscriptions/fa334fc9-1c6f-45d1-839f-a006b9cbeaab/resourceGroups/TESTRG1/providers/Microsoft.Compute/virtualMachines/testVM1",
            "resourceType": "Microsoft.Compute",
            "entitlementId": "fa334fc9-1c6f-45d1-839f-a006b9cbeaab",
            "entitlementName": "Partner Subscription",
            "resourceGroupName": "TESTRG1",
            "name": "testVM1",
            "resourceName": "testVM1",
            "totalCost": 80.3322286322163563,
            "currencyCode": "GBP",
            "usdTotalCost": 98.1699999999999985,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "ResourceUsageRecord"
            }
        },
        {
            "subscriptionId": "5a2a03c7-846e-ba03-c946-dee8841e2b94",
            "resourceUri": "/subscriptions/fa334fc9-1c6f-45d1-839f-a006b9cbeaab/resourceGroups/testrg1/providers/Microsoft.Storage/storageAccounts/testrg1diag153",
            "resourceType": "Microsoft.Storage",
            "entitlementId": "fa334fc9-1c6f-45d1-839f-a006b9cbeaab",
            "entitlementName": "Partner Subscription",
            "resourceGroupName": "testrg1",
            "name": "testrg1diag153",
            "resourceName": "testrg1diag153",
            "totalCost": 0.0081829712368561032,
            "currencyCode": "GBP",
            "usdTotalCost": 0.0099999999999999997,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "ResourceUsageRecord"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/431f479f-9cb2-4486-a3ad-b47f844c1dd2/subscriptions/5a2a03c7-846e-ba03-c946-dee8841e2b94/resourceusagerecords",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
