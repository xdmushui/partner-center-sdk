---
title: Retrieve a relationship request URL
description: How to retrieve a relationship request URL to send to a customer.
ms.assetid: 31D9EDB2-4ABE-4C57-A394-2FF256F7D3CA
ms.date: 12/15/2017
ms.localizationpriority: medium
---

# Retrieve a relationship request URL


**Applies To**

- Partner Center
- Partner Center operated by 21Vianet
- Partner Center for Microsoft Cloud Germany

How to retrieve a relationship request URL to send to a customer.

## <span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>Prerequisites


- Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with App+User credentials only.

## <span id="C_"/><span id="c_"/>C#


To retrieve a relationship request URL, first use [**IAggregatePartner.Customers**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.ipartner.customers) to get an interface to the partner's customer operations. Next, use the [**RelationshipRequest**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.relationshiprequest) property to get an interface to customer relationship request operations. Finally, call the [**Get**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.relationshiprequests.icustomerrelationshiprequest.get) or [**GetAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.relationshiprequests.icustomerrelationshiprequest.getasync) method to retrieve the URL.

``` csharp
// IAggregatePartner partnerOperations;

var customerRelationshipRequest = partnerOperations.Customers.RelationshipRequest.Get();
```

**Sample**: [Console test app](console-test-app.md). **Project**: Partner Center SDK Samples **Class**: GetCustomerRelationshipRequest.cs

## <span id="Request"/><span id="request"/><span id="REQUEST"/>Request


**Request syntax**

| Method  | Request URI                                                                            |
|---------|----------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/relationshiprequests HTTP/1.1 |

 

**Request headers**

- See [Partner Center REST headers](headers.md) for more information.

**Request body**

None

**Request example**

```http
GET https://api.partnercenter.microsoft.com/v1/customers/relationshiprequests HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ee519026-4c67-4113-bec7-a38aca621bf0
MS-CorrelationId: 02971f0f-1029-47b2-9fdb-1932f0987470
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <span id="Response"/><span id="response"/><span id="RESPONSE"/>Response


If successful, the response contains the [RelationshipRequest](relationships.md#relationshiprequest) object.

**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center REST error codes](error-codes.md).

**Response example**

```http
HTTP/1.1 200 OK
Content-Length: 196
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 02971f0f-1029-47b2-9fdb-1932f0987470
MS-RequestId: ee519026-4c67-4113-bec7-a38aca621bf0
MS-CV: jbYZRWjU3E262f8o.0
MS-ServerId: 030020643
Date: Fri, 19 May 2017 22:32:07 GMT
﻿
{
    "url": "https://portal.office.com/partner/partnersignup.aspx?type=ResellerRelationship&amp;id=3b33e682-00c3-41ee-9dd2-a548adf56438&amp;csp=1&amp;msppid=0",
    "attributes": {
        "objectType": "RelationshipRequest"
    }
}
```

 

 




