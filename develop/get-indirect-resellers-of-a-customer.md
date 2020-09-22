---
title: Get indirect resellers of a customer
description: How to get a list of the indirect resellers that have a relationship with a specified customer.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice:  partnercenter-sdk
author: dineshvu
ms.author: dineshvu
---

# Get indirect resellers of a customer

**Applies To**

- Partner Center

How to get a list of the indirect resellers that have a relationship with a specified customer.

## Prerequisites

- Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with App+User credentials only.

- A customer ID (`customer-tenant-id`). If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard). Select **CSP** from the Partner Center menu, followed by **Customers**. Select the customer from the customer list, then select **Account**. On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section. The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).

## C\#

To retrieve a list of indirect resellers with whom the specified customer has a relationship, first get an interface to customer collection operations for the specific customer from the [**partnerOperations.Customers**/dotnet/api/microsoft.store.partnercenter.ipartner.relationships) property by providing the customer ID to identify the customer. Then call the [**Relationships.Get**/dotnet/api/microsoft.store.partnercenter.relationships.icustomerrelationshipcollection.get) or [**Get\_Async**/dotnet/api/microsoft.store.partnercenter.relationships.icustomerrelationshipcollection.getasync) method to get the list of indirect resellers.

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;

 var indirectResellers = partnerOperations.Customers[customerId].Relationships.Get();
```

**Sample**: [Console test app](console-test-app.md)**Project**: Partner Center SDK Samples **Class**: GetIndirectResellersOfCustomer.cs

## REST request

### Request syntax

| Method  | Request URI                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/relationships HTTP/1.1 |

### URI parameter

Use the following path parameter to identify the customer.

| Name        | Type   | Required | Description                                           |
|-------------|--------|----------|-------------------------------------------------------|
| customer-id | string | Yes      | A GUID formatted string that identifies the customer. |

### Request headers

For more information, see [Partner Center REST headers](headers.md).

### Request body

None.

### Request example

```http
GET https://api.partnercenter.microsoft.com/v1/customers/c501c3c4-d776-40ef-9ecf-9cefb59442c1/relationships HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: c9251710-5a30-4cd3-891a-c42d550af9a8
MS-CorrelationId: a96f326c-a392-44f4-bcfe-43152a756ba8
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## REST response

If successful, the response body contains a collection of [PartnerRelationship](relationships-resources.md) resources to identify the resellers.

### Response success and error codes

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center error codes](error-codes.md).

### Response example

```http
HTTP/1.1 200 OK
Content-Length: 264
Content-Type: application/json; charset=utf-8
MS-CorrelationId: a96f326c-a392-44f4-bcfe-43152a756ba8
MS-RequestId: c9251710-5a30-4cd3-891a-c42d550af9a8
MS-CV: plJP3ufU0UqXMeuh.0
MS-ServerId: 020021921
Date: Fri, 07 Apr 2017 23:42:11 GMT

{
    "totalCount": 1,
    "items": [{
            "id": "484e548c-f5f3-4528-93a9-c16c6373cb59",
            "name": "First Up Consultants",
            "relationshipType": "is_indirect_cloud_solution_provider_of",
            "mpnId": "4847383",
            "attributes": {
                "objectType": "PartnerRelationship"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
