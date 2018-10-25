---
title: Update referral status
description: How to to update a referral's status
ms.date: 10/01/18
ms.localizationpriority: medium
---

# Update referral status


**Applies To**

-   Partner Center


This topic explains how to update a referral's status.


## <span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>Prerequisites

-   Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.


## <span id="REST_Request"></span><span id="rest_request"></span><span id="REST_REQUEST"></span>REST Request


**Request syntax**

| Method   | Request URI                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **PUT** | https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}                                      |

 
**Request headers**

-   See [Partner Center REST headers](headers.md) for more information.

**Request body**

This table describes the [Referral](referral.md) properties in the request body.

| Property              | Type                                              | Description                                                                                                       |
|-----------------------|---------------------------------------------------|-------------------------------------------------------------------------------------------------------------------|
| Id                    | string                                            | The ID for this Referral.                                                                                         |
| EngagementId          | string                                            | The EngagementID for this Referral. Multiple referrals can be associated to a single EngagementID                 |
| Name                  | string                                            | The name of the Referral.                 |
| OrganizationId        | [profiles](referral.md#OrganizationProfile)       | The organization ID of the party that owns the referral.           |
| BusinessProfileId     | string                                            | The business profile ID of the organization that owns the referral.                                       |
| OrganizationName      | string                                            | The organization name that owns the referral. Example: Store your own Dynamics 365 lead/opportunity ID   |
| ExternalReferenceId   | string                                            | An external identifier for the referral.                                                                          |
| CreatedDateTime       | string in UTC date time format                    | The date the referral was created.                                                                                |
| UpdatedDateTime       | string in UTC date time format                    | The date the referral was last updated.                                                                           |
| ExpirationDateTime    | string in UTC date time format                    | The date the referral will expire.                                                                                |
| Status                | [ReferralStatus](referral.md#ReferralStatus)      | An [Enum](https://docs.microsoft.com/dotnet/api/system.enum) with values that indicate the referral status. |
| Substatus          | [ReferralSubstatus](referral.md#ReferralSubstatus)      | An [Enum](https://docs.microsoft.com/dotnet/api/system.enum) with values that indicate the referral sub status. |
| StatusReason          | string                                            | A descriptive message about the status. Example: Why was the referral lost? |
| ReferralType          | [ReferralType](referral.md#ReferralType)          | Represents the referral type.                                                                                     |
| Qualification         | [ReferralQualification](referral.md#ReferralQualification)| Represents the quality of the referral.                                                                           |
| CustomerProfile       | [CustomerProfile](referral.md#CustomerProfile)    | Customer contact information.                                                                                     |
| Consent               | [CustomerConsent](referral.md#CustomerConsent)    | Consent flags around sharing information with other organizations and allowing them to contact the customer.         |
| Details               | [ReferralDetails](referral.md#ReferralDetails)    | Customer details, notes, deal value, currency closing date.                                                                |
| Team                  | [Member](referral.md#Member)                      | Represents users in the organizations that are involved in the partner engagement.                                |
| InviteContext         | [InviteContext](referral.md#InviteContext)        | Represents additional information a user can provide when inviting another organization into the partner engagement.  |

**Status & Substatus transition states**

| Status                | Allowed Status Transition     | Allowed Substatus                  |
|-----------------------|-------------------------------|---------------------------------------|
| New                   | New, Active, Closed           | Pending, Received                     |
| Active                | Active, Closed                | Accepted                              |
| Closed                | Closed                        | Won, Lost, Declined, Expired          |

**Request example**

```http
PUT https://api.partner.microsoft.com/v1.0/engagements/referrals/49d90c72-3326-4f61-aacc-2cb57970448c HTTP/1.1
Authorization: Bearer <token>
Host: api.partner.microsoft.com
Content-Type: application/json
 
 {
    "id": "49d90c72-3326-4f61-aacc-2cb57970448c",
    "organizationId": "msft",
    "organizationName": "Microsoft",
    "externalReferenceId": "mycrmid1234",
    "createdDateTime": "2018-10-01T18:17:36.254263Z",
    "updatedDateTime": "2018-10-01T18:17:36.254263Z",
    "expirationDateTime": "2018-10-09T00:00:00Z",
    "status": "Closed",
    "Substatus": "Won",
    "StatusReason": "Customer engagement was a success!",
    "qualification": "SalesQualified",
    "type": "Shared",
    "customerProfile": {
        "name": "AdventureWorks",
        "address": {
            "addressLine1": "One Microsoft Way",
            "addressLine2": "34",
            "city": "Redmond",
            "state": "WA",
            "postalCode": "98052",
            "country": "US"
        },
        "size": "10to50employees",
        "team": [
            {
                "firstName": "John",
                "lastName": "Doe",
                "phoneNumber": "1234567890",
                "email": "john.doe@adventure-works.com"
            },
            {
                "firstName": "Dawn",
                "lastName": "Smith",
                "phoneNumber": "4035698759",
                "email": "dawn.smith@adventure-works.com"
            }
        ],
        "ids": {}
    },
    "consent": {
        "consentToToShareInfoWithOthers": true,
        "consentToContact": true,
        "consentToMicrosoftToContactSpecificPartners": true
    },
    "details": {
        "notes": "Customer is looking to leverage Microsoft 365 in their bicycle store chain. They are also interested in an insights and analytics application to track sales performance.",
        "requirements": {}
    },
    "team": [
        {
            "firstName": "Luke",
            "lastName": "Johnson",
            "phoneNumber": "1231231234",
            "email": "luke.johnson@fabrikam.com"
        }
    ]
}
```

## <span id="Response"></span><span id="response"></span><span id="RESPONSE"></span>REST Response

If successful, this method returns the populated [Referral](referral.md) resource in the response body.

**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Error Codes](error-codes.md).

**Response example**

``` http
{
    "id": "49d90c72-3326-4f61-aacc-2cb57970448c",
    "engagementId": "a9c8c67f-6b29-4a80-abf8-2b07a41b7902",
    "organizationId": "msft",
    "organizationName": "Microsoft",
    "externalReferenceId": "mycrmid1234",
    "createdDateTime": "2018-10-01T20:51:16.8337242Z",
    "updatedDateTime": "2018-10-01T20:51:16.8337242Z",
    "expirationDateTime": "2018-10-09T00:00:00Z",
    "status": "Closed",
    "Substatus": "Won",
    "StatusReason": "Customer engagement was a success!",
    "qualification": "SalesQualified",
    "type": "Shared",
    "customerProfile": {
        "name": "AdventureWorks",
        "address": {
            "addressLine1": "One Microsoft Way",
            "addressLine2": "34",
            "city": "Redmond",
            "state": "WA",
            "postalCode": "98052",
            "country": "US"
        },
        "size": "10to50employees",
        "team": [
            {
                "firstName": "John",
                "lastName": "Doe",
                "phoneNumber": "1234567890",
                "email": "john.doe@adventure-works.com"
            },
            {
                "firstName": "Dawn",
                "lastName": "Smith",
                "phoneNumber": "4035698759",
                "email": "dawn.smith@adventure-works.com"
            }
        ],
        "ids": {}
    },
    "consent": {
        "consentToToShareInfoWithOthers": true,
        "consentToContact": true,
        "consentToMicrosoftToContactSpecificPartners": true
    },
    "details": {
        "notes": "Customer is looking to leverage Microsoft 365 in their bicycle store chain. They are also interested in an insights and analytics application to track sales performance.",
        "requirements": {}
    },
    "team": [
        {
            "firstName": "Luke",
            "lastName": "Johnson",
            "phoneNumber": "1231231234",
            "email": "luke.johnson@fabrikam.com"
        }
    ],
    "links": {
        "relatedReferrals": {
            "uri": "/v2/referrals/?engagementId=a9c8c67f-6b29-4a80-abf8-2b07a41b7902",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/v2/referrals/49d90c72-3326-4f61-aacc-2cb57970448c",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Referral"
    }
}
```
