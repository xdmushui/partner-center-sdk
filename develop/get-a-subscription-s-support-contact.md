---
title: Get a subscription's support contact
description: How to get a subscription's support contact.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice:  partnercenter-sdk
---

# Get a subscription's support contact

**Applies To**

- Partner Center
- Partner Center for Microsoft Cloud Germany
- Partner Center for Microsoft Cloud for US Government

How to get a subscription's support contact.

## Prerequisites

- Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with App+User credentials only.

- A customer ID (`customer-tenant-id`). If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard). Select **CSP** from the Partner Center menu, followed by **Customers**. Select the customer from the customer list, then select **Account**. On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section. The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).

- A subscription identifier.

## C\#

To get a subscription's support contact, start by using the [**IAggregatePartner.Customers.ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer. Then, get an interface to subscription operations by calling the [**Subscriptions.ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the subscription ID. Next, use the [**SupportContact**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.supportcontact) property to obtain an interface to support contact operations, and then call the [**Get**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get) or [**GetAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync) method to retrieve the [**SupportContact**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.subscriptions.supportcontact) object.

``` csharp
// IAggregatePartner partnerOperations.
// string customerId;
// string subscriptionId;

// Retrieve subscription's support contact.
var supportContact = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId).SupportContact.Get();
```

**Sample**: [Console test app](console-test-app.md). **Project**: Partner Center SDK Samples **Class**: GetSubscriptionSupportContact.cs

## REST request

### Request syntax

| Method  | Request URI                                                                                                                    |
|---------|--------------------------------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/supportcontact HTTP/1.1 |

### URI parameter

Use the following path parameters to identify the customer and subscription.

| Name            | Type   | Required | Description                                                     |
|-----------------|--------|----------|-----------------------------------------------------------------|
| customer-id     | string | Yes      | A GUID formatted string that identifies the customer.           |
| subscription-id | string | Yes      | A GUID formatted string that identifies the trial subscription. |

### Request headers

For more information, see [Partner Center REST headers](headers.md).

### Request body

None.

### Request example

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/C8D8FBAB-6A62-44DC-BE50-B7C74E43A296/supportcontact HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: d052776c-e8fd-4803-b6a3-1659055ac3c4
MS-CorrelationId: a6c552a8-1922-4d0c-bb94-335a33334d14
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## REST response

If successful, the response body contains the [SupportContact](subscription-resources.md#supportcontact) resource.

### Response success and error codes

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center error codes](error-codes.md).

### Response example

```http
HTTP/1.1 200 OK
Content-Length: 328
Content-Type: application/json; charset=utf-8
MS-CorrelationId: a6c552a8-1922-4d0c-bb94-335a33334d14
MS-RequestId: d052776c-e8fd-4803-b6a3-1659055ac3c4
MS-CV: bLbUhqy0+ESOX1v4.0
MS-ServerId: 201022015
Date: Tue, 20 Jun 2017 19:30:19 GMT

﻿{
    "supportTenantId": "3B33E682-00C3-41EE-9DD2-A548ADF56438",
    "supportMpnId": "4391507",
    "name": "Trey Research",
    "links": {
        "self": {
            "uri": "/customers/0C39D6D5-C70D-4C55-BC02-F620844F3FD1/subscriptions/C8D8FBAB-6A62-44DC-BE50-B7C74E43A296/supportcontact",
            "method": "Get",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "SupportContact"
    }
}
```
