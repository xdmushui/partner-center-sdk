---
title: Get meter usage records for a subscription of a customer
description: How to get meter usage records of a customer for specific Azure service or resource during the current billing period.
ms.assetid: 58FA3CBD-27CF-46C5-9EB2-188D83896F7D
ms.date: 09/17/2019
ms.localizationpriority: medium
---

# Get meter usage records for a subscription of a customer

Applies to:

- Partner Center
- Partner Center for Microsoft Cloud Germany
- Partner Center for Microsoft Cloud for US Government

This topic describes how to get the collection of **MeterUsageRecord** resource. This resource represents an aggregated total per meter for the current billing cycle, across your entire Azure plan.

## Prerequisites

- Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with App+User credentials only.
- A customer ID (**customer-tenant-id**). If you do not have a customer's ID, you can look up the ID in Partner Center by choosing the customer from the customers list, selecting Account, then saving their Microsoft ID.
- A subscription ID

>[!NOTE]
>This is equivalent to “subscriptions/{subscription-id}/usagerecords/resources” (which will continue to function for 145P only). 
>This new route will support both 145P and Azure Plan. In order to get this information for Azuer plan, you will need to switch to this new route. Other than the mentioned properties, the response is the same as the old route.

## C\#

To get meter usage records of a customer for specific Azure service or resource during the current billing period:

1. Use your **IAggregatePartner.Customers** collection to call the **ById()** method.
2. Then call the Subscriptions property, as well as **UsageRecords**, then the **Meters** property. Finish by calling the Get() or GetAsync() methods.

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;
	// var selectedSubscriptionId as string;

    var usageRecords = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).UsageRecords.Meters.Get();
    ```

For an example, see the following:

- Sample: [Console test app](console-test-app.md)
- Project: **PartnerSDK.FeatureSamples**
- Class: **GetSubscriptionUsageRecordsByMeter.cs**

## REST request

### Request syntax

| Method  | Request URI                                                                                                                             |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/meterusagerecords HTTP/1.1 |

#### URI parameter

This table lists the required query parameter to get the customer's rated usage information.

| Name                   | Type     | Required | Description                               |
|------------------------|----------|----------|-------------------------------------------|
| **customer-tenant-id** | **guid** | Y        | A GUID corresponding to the customer.     |
| **subscription-id**    | **guid** | Y        | A GUID corresponding to the subscription. |

>[!NOTE]
>For Azure plan, provide the **plan-id** as the **subscription-id** in this route.

### Request headers

See [Headers](headers.md) for more information.

### Request body

None.

### Request example

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/meterusagerecords HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## REST response

If successful, this method returns a **PagedResourceCollection<MeterUsageRecord>** resource in the response body.

### Response success and error codes

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, the error type, and additional parameters. For a full list, see [Error Codes](error-codes.md).

### Response example 1 - Customer purchased 145P Azure PayG

>[!NOTE]
>For customers with 145P, there will be no change to API response.

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
            "offerId": "MS-AZR-0145P",
            "resourceId": "ECF71641-F347-41B6-B02C-187B1B778A43",
            "id": "ECF71641-F347-41B6-B02C-187B1B778A43",
            "resourceName": "Microsoft Azure",
            "name": "Microsoft Azure",
            "totalCost": 22.861172,
            "currencyLocale": "fr-FR",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-01T23:04:41.193+00:00",
            "attributes": {
                "objectType": "SubscriptionMonthlyUsageRecord"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/aa2c5268-e55d-4b92-8822-652b5795a1ed/subscriptions/usagerecords/",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}


### Response example 2 - Customer purchased Azure Plan

>[!NOTE]
>For customers with Azure Plan, there are few changes in API response. 
>"currencyLocale" is replaced with 'currencyCode'.
>"usdTotalCost" is new field.

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Fri, 26 Feb 2016 20:31:45 GMT

{
    "totalCount": 4,
    "items": [
        {
            "subscriptionId": "5a2a03c7-846e-ba03-c946-dee8841e2b94",
            "meterId": "DZH318Z0BNVX-005J-Data Transfer In (GB)",
            "meterName": "Data Transfer In",
            "category": "Bandwidth",
            "subcategory": "Bandwidth",
            "quantityUsed": 0.01129,
            "unit": "1 GB",
            "totalCost": 0,
            "currencyCode": "GBP",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "MeterUsageRecord"
            }
        },
        {
            "subscriptionId": "5a2a03c7-846e-ba03-c946-dee8841e2b94",
            "meterId": "DZH318Z0BNVX-005J-Data Transfer Out (GB)",
            "meterName": "Data Transfer Out",
            "category": "Bandwidth",
            "subcategory": "Bandwidth",
            "quantityUsed": 0.000224,
            "unit": "1 GB",
            "totalCost": 0,
            "currencyCode": "GBP",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "MeterUsageRecord"
            }
        },
        {
            "subscriptionId": "5a2a03c7-846e-ba03-c946-dee8841e2b94",
            "meterId": "DZH318Z0BNZ5-006G-10K Batch Write Operations",
            "meterName": "Batch Write Operations",
            "category": "Storage",
            "subcategory": "Tables",
            "quantityUsed": 0.2462,
            "unit": "10K",
            "totalCost": 0,
            "currencyCode": "GBP",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "MeterUsageRecord"
            }
        },
        {
            "subscriptionId": "5a2a03c7-846e-ba03-c946-dee8841e2b94",
            "meterId": "DZH318Z0BNZ5-006G-Data Stored (GB/Month)",
            "meterName": "LRS Data Stored",
            "category": "Storage",
            "subcategory": "Tables",
            "quantityUsed": 0.002632,
            "unit": "1 GB/Month",
            "totalCost": 0,
            "currencyCode": "GBP",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "MeterUsageRecord"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/431f479f-9cb2-4486-a3ad-b47f844c1dd2/subscriptions/5a2a03c7-846e-ba03-c946-dee8841e2b94/meterusagerecords",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
