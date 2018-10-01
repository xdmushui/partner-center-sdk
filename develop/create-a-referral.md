---
title: Create a referral
description: How to create a referral
ms.date: 10/01/18
ms.localizationpriority: medium
---

# Create a referral


**Applies To**

-   Partner Center


This topic explains how to create a referral.


## <span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>Prerequisites

-   Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.


## <span id="REST_Request"></span><span id="rest_request"></span><span id="REST_REQUEST"></span>REST Request

**Request syntax**

| Method   | Request URI                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **POST** | https://api.partner.microsoft.com/referrals?api-version=v1.0                                                   |
 
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
| Consent               | [CustomerConsent](referral.md#CustomerConsent)    | Consent flags around sharing information with other organizations and allowing them to contact the customer.         |
| Details               | [ReferralDetails](referral.md#ReferralDetails)    | Customer details, notes, deal value, closing date.                                                                |
| Team                  | [Member](referral.md#Member)                      | Represents users in the organizations that are involved in the partner engagement.                                |
| InviteContext         | [InviteContext](referral.md#InviteContext)        | Represents additional information a user can provide when inviting another organization into the partner engagement.  |


**Request example**

```http
POST https://api.partner.microsoft.com/referrals?api-version=v1.0 HTTP/1.1
Authorization: Bearer <token>
Host: api.partner.microsoft.com
Content-Type: application/json

{  
    "ExternalReferenceId": "MyCRMID1234",
    "status": "Active",
    "statusDetail":"Pending",
    "Type": "Shared",
    "Qualification": "SalesQualified",
    "customerProfile": {
        "name": "Contoso Inc",
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
                "firstName": "Sue",
                "lastName": "Smith",
                "phoneNumber": "1234567890",
                "email": "sue.smith@contoso.com"
            },
            {
                "firstName": "Joe",
                "lastName": "Hansen",
                "phoneNumber": "4035698759",
                "email": "joe.hansen@contoso.com"
            }
        ]
    },
    "consent": {
    	"ConsentToToShareInfoWithOthers": "true",
    	"ConsentToContact": "true",
    	"ConsentToMicrosoftToContactSpecificPartners": "true"
    },
    "details": {
        "notes": "Customer is looking to leverage Dynamics 365 to manage their supply chain. There is also a need to leverage a set of custom apps to enable their business processes.",
        "dealValue": 50000,
        "requirements": {
         "Industries": [
                {
                    "id": "Manufacturing"
                }
            ],
             "products": [
                {
                    "id": "Dynamics365Enterprise"
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
    ]
    
}
```


## <span id="Response"></span><span id="response"></span><span id="RESPONSE"></span>REST Response

If successful, this API returns a [Referral](referral.md) resource. Save the Referral ID for future use with the Partner Center SDK.

**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Error Codes](error-codes.md).

**Response example**

``` http
{
    "id": "0d43414c-fb9f-4ca0-9b8d-29deb70364cf",
    "engagementId": "29c3f916-8840-4565-b584-48ccafe0b835",
    "organizationId": "msft",
    "organizationName": "Microsoft",
    "externalReferenceId": "mycrmid1234",
    "createdDateTime": "2018-10-01T18:01:32.8796627Z",
    "updatedDateTime": "2018-10-01T18:01:32.8796627Z",
    "expirationDateTime": "2018-10-09T00:00:00Z",
    "status": "Active",
    "statusDetail": "Accepted",
    "qualification": "SalesQualified",
    "type": "Shared",
    "customerProfile": {
        "name": "Contoso Inc",
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
                "firstName": "Sue",
                "lastName": "Smith",
                "phoneNumber": "1234567890",
                "email": "sue.smith@contoso.com"
            },
            {
                "firstName": "Joe",
                "lastName": "Hansen",
                "phoneNumber": "4035698759",
                "email": "joe.hansen@contoso.com"
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
        "notes": "Customer is looking to leverage Dynamics 365 to manage their supply chain. There is also a need to leverage a set of custom apps to enable their business processes.",
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
            "uri": "/v2/referrals/?engagementId=29c3f916-8840-4565-b584-48ccafe0b835",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/v2/referrals/0d43414c-fb9f-4ca0-9b8d-29deb70364cf",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Referral"
    }
}
```
