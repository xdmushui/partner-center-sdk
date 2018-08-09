---
title: Verify domain availability
description: How to determine if a domain is available for use.
ms.assetid: 9ECF8241-3672-441D-B34D-83F7C23138B3
ms.author: mhopkins
ms.date: 12/15/2017
ms.topic: article
ms.prod: partner-center
ms.technology: partner-center-sdk
ms.localizationpriority: medium
---

# Verify domain availability


**Applies To**

-   Partner Center
-   Partner Center operated by 21Vianet
-   Partner Center for Microsoft Cloud Germany
-   Partner Center for Microsoft Cloud for US Government

How to determine if a domain is available for use.

## <span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>Prerequisites


-   Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.
-   A domain (e.g. "contoso.onmicrosoft.com").

## <span id="C_"></span><span id="c_"></span>C#


To verify if a domain is available, first call [**IAggregatePartner.Domains**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.ipartner.domains) to obtain an interface to domain operations. Then call the [**ByDomain**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.domains.idomaincollection.bydomain) method with the domain to check. This retrieves an interface to the operations available for a specific domain. Finally, call the [**Exists**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.domains.idomain.exists) method to see if the domain already exists.

``` csharp
// IAggregatePartner partnerOperations;
// const string domain = "contoso.onmicrosoft.com";  

bool result = partnerOperations.Domains.ByDomain(domain).Exists();
```

**Sample**: [Console test app](console-test-app.md). **Project**: Partner Center SDK Samples **Class**: CheckDomainAvailability.cs

## <span id="Request"></span><span id="request"></span><span id="REQUEST"></span>Request


**Request syntax**

| Method   | Request URI                                                              |
|----------|--------------------------------------------------------------------------|
| **HEAD** | [*{baseURL}*](partner-center-rest-urls.md)/v1/domains/{domain} HTTP/1.1 |

 

**URI parameter**

Use the following query parameter to verify domain availability.

| Name       | Type       | Required | Description                                   |
|------------|------------|----------|-----------------------------------------------|
| **domain** | **string** | Y        | A string that identifies the domain to check. |

 

**Request headers**

-   See [Partner Center REST headers](headers.md) for more information.

**Request body**

None

**Request example**

```
HEAD https://api.partnercenter.microsoft.com/v1/domains/contoso.onmicrosoft.com HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: cf5b00d6-9240-431c-a973-cc06c904e5bf
MS-CorrelationId: ec57501a-a4c3-45ee-ab2b-da4250545fc9
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <span id="Response"></span><span id="response"></span><span id="RESPONSE"></span>Response


If the domain exists it is not available for use and a response status code 200 OK is returned. If the domain is not found it is available for use and a response status code 404 Not Found is returned.

**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center REST error codes](error-codes.md).

**Response example for when the domain is already in use**

```
HTTP/1.1 200 OK
Content-Length: 0
MS-CorrelationId: ec57501a-a4c3-45ee-ab2b-da4250545fc9
MS-RequestId: cf5b00d6-9240-431c-a973-cc06c904e5bf
MS-CV: 7UXAHds8J0mNUCSp.0
MS-ServerId: 201022015
Date: Tue, 31 Jan 2017 22:22:35 GMT
```

**Response example for when the domain is available**

```
HTTP/1.1 404 Not Found
Content-Length: 0
MS-CorrelationId: 54770745-17f0-433c-bd7b-0265e5b38f98
MS-RequestId: 1169a4cd-3be7-4e29-9cb3-0f78ffa2e91e
MS-CV: RRmc+bEw9U2e97CC.0
MS-ServerId: 202010406
Date: Tue, 31 Jan 2017 22:36:01 GMT
```

 

 




