---
title: Get a list of Azure entitlements for a subscription
description: You can use the AzureEntitlement resource to  get a collection of Azure entitlement resources that belong to a subscription.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice:  partnercenter-sdk
ms.localizationpriority: medium
---

# Get a list of Azure entitlements for a subscription

**Applies to:**

- Partner Center

You can use the [Azure entitlement resource](subscription-resources.md#azureentitlement) (**AzureEntitlement**) to get a collection of resources that belong to a subscription.

## Prerequisites

- Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.
- A customer identifier (**customer-tenant-id**). If you don't have a customer's identifier, you can look it up in Partner Center by choosing the customer from the customers list, selecting **Account**, then saving their **Microsoft ID**.
- A subscription identifier.

## REST request

### Request syntax

| Method  | Request URI                                                                                                                   |
|---------|---------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/azureentitlements HTTP/1.1 |

#### URI parameters

The following table lists the required query parameters to get all the Azure entitlements for a subscription.

| Name                   | Type     | Required | Description                           |
|------------------------|----------|----------|---------------------------------------|
| **customer-tenant-id** | **guid** | Y        | A GUID corresponding to the customer. |
| **subscription-id**       | **guid** | Y        | A GUID corresponding to the subscription.    |

### Request headers

For more information, see [Partner Center REST headers](headers.md).

### Request body

None.

### Request example

```http
GET https://api.partnercenter.microsoft.com/v1/customers/11f9bc2a-1f38-431c-a0b0-9455c6f5bbc0/subscriptions/3f15978e-005c-b763-bb78-2a8fab289c58/azureEntitlements HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 16fee928-dc2c-412f-adbb-871f68babf16
MS-CorrelationId: c49004b1-224f-4d86-a607-6c8bcc52cfdd
Connection: Keep-Alive
```

## REST response

If successful, this method returns a collection of [**AzureEntitlement**](subscription-resources.md#azureentitlement) resources in the response body.

### Response success and error codes

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Error Codes](error-codes.md).

### Response example

```http
HTTP/1.1 200 OK
Content-Length: 73754
Content-Type: application/json
MS-CorrelationId: c49004b1-224f-4d86-a607-6c8bcc52cfdd
MS-RequestId: 16fee928-dc2c-412f-adbb-871f68babf16
Date: Wed, 04 Oct 2019 05:50:45 GMT

{
"totalCount":1,
"items":[
  {
    "id":"899ae6f1-8a74-4d5e-b6c6-e6b5019bbff8",
    "friendlyName":"Microsoft Azure",
    "status":"active",
    "subscriptionId":"3f15978e-005c-b763-bb78-2a8fab289c58"
   }],
    "attributes":{"objectType":"Collection"}
  }
