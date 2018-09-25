---
title: Create a referral
description: How to create a referral
ms.assetid: 
ms.date: 10/01/18
ms.localizationpriority: medium
---

# Create a referral


**Applies To**

-   Partner Center


How to create a referral

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
| OrganizationId        | string                                            | The organization ID of the party that owns the referral (Microsoft Partner Account ID / MSFT).           |
| BusinessProfileId     | string                                            | The business profile ID of the organization that owns the referral.                                       |
| OrganizationName      | string                                            | The organization name that owns the referral. Example: Store your own Dynamics 365 lead/opportunity ID   |
| ExternalReferenceId   | string                                            | An external identifier for the referral.                                                                          |
| CreatedDateTime       | string in UTC date time format                    | The date the referral was created.                                                                                |
| UpdatedDateTime       | string in UTC date time format                    | The date the referral was last updated.                                                                           |
| ExpirationDateTime    | string in UTC date time format                    | The date the referral will expire.                                                                                |
| Status                | [ReferralStatus](referral.md#ReferralStatus)      | An [Enum](https://docs.microsoft.com/dotnet/api/system.enum) with values that indicate the referral status. |
| StatusDetail          | [ReferralStatusDetail](referral.md#ReferralStatusDetail)      | An [Enum](https://docs.microsoft.com/dotnet/api/system.enum) with values that indicate the referral status detail. |
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

{
  {
  "organizationId": "1",
  "businessProfileId": "1",
  "organizationName": "Contoso Inc",
  "externalReferenceId": "CRMID1234567",
  "createdDateTime": "2018-09-21T17:23:33.809Z",
  "updatedDateTime": "2018-09-21T17:23:33.809Z",
  "expirationDateTime": "2018-09-21T17:23:33.809Z",
  "status": "New",
  "statusDetail": "Pending",
  "qualification": "SalesQualified",
  "type": "Shared",
  "customerProfile": {
    "id": "string",
    "name": "Contoso Inc",
    "address": {
      "addressLine1": "One Microsoft Way",
      "addressLine2": "",
      "city": "Redmond",
      "state": "WA",
      "postalCode": "98034",
      "country": "US",
      "region": ""
    },
    "size": "251to1000employees",
    "team": [
      {
        "firstName": "Sue",
        "lastName": "Smith",
        "phoneNumber": "425-789-7889",
        "email": "sue.smith@contoso.com"
      }
    ],
    "ids": {
      "duns": "1234567"
    }
  },
  "consent": {
    "consentToToShareInfoWithOthers": true,
    "consentToContact": true,
    "consentToMicrosoftToContactSpecificPartners": true
  },
  "details": { 
    "notes": "Customer is looking to leverage Dynamics 365 to manage their supply chain. There is also a need to leverage a set of custom apps to enable their business processes.",
    "estimatedDealValue": "50000",
    "estimatedClosingDateTime": "2018-09-21T17:23:33.810Z",
    "requirements": {
      "industries": [
        {
          "id": "Healthcare"
        }
      ],
      "products": [
        {
          "id": "Azure"
        }
      ],
      "services": [
        {
          "id": "DeploymentOrMigration"
        }
      ],
      "solutions": [
        {
          "id": "DevOps"
        }
      ]
    }
  },
  "team": [
    {
      "firstName": "Ryan",
      "lastName": "Barschaw",
      "phoneNumber": "123-456-7890",
      "email": "rbars@microsoft.com"
    }
  ],
  "inviteContext": {
    "notes": "Hi Microsoft, I would like your support in migrating Contoso Inc to Dynamics 365",
    "invitedByOrganizationId": "string"
  }
}

```

## <span id="Response"></span><span id="response"></span><span id="RESPONSE"></span>REST Response

If successful, this API returns a [Referral](referral.md) resource. Save the Referral ID for future use with the Partner Center SDK.

**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Error Codes](error-codes.md).

**Response example**

``` http

to do

```

 

 




