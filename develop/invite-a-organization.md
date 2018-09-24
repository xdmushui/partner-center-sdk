---
title: Invite a organization
description: How to invite an organization
ms.assetid: 
ms.date: 10/01/18
ms.localizationpriority: medium
---

# Invite a organization


**Applies To**

-   Partner Center


Invite a organization

## <span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>Prerequisites


-   Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.


## <span id="REST_Request"></span><span id="rest_request"></span><span id="REST_REQUEST"></span>REST Request


**Request syntax**

| Method   | Request URI                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **POST** | https://api.partner.microsoft.com/v1/referrals/                                                    |

**Request headers**

-   See [Partner Center REST headers](headers.md) for more information.

**Request body**

This table describes the [Referral](referral.md) properties in the request body.

| Property              | Type                                              | Description                                                                                                       |
|-----------------------|---------------------------------------------------|-------------------------------------------------------------------------------------------------------------------|
| Id                    | string                                            | The ID for this Referral.                                                                                         |
| EngagementId          | string                                            | The EngagementID for this Referral. Multiple referrals can be associated to a single EngagementID                 |
| OrganizationId        | string                                            | The organization ID of the party that received/owns the referral (Microsoft Partner Account ID / MSFT).           |
| BusinessProfileId     | string                                            | The business profile ID of the organization who received/owns the referral.                                       |
| OrganizationName      | string                                            | The organization name that received/owns the referral. Example: Store your own Dynamics 365 load/opportunity ID   |
| ExternalReferenceId   | string                                            | An external identifier for the referral.                                                                          |
| CreatedDateTime       | string in UTC date time format                    | The date the referral was created.                                                                                |
| UpdatedDateTime       | string in UTC date time format                    | The date the referral was last updated.                                                                           |
| ExpirationDateTime    | string in UTC date time format                    | The date the referral will expire.                                                                                |
| Status                | [ReferralStatus](referral.md#ReferralStatus)      | An [Enum](https://docs.microsoft.com/en-us/dotnet/api/system.enum) with values that indicate the referral status. |
| StatusDetail          | [ReferralStatusDetail](referral.md#ReferralStatusDetail)      | An [Enum](https://docs.microsoft.com/en-us/dotnet/api/system.enum) with values that indicate the referral status detail. |
| ReferralType          | [ReferralType](referral.md#ReferralType)          | Represents the referral type.                                                                                     |
| Qualification         | [ReferralQualification](referral.md#ReferralQualification)| Represents the quality of the referral.                                                                           |
| CustomerProfile       | [CustomerProfile](referral.md#CustomerProfile)    | Customer contact information.                                                                                     |
| Consent               | [CustomerConsent](referral.md#CustomerConsent)    | Consent flags around sharing information with other organizations and allowing them to contact the customer          |
| Details               | [ReferralDetails](referral.md#ReferralDetails)    | Customer details, notes, deal value, closing date.                                                                |
| Team                  | [Member](referral.md#Member)                      | Represents users in the organizations that are involved in the partner engagement                                 |
| InviteContext         | [InviteContext](referral.md#InviteContext)        | Represents additional information a user can provide when inviting another organization into the partner engagement   |


**Request example**

```http
POST https://api.partner.microsoft.com/v1/referrals HTTP/1.1
Authorization: Bearer <token>
Host: api.partner.microsoft.com
Content-Type: application/json

to do

```

## <span id="Response"></span><span id="response"></span><span id="RESPONSE"></span>REST Response

If successful, this API returns a [Referral](referral.md) resource. Save the Referral ID for future use.

**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Error Codes](error-codes.md).

**Response example**

``` http

to do 

```

 

 




