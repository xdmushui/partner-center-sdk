---
title: Update referral status
description: How to create a referral
ms.assetid: 
ms.author: mhopkins
ms.date: 10/01/18
ms.topic: article
ms.prod: partner-center
ms.technology: partner-center-sdk
ms.localizationpriority: medium
---

# Update referral status


**Applies To**

-   Partner Center


Update referral status

## <span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>Prerequisites


-   Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.


## <span id="C_"></span><span id="c_"></span>C#


To do: Describe in english how Update referral status


``` csharp
<to do>
```

## <span id="REST_Request"></span><span id="rest_request"></span><span id="REST_REQUEST"></span>REST Request


**Request syntax**

| Method   | Request URI                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **POST** | [*{baseURL}*](partner-center-rest-urls.md)/v1/referrals/{referralId}                                        |

 
**Request headers**

-   See [Partner Center REST headers](headers.md) for more information.

**Request body**

This table describes the [Referral](referral.md) properties in the request body.

| Property              | Type                                              | Description                                                                                                       |
|-----------------------|---------------------------------------------------|-------------------------------------------------------------------------------------------------------------------|
| Id                    | string                                            | The ID for this Referral.                                                                                         |
| Status                | [ReferralStatus](referral.md#ReferralStatus)     | An [Enum](https://docs.microsoft.com/en-us/dotnet/api/system.enum) with values that indicate the referral status. |
| ReferralSource        | [ReferralSource](referral.md#ReferralSource)     | An [Enum](https://docs.microsoft.com/en-us/dotnet/api/system.enum) with values that indicate the referral source. |
| CustomerProfile       | [CustomerProfile](referral.md#CustomerProfile)   | Customer contact information                                                                                      |
| Details               | [ReferralDetails](referral.md#ReferralDetails)   | Customer details, notes, deal value, closing date                                                                 |
| Participants          | [Participant](referral.md#Participant)           | Represents the customer interest in Industry, Products, Services, Solutions                                       |


**Request example**

```json
POST https://api.partner.microsoft.com/v1/referrals/{referralId} HTTP/1.1
Authorization: Bearer <token>
Host: api.partner.microsoft.com
Content-Type: application/json
 
 <to do>
```

## <span id="Response"></span><span id="response"></span><span id="RESPONSE"></span>REST Response

If successful, this method returns the populated [Referral](referral.md) resource in the response body.

**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Error Codes](error-codes.md).

**Response example**

``` json
<to do>
```

 

 




