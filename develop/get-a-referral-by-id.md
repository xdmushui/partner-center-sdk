---
title: Get a referral by ID
description: How to create a referral
ms.date: 10/01/18
ms.localizationpriority: medium
---

# Get a referral by ID


**Applies To**

-   Partner Center


This topic explains how to create a referral.


## <span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>Prerequisites

-   Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.


## <span id="REST_Request"></span><span id="rest_request"></span><span id="REST_REQUEST"></span>REST Request

**Request syntax**

| Method   | Request URI                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **GET** | https://api.partner.microsoft.com/v1/referrals/{referralId}                                        |

 
**URI parameter**

Use the following query parameters to get a list of referrals

| Name                   | Type     | Required | Description                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|Id                      | string   | No       | A referral ID       |

**Request headers**

-   See [Partner Center REST headers](headers.md) for more information.

**Request body**

This table describes the [Referral](referral.md) properties in the request body.

**Request example**

```http
GET https://api.partner.microsoft.com/v1/referrals/{referralId} HTTP/1.1
Authorization: Bearer <token>
Host: api.partner.microsoft.com
Content-Type: application/json

```


## <span id="Response"></span><span id="response"></span><span id="RESPONSE"></span>REST Response

If successful, this method returns the populated [Referral](referral.md) resource in the response body.

**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Error Codes](error-codes.md).

**Response example**

``` http
{
    "id": "fa2ebe8d-754c-4d43-baa1-c31688a9c8ff",
    "engagementId": "5357cdc2-743e-4dd5-89c6-f3731f8b69ce",
    "organizationId": "msft",
    "organizationName": "Microsoft",
    "externalReferenceId": "mycrmid1234",
    "createdDateTime": "2018-09-26T22:50:17.9817213Z",
    "updatedDateTime": "2018-09-26T22:50:17.9817213Z",
    "expirationDateTime": "2018-10-04T00:00:00Z",
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
        "requirements": {
            "industries": [
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
                {
                    "name": "Business Insights and Analytics",
                    "type": "Name",
                    "id": "SOL-34104-EBA"
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
    "links": {
        "relatedReferrals": {
            "uri": "/v2/referrals/?engagementId=5357cdc2-743e-4dd5-89c6-f3731f8b69ce",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/v2/referrals/fa2ebe8d-754c-4d43-baa1-c31688a9c8ff",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Referral"
    }
}
```
