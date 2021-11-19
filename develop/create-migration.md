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
| termDuration          | string           | No              | Term duration can be specified to be changed upon migration.                                              |
| billingCycle          | string           | No              | Billing cycle can be specified to be changed upon migration.                                              |
| purchaseFullTerm      | bool             | No              | A new term can be started in NCE upon migration.                                                          |
| quantity              | int              | No              | License quantity for a subscription can be increased or decreased upon migration.                         |

### Request example

```http
{
    "currentSubscriptionId" : "9beb6319-6889-4d28-a155-68ca9c783842"
}
```

```http
{ 
    "currentSubscriptionId": "5C77DC7F-BE2C-4306-A3B5-0EBB4365D7FC", 
    "termDuration": "P1M", 
    "billingCycle": "Monthly", 
} 
```

```http
{
    "currentSubscriptionId": "5C77DC7F-BE2C-4306-A3B5-0EBB4365D7FC", 
    "purchaseFullTerm": true 
}
```

## REST response

If successful, this method returns a collection of [Subscription](subscription-resources.md) resources in the response body.

### Response success and error codes

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center REST error codes](error-codes.md).

### Response examples

```http
{
    "id": "f46fbd87-b204-40e5-b891-d0879ca3bf62",
    "startedTime": "2021-10-13T16:30:32.1446219Z",
    "completedTime": "2021-10-13T16:35:40.3844713Z",
    "currentSubscriptionId": "5C77DC7F-BE2C-4306-A3B5-0EBB4365D7FC",
    "status": "Completed",
    "customerTenantId": "75c5e79e-7e9f-429f-b772-ed3d38768f7c",
    "catalogItemId": "CFQ7TTC0LF8Q:0001:CFQ7TTC0KJ4N",
    "newCommerceSubscriptionId": "8adde5ce-52e3-47b5-c49c-df9c210bd5df",
    "newCommerceOrderId": "8672a13e9197",
    "subscriptionEndDate": "2022-10-13T00:00:00Z",
    "quantity": 1,
    "termDuration": "P1Y",
    "billingCycle": "Monthly",
    "purchaseFullTerm": false
}
```
