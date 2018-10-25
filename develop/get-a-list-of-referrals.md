---
title: Get a list of referrals
description: How to create a referral
ms.date: 10/01/18
ms.localizationpriority: medium
---

# Get a list of referrals


**Applies To**

-   Partner Center


This topic explains how to create a referral.


## <span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>Prerequisites

-   Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.


## <span id="REST_Request"></span><span id="rest_request"></span><span id="REST_REQUEST"></span>REST Request

**Request syntax**

| Method   | Request URI                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **GET** | https://api.partner.microsoft.com/v1.0/engagements/referrals?pageSize=20&self=true&status=new                |

**URI parameter**

Use the following query parameters to get a list of referrals

| Name                   | Type     | Required | Description                                                                        |
|------------------------|----------|----------|------------------------------------------------------------------------------------|
|engagementId            | string   | No       | An engagement ID.                                                                  |
|self                    | string   | No       | A string of value "true" will return only the referrals for your organization.     |
|status                  | string   | No       | A string that represents a [ReferralStatus](referral.md#ReferralStatus).           |
|pageSize                | string   | No       | Number of referrals that should be returned. 100 is the maximum.                   |
|invitedByOrganization   | string   | No       | An [organization ID](profiles.md#OrganizationProfile). Will return referrals associated with a specific organization. |


 
**Request headers**

-   See [Partner Center REST headers](headers.md) for more information.

**Request body**

None.

**Request example**

```http
GET https://api.partner.microsoft.com/v1.0/engagements/referrals&pageSize=2&self=true&status=Active HTTP/1.1
Authorization: Bearer <token>
Host: api.partner.microsoft.com
Content-Type: application/json

```


## <span id="Response"></span><span id="response"></span><span id="RESPONSE"></span>REST Response

If successful, the response body contains a collection of [Referral](referral.md) resources in the response body.

**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Error Codes](error-codes.md).

**Response example**

``` http
{
    "totalCount": 2,
    "items": [        
        {
            "id": "e491c7e7-9e8c-4309-acd4-d4c1826ae17d",
            "engagementId": "e312414d-718a-4685-be09-83fe323a012a",
            "organizationId": "msft",
            "organizationName": "Microsoft",
            "externalReferenceId": "mycrmid1234",
            "createdDateTime": "2018-10-01T18:09:24.3590344Z",
            "updatedDateTime": "2018-10-01T18:09:24.3590344Z",
            "expirationDateTime": "2018-10-09T00:00:00Z",
            "status": "Active",
            "Substatus": "Accepted",
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
                    "uri": "/v2/referrals/?engagementId=e312414d-718a-4685-be09-83fe323a012a",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/v2/referrals/e491c7e7-9e8c-4309-acd4-d4c1826ae17d",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Referral"
            }
        },
        {
            "id": "f2f4ba01-e6ae-45b1-936b-7404a83ee04d",
            "engagementId": "7055d680-e974-4378-aa60-456d2d57caff",
            "organizationId": "msft",
            "organizationName": "Microsoft",
            "externalReferenceId": "mycrmid1234",
            "createdDateTime": "2018-10-01T18:17:14.7383089Z",
            "updatedDateTime": "2018-10-01T18:17:14.7383089Z",
            "expirationDateTime": "2018-10-09T00:00:00Z",
            "status": "Active",
            "Substatus": "Accepted",
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
                    "uri": "/v2/referrals/?engagementId=7055d680-e974-4378-aa60-456d2d57caff",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/v2/referrals/f2f4ba01-e6ae-45b1-936b-7404a83ee04d",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Referral"
            }
        }
    ],
    "links": {
        "next": {
            "uri": "/v2/referrals/",
            "method": "GET",
            "headers": [
                {
                    "key": "MS-ContinuationToken",
                    "value": "I8mkG0aYAcwWv2+An8mkFh7QuRWhSZLenXBHNdCBRXVIqIsCbLIbCMunXURexTjlvL0AvkhUznSvuV7d9tphe5rwOorMSRKfCBQCEMkWpaYVXKpguTDGAoGT9h67jq42rbxSlRAUgZ++Xs0sNqRw+rgRpXv5oopXxonelj9LvePooI/5/7tDXwGjNzKdU3AqC3fjpdW88AMF+AgIzU8e342zTvCzZCcKMHL5JHylG1mLiZ5qLXEVXC5qQe3rlfg9gY8SphB7+PSyugR1fSkDCS+eEfhfss58LjRTTqGPa2NAhUPosEAjtQ5nDgXw26dPbR8pnY70N8Ggm8jOLjc2Sxk8AwVX+LOP1EoeQPi7zQr7zBduiGynZG3equ+FUXxkvtn7/NMhTtWCxaaHwYX+o/eaXgJan+d/Z8L3MEZDHamgIeWcaNFgsIO74Cdz7Ya51sRoYlaPZz4Wow8PXnoNjWnaF0kgn6yHX2lTw0BdH12oB4e1bKCnTts4oKg3aKWP3nAFCYsZC0PGapKNrxvyKQ=="
                }
            ]
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
