---
title: Delete Indirect Reseller in Sandbox
description: Provides information on deleting Sandbox Indirect Resellers and enabling end-to-end testing using APIs.
ms.date: 5/24/2021
ms.author: vijvala
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
---

# Delete Indirect Reseller in Sandbox

This document shows how to delete Sandbox Indirect Providers and enable end-to-end testing using APIs.

**Applies to:** Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany

> [!Important]
> This document describes features that are only allowed in the Sandbox environment for Indirect Model experiences.

## Prerequisites

- Credentials as described in [Partner Center Authentication](partner-center-authentication.md). This scenario supports authentication with App+User credentials.

## Delete Sandbox Indirect Reseller through API

## REST request

### Request syntax

| Method | Request URI                                                                             |
|------------|-------------------------------------------------------------------------------------|
| **DELETE** | [*{baseURL}*](partner-center-rest-urls.md)/v1//sandboxIndirectReseller/{resellerId} |

### Request headers

- This API is idempotent (it will not yield a different result if you call it multiple times).
- A request ID and correlation ID are required.
- For more information, see [Partner Center REST
> headers](https://docs.microsoft.com/en-us/partner-center/develop/headers).

## Request Example

DELETE https://api.partnercenter.microsoft.com/v1/sandboxIndirectReseller/{resellerID}

```http
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

###  Response example

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
Date: Wed, 16 Feb 2021 00:43:02 GMT
```

### Response success and error codes

Each response comes with an HTTP status code that indicates success or failure as well as additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center error
codes](error-codes.md).

This method returns the following status success and error codes:

| HTTP Status Code                     | Error code     | Description                                      |
|--------------------------------------|----------------|--------------------------------------------------|
| 401                                  | 6002           | Unauthorized token or Not a Tip Provider Account |
| 403                                  | 6003           | Delete Sandbox IR is not allowed                 |
| 403                                  | 6004           | Create Sandbox IR operation not allowed          |
| 409                                  | 1003           | Conflict while creating tenant                   |
