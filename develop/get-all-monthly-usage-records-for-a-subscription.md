---
title: Get all monthly usage records for a subscription.
description: You can use the AzureResourceMonthlyUsageRecord resource collection to get a list of services within a customer's subscription and their associated rated usage information.
ms.assetid: 037D71B9-8E8B-4BC0-8388-9CBC97218CED
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice:  partnercenter-sdk
ms.localizationpriority: medium
---

# Get all monthly usage records for a subscription.

**Applies to:**

- Partner Center
- Partner Center for Microsoft Cloud Germany
- Partner Center for Microsoft Cloud for US Government

You can use the [**AzureResourceMonthlyUsageRecord**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.usage.azureresourcemonthlyusagerecord) resource collection to get a list of services within a customer's subscription and their associated rated usage information.

## Prerequisites

- Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.
- A customer identifier (**customer-tenant-id**). If you don't have a customer's identifier, you can look up the identifier in Partner Center. Choose the customer from the list of customers, then select **Account**, then save their **Microsoft ID**.
- A subscription identifier.

*This API only supports Microsoft Azure (MS-AZR-0145P) subscriptions. If you are using an Azure plan, see [Get usage data for subscription by meter](get-a-customer-subscription-meter-usage-records.md) instead.*

## C\#

To get a subscription's resource usage information:

1. Use your **IAggregatePartner.Customers** collection to call the **ById()** method.
2. Call the **Subscriptions** property, as well as **UsageRecords**, then the **Resources** property.
3. Call the **Get()** or **GetAsync()** methods.

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;
// var selectedSubscriptionID as string;

var usageRecords = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).UsageRecords.Resources.Get();
```

For an example, see the following:

- Sample: [Console test app](console-test-app.md)
- Project: **PartnerSDK.FeatureSample**
- Class: **SubscriptionResourceUsageRecords.cs**

## REST

### REST request

#### Request syntax

| Method  | Request URI                                                                                                                                       |
|---------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/usagerecords/resources HTTP/1.1 |

##### URI parameters

This table lists the required query parameters to get the rated usage information.

| Name                    | Type     | Required | Description                               |
|-------------------------|----------|----------|-------------------------------------------|
| **customer-tenant-id**  | **guid** | Y        | A GUID corresponding to the customer.     |
| **subscription-id** | **guid** | Y        | A GUID corresponding to the subscription. |

#### Request headers

For more information, see [Partner Center REST headers](headers.md).

#### Request body

None.

#### Request example

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/usagerecords/resources HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 65b26053-37d0-4303-9fd1-46ad8012bcb6
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

### REST response

If successful, this method returns a collection of **AzureResourceMonthlyUsageRecord** resources in the response body.

#### Response success and error codes

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Error Codes](error-codes.md).

#### Response example

```http
HTTP/1.1 200 OK
Content-Length: 12014
Content-Type: application/json
MS-CorrelationId: 648a26a4-a63e-459f-844b-4f29d7913353
MS-RequestId: be82a8ba-4a53-49f7-8313-b033c058687e
Date: Tue, 10 Nov 2015 19:09:59 GMT

{
    "totalCount":20,
    "items":[{
        "category":"Storage",
        "subcategory":"LOCALLY REDUNDANT",
        "quantityUsed":0.151287527825352,
        "unit":"GB",
        "id":"2a2419c0-cefe-46b2-8004-8eb002ad606c",
        "name":"Azure Resource 1",
        "totalCost":0.195779159290613,
        "currencyLocale":"en-US",
        "attributes":{
            "objectType":"AzureResourceMonthlyUsageRecord"
        }
    },
    {
        "category":"Remote App",
        "subcategory":"Remote App",
        "quantityUsed":0.932546524299563,
        "unit":"GB",
        "id":"7e4099c8-2b3d-41a6-a1bd-d5cf315989b2",
        "name":"Azure Resource 2",
        "totalCost":0.920983775016379,
        "currencyLocale":"en-US",
        "attributes":{
            "objectType":"AzureResourceMonthlyUsageRecord"
        }
    }],
    "links":{
        "self":{
            "uri":"/v1/customers/<customer-tenant-id>/subscriptions/<id-for-subscription>%20/usagerecords",
            "method":"GET",
            "headers":[]
        }
    },
    "attributes":{
        "objectType":"Collection"
    }
}
```
