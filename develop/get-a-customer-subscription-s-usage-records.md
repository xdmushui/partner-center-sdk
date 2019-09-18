---
title: Get all subscription usage records for a customer
description: How to get susbcription usage records for a customer of a specific Azure service or resource during the current billing period.
ms.assetid: 58FA3CBD-27CF-46C5-9EB2-188D83896F7D
ms.date: 09/17/2019
ms.localizationpriority: medium
---

# Get susbcription usage records for a customer

Applies to:

- Partner Center
- Partner Center for Microsoft Cloud Germany
- Partner Center for Microsoft Cloud for US Government

This topic describes how to get the colletion of **SubscriptionMonthlyUsageRecord** resource. This resource represents the customer's usage of a specific Azure service or resource during the current billing period.

## Prerequisites

- Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with App+User credentials only.
- A customer ID (**customer-tenant-id**). If you do not have a customer's ID, you can look up the ID in Partner Center by choosing the customer from the customers list, selecting Account, then saving their Microsoft ID.

## C\#

To get susbcription usage records for a customer of a specific Azure service or resource during the current billing period.:

1. Use your **IAggregatePartner.Customers** collection to call the **ById()** method.
2. Then call the **Subscriptions** property, as well as **UsageRecords** property. Finish by calling the Get() or GetAsync() methods.

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;

    var usageRecords = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.UsageRecords.Get();
    ```

For an example, see the following:

- Sample: [Console test app](console-test-app.md)
- Project: **PartnerSDK.FeatureSamples**
- Class: **GetSubscriptionUsageRecords.cs**

## REST request

### Request syntax

| Method  | Request URI                                                                                                      |
|---------|------------------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/usagerecords HTTP/1.1 |

#### URI parameter

This table lists the required query parameter to get the customer's rated usage information.

| Name                   | Type     | Required | Description                           |
|------------------------|----------|----------|---------------------------------------|
| **customer-tenant-id** | **guid** | Y        | A GUID corresponding to the customer. |

### Request headers

See [Headers](headers.md) for more information.

### Request body

None.

### Request example

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/usagerecords HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## REST response

If successful, this method returns a **SubscriptionMonthlyUsageRecord** resource in the response body.

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
    "totalCount": 1,
    "items": [
        {
            "status": "active",
            "partnerOnRecord": "6048879",
            "offerId": "DZH318Z0BPS6:0001:DZH318Z0BML6",
            "resourceId": "5a2a03c7-846e-ba03-c946-dee8841e2b94",
            "id": "5a2a03c7-846e-ba03-c946-dee8841e2b94",
            "resourceName": "Azure plan",
            "name": "Azure plan",
            "totalCost": 82.3616054989566696032,
            "currencyCode": "GBP",
            "usdTotalCost": 100.6499999999999985997,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "SubscriptionMonthlyUsageRecord"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/431f479f-9cb2-4486-a3ad-b47f844c1dd2/subscriptions/usagerecords",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
