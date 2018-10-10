---
title: Get a customer's qualification
description: How to get a customer's qualification.
ms.assetid: 1C9E986B-2887-460B-9D71-4520BB18C32A
ms.date: 09/12/2018
ms.localizationpriority: medium
---


# Get a customer's qualification

**Applies To**

-   Partner Center
-   Partner Center operated by 21Vianet
-   Partner Center for Microsoft Cloud Germany
-   Partner Center for Microsoft Cloud for US Government

How to get a customer's qualification.  


## <span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>Prerequisites

-   Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.
-   A customer identifier.


## <span id="C_"></span><span id="c_"></span>C#

To get a customer's qualification, first use the [**IAggregatePartner.Customers.ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier to identify the customer. Then use the [**Qualification**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) property to retrieve an interface to validation operations. Finally, call the [**Get**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) or [**GetAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) methods to retrieve the customer's qualification.

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;

var customerQualification = partnerOperations.Customers.ById(customerId).Qualification.Get();
```


## <span id="Request"></span><span id="request"></span><span id="REQUEST"></span>Request

**Request syntax**

| Method  | Request URI                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/qualification HTTP/1.1 |

 
**URI parameter**

This table lists the required query parameter to get all the qualification.

| Name               | Type   | Required | Description                                           |
|--------------------|--------|----------|-------------------------------------------------------|
| customer-tenant-id | string | Yes      | A GUID-formatted string that identifies the customer. |

**Request headers**

-   See [Partner Center REST headers](headers.md) for more information.

**Request body**

None.

**Request example**

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualification HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 
MS-CorrelationId: 
Connection: Keep-Alive
```


## <span id="Response"></span><span id="response"></span><span id="RESPONSE"></span>Response

If successful, this method returns a collection of [Qualification](qualification.md) resources in the response body.  Below is an example of the GET call on a customer with the Education qualification.

**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center REST error codes](error-codes.md).

**Response example**

```http
HTTP/1.1 200 OK
Content-Length: 
Content-Type: application/json
MS-CorrelationId: 
MS-RequestId: 
Date: Wed, 19 Aug 2018 05:43:06 GMT

{
    "education"
}
```
