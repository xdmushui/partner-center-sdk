---
title: Get a list of referrals
description: How to create a referral
ms.assetid: 
ms.author: mhopkins
ms.date: 10/01/18
ms.topic: article
ms.prod: partner-center
ms.technology: partner-center-sdk
ms.localizationpriority: medium
---

# Get a list of referrals


**Applies To**

-   Partner Center


How to create a referral

## <span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>Prerequisites


-   Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.


## <span id="REST_Request"></span><span id="rest_request"></span><span id="REST_REQUEST"></span>REST Request


**Request syntax**

| Method   | Request URI                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **GET** | https://api.partner.microsoft.com/v1/referrals/                                                     |


**URI parameter**

Use the following query parameters to get a list of referrals

| Name                   | Type     | Required | Description                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|engagementId            | string   | No       | An engagement ID       |
|self                    | string   | No       | A string of value "true". Will return only the referrals for your organization      |
|status                  | string   | No       | A string that represents a [ReferralStatus](referral.md#ReferralStatus)        |
|invitedByOrganization   | string   | No       | An organization ID. Will return referrals associated to an specific organization       |
 
**Request headers**

-   See [Partner Center REST headers](headers.md) for more information.

**Request body**

None.

**Request example**

```http
GET https://api.partner.microsoft.com/v1/referrals HTTP/1.1
Authorization: Bearer <token>
Host: api.partner.microsoft.com
Content-Type: application/json
 
<to do>

```

## <span id="Response"></span><span id="response"></span><span id="RESPONSE"></span>REST Response

If successful, the response body contains a collection of [Referral](referral.md) resources in the response body.

**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Error Codes](error-codes.md).

**Response example**

``` http
<to do>
```

 

 




