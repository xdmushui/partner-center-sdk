---
title: Create a new commerce migration
description: How to create a new commerce migration
ms.date: 10/04/2021
ms.service: partner-dashboard
ms.subservice:  partnercenter-sdk
---

#  Create a new commerce migration

**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

How to create a migration of a subscription to New Commerce Experience

## Prerequisites

- Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.

- A customer ID (`customer-tenant-id`). If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard). Select **CSP** from the Partner Center menu, followed by **Customers**. Select the customer from the customer list, then select **Account**. On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section. The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).

- A current subscription ID

## REST request

### Request syntax

| Method  | Request URI                                                                                                            |
|---------|------------------------------------------------------------------------------------------------------------------------|
|**POST** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/migrations/newcommerce HTTP/1.1           |

### URI parameter

This table lists the required query parameters to create a new commerce migration.

| Name               | Type   | Required | Description                                           |
|--------------------|--------|----------|-------------------------------------------------------|
| customer-tenant-id | string | Yes      | A GUID-formatted string that identifies the customer. |

### Request headers

For more information, see [Partner Center REST headers](headers.md).

### Request body

This table describes the [Subscription](subscription-resources.md) properties in the request body.

| Property              | Type             | Required        | Description |
|-----------------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| currentSubscriptionId | string           | Yes             | A subscription identifier that indicates which subscription requires validation for migration.            |

### Request example

```http
"currentSubscriptionId" : "9beb6319-6889-4d28-a155-68ca9c783842"
```

## REST response

If successful, this method returns a collection of [Subscription](subscription-resources.md) resources in the response body.

### Response success and error codes

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center REST error codes](error-codes.md).

### Response examples

```http
{
    "id": "d3a0ef43-a208-4c32-8b10-f15e99d4e782",
    "currentSubscriptionId": "9beb6319-6889-4d28-a155-68ca9c783842",
    "status": "Processing",
    "customerTenantId": "a836f6d8-1b17-44af-aaf1-1e5511c5d4e1",
    "partnerTenantId": "7828d7ba-f17b-45c3-a1ce-8b6c3e3a26c0",
    "catalogItemId": "CFQ7TTC0LF8S:0002:CFQ7TTC0KSVV",
    "subscriptionEndDate": "2022-09-06T00:00:00Z",
    "quantity": 1,
    "termDuration": "P1Y",
    "billingCycle": "Monthly"
}
```
