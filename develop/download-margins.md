---
title: Gets a list of margins in comma delimited format for a given partner.
description: Gets a list of margins in comma delimited format for a given partner.
ms.date: 09/30/2021
ms.service: partner-dashboard
ms.subservice:  partnercenter-sdk
author: BrentSerbus
ms.author: brserbus
---

# Download margins


**Applies to**: Partner Center 

**Appropriate roles**: Global admin | Admin agent

Partners can get a list of active margins for a given partner. This method returns margins based on the partner and available start and end dates. Download margins returns the data in a comma delimited format.

## Prerequisites

- Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.


## REST request
[GET] /v1/margins

### Request syntax

| Method   | Request URI                                                                                                                         |
|----------|-------------------------------------------------------------------------------------------------------------------------------------|
| **GET**  | [*{baseURL}*](partner-center-rest-urls.md)/v1/margins/download HTTP/1.1 |

### Request headers

For more information, see [Partner Center REST headers](headers.md).

### Request body

None

### Request example

```http
GET https://api.partnercenter.microsoft.com/v1/margins/download HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
X-Locale: en-US
```

## REST response

If successful, this method returns the price list as a file stream as a.csv file

### Response success and error codes

Each response comes with an HTTP status code that indicates success or failure and more debugging information. Use a network trace tool to read this code, error type, and more parameters. For the full list, see [Error Codes](error-codes.md).

### Response example

```http
HTTP/1.1 200 OK
Content-Length: 138
Content-Type: application/json
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
Date: Fri, 26 Feb 2021 20:42:26 GMT

"id","productId","publisherName","productTitle","productType"","marginPercentage","startDate","endDate","status","statusDate"
"97620c21cc32_97cdce68-cce4-42aa-9410-233fd0269502","DZH318Z08L40","Market Place Test","Software As A Service Support Preview App","SaaS","10.0","2021-08-04T23:16:22.4736653Z","2022-03-31T23:59:59Z","live","2021-08-04T23:16:22.4736653Z"

```