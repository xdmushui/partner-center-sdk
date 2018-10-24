---
title: Invite an organization
description: How to invite an organization
ms.date: 10/01/18
ms.localizationpriority: medium
---

# Invite a organization


**Applies To**

-   Partner Center


This topic explains how to invite an organization

## <span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>Prerequisites


-   Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.


## <span id="REST_Request"></span><span id="rest_request"></span><span id="REST_REQUEST"></span>REST Request

**Request syntax**

| Method   | Request URI                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **POST** | https://api.partner.microsoft.com/engagements/referrals?api-version=v1.0                                                    |

**Request headers**

-   See [Partner Center REST headers](headers.md) for more information.

**Request body**

This table describes the [Referral](referral.md) properties in the request body.

| Property              | Type                                              | Description                                                                                                       |
|-----------------------|---------------------------------------------------|-------------------------------------------------------------------------------------------------------------------|
| Id                    | string                                            | The ID for this Referral.                                                                                         |
| EngagementId          | string                                            | The EngagementID for this Referral. Multiple referrals can be associated to a single EngagementID                 |
| OrganizationId        | string                                            | The organization ID of the party that owns the referral (Microsoft Partner Account ID / MSFT).           |
| BusinessProfileId     | string                                            | The business profile ID of the organization that owns the referral.                                       |
| OrganizationName      | string                                            | The organization name that owns the referral. Example: Store your own Dynamics 365 lead/opportunity ID   |
| ExternalReferenceId   | string                                            | An external identifier for the referral.                                                                          |
| CreatedDateTime       | string in UTC date time format                    | The date the referral was created.                                                                                |
| UpdatedDateTime       | string in UTC date time format                    | The date the referral was last updated.                                                                           |
| ExpirationDateTime    | string in UTC date time format                    | The date the referral will expire.                                                                                |
| Status                | [ReferralStatus](referral.md#ReferralStatus)      | An [Enum](https://docs.microsoft.com/dotnet/api/system.enum) with values that indicate the referral status. |
| Substatus          | [ReferralSubstatus](referral.md#ReferralSubstatus)      | An [Enum](https://docs.microsoft.com/dotnet/api/system.enum) with values that indicate the referral status detail. |
| ReferralType          | [ReferralType](referral.md#ReferralType)          | Represents the referral type.                                                                                     |
| Qualification         | [ReferralQualification](referral.md#ReferralQualification)| Represents the quality of the referral.                                                                           |
| CustomerProfile       | [CustomerProfile](referral.md#CustomerProfile)    | Customer contact information.                                                                                     |
| Consent               | [CustomerConsent](referral.md#CustomerConsent)    | Consent flags around sharing information with other organizations and allowing them to contact the customer.         |
| Details               | [ReferralDetails](referral.md#ReferralDetails)    | Customer details, notes, deal value, closing date.                                                                |
| Team                  | [Member](referral.md#Member)                      | Represents users in the organizations that are involved in the partner engagement.                                |
| InviteContext         | [InviteContext](referral.md#InviteContext)        | Represents additional information a user can provide when inviting another organization into the partner engagement.  |


**Request example**

```http
POST https://api.partner.microsoft.com/engagements/referrals?api-version=v1.0 HTTP/1.1
Authorization: Bearer <token>
Host: api.partner.microsoft.com
Content-Type: application/json

{  
    "engagementId": "bde8552b-958b-4663-8a7b-96fae3d009b3",
    "organizationId": "msft",
    "organizationName": "Microsoft",
    "ExternalReferenceId": "MyCRMID1234",
    "status": "New",
    "Substatus":"Pending",
    "Type": "Shared",
    "Qualification": "SalesQualified",
    "customerProfile": {
        "name": "AdventureWorks",
        "size": "10to50employees",
        "address": {
            "addressLine1": "One Microsoft Way",
            "addressLine2": "34",
            "city": "Redmond",
            "state": "WA",
            "postalCode": "98052",
            "country": "US"
        },
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
        ]
    },
    "consent": {
    	"ConsentToToShareInfoWithOthers": "true",
    	"ConsentToContact": "true",
    	"ConsentToMicrosoftToContactSpecificPartners": "true"
    },
    "details": {
        "notes": "Customer is looking to leverage Microsoft 365 in their bicycle store chain. They are also interested in an insights and analytics application to track sales performance.",
        "dealValue": 15000,
        "requirements": {
         "Industries": [
                {
                    "id": "Retail & Consumer Goods"
                }
            ],
             "products": [
                {
                    "id": "Microsoft365"
                }
            ],
            "services": [
                {
                    "id": "DeploymentOrMigration"
                }
            ],
            "solutions": [
            	{   "id": "SOL-34104-EBA",
                	"name": "Business Insights and Analytics",
                    "type": "Name"
                }
            ]
        }
    },
    "team": [
    	{
            "firstName": "Luke",
            "lastName": "Johnson",
            "phoneNumber": "1231231234",
            "email": "luke.johnson@fabrikam.com"
        }
    ],
    "inviteContext" : {
    	"notes": "Hi Microsoft, I would like your support in co-selling with Adventure Works."
    }
}
```


## <span id="Response"></span><span id="response"></span><span id="RESPONSE"></span>REST Response

If successful, this API returns a [Referral](referral.md) resource. Save the Referral ID for future use.

**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Error Codes](error-codes.md).

**Response example**

``` http
<to do> 
```
