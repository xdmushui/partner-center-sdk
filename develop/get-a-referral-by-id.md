---
title: Get a referral by ID
description: How to create a referral
ms.date: 10/01/18
ms.localizationpriority: medium
---

# Get a referral by ID


**Applies To**

-   Partner Center


This topic explains how to get a referral by ID.


## <span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>Prerequisites

-   Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.


## <span id="REST_Request"></span><span id="rest_request"></span><span id="REST_REQUEST"></span>REST Request

**Request syntax**

| Method   | Request URI                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **GET** | https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}                                     |

 
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
GET https://api.partner.microsoft.com/v1.0/engagements/referrals/0d43414c-fb9f-4ca0-9b8d-29deb70364cf HTTP/1.1
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
    "id": "0d43414c-fb9f-4ca0-9b8d-29deb70364cf",
    "engagementId": "29c3f916-8840-4565-b584-48ccafe0b835",
    "organizationId": "7d23e5ca-19dc-4eaa-aac8-5e6b559f0d1d",
    "organizationName": "Fabrikam Partner Inc",
    "externalReferenceId": "mycrmid1234",
    "createdDateTime": "2018-10-01T18:01:32.8796627Z",
    "updatedDateTime": "2018-10-01T18:01:32.8796627Z",
    "expirationDateTime": "2018-10-09T00:00:00Z",
    "status": "Active",
    "Substatus": "Accepted",
    "qualification": "SalesQualified",
    "type": "Independent",
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
