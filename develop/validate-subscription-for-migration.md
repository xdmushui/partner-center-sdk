---
title: Validate a subscription for migration
description: How to validate if a subscription is eligible for migration.
ms.date: 10/04/2021
ms.service: partner-dashboard
ms.subservice:  partnercenter-sdk
---

# Validate a subscription for migration

**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

How to validate a subscription for migration to New Commerce Experience

## Prerequisites

- Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.

- A customer ID (`customer-tenant-id`). If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard). Select **CSP** from the Partner Center menu, followed by **Customers**. Select the customer from the customer list, then select **Account**. On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section. The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).

- A current subscription ID

## REST request

### Request syntax

| Method  | Request URI                                                                                                            |
|---------|------------------------------------------------------------------------------------------------------------------------|
|**POST** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/migrations/newcommerce/validate HTTP/1.1  |

### URI parameter

This table lists the required query parameters to validate a subscription for migration.

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

If successful, this method returns an "isEligible" boolean in the response body, indicating if the current subscription is eligible for migration to new commerce.

### Response success and error codes

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center REST error codes](error-codes.md).

### Response examples

```http
1. 
    {
        "currentSubscriptionId": "9beb6319-6889-4d28-a155-68ca9c783842",
        "isEligible": false,
        "errors": [
            {
                "code": 5,
                "description": "Subscription cannot be migrated to New Commerce because the equivalent offer is not yet available in New Commerce",
            }
        ]
    }
```

```http
2. 
    {
        "currentSubscriptionId": "9beb6319-6889-4d28-a155-68ca9c783842",
        "isEligible": true,
        "catalogItemId": "CFQ7TTC0LF8S:0002:CFQ7TTC0KSVV",
    }
```
