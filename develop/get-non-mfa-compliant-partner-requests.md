---
title: Get a list of non MFA partner user requests
description: Obtains a list of recent non MFA compliant partner user requests
ms.date: 05/03/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
---

# Get non MFA compliant partner requests.md

Applies to:

- Partner Center API

This topic explains how to obtain a list of non MFA compliant partner user requests. 

## Prerequisites

- Credentials as described in [Partner API authentication](api-authentication.md). This scenario supports authentication with App+User credentials.

## REST Request

### Request syntax

| Method  | Request URI                                                  |
|---------|--------------------------------------------------------------|
| **GET** | <https://api.partnercenter.microsoft.com/pcapi/v1/nonMfaCompliantPartnerPrincipals> |

### Request headers

- See [Partner API REST headers](headers.md) for more information.

### Request example

```http
POST https://api.partnercenter.microsoft.com/pcapi/v1/nonMfaCompliantPartnerPrincipals HTTP/1.1
Authorization: Bearer <token>
Host: api.partnercenter.microsoft.com
Content-Type: application/json

```

## REST Response

If successful, this method returns a response containing the following fields.

### Response body

This table describes the properties in the response body for a non MFA compliant partner principals.

| Property                            | Type            | Description               |
|-------------------------------------|-----------------|---------------------------|
| ObjectId                            | string          |                           |
| TenantId                            | string          |                           |
| Upn                                 | string          |                           |
| LastNonMfaCompliantLoginDateTime    | string          |                           |

### Response success and error codes

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Error Codes](error-codes.md).

### Response example

``` http
  {
    "objectId": "",
    "tenantId": "",
    "upn": "",
    "lastNonMfaCompliantLoginDateTime": ""
  }
```

