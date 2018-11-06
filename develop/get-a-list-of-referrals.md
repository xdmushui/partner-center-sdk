---
title: Get a list of referrals
description: How to create a referral
ms.date: 11/08/18
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
            "id": "c5fbb3b6-be74-4795-9fb5-4324c73fed37",
            "engagementId": "65edc0b5-3485-41b7-a17e-dfa9ef4706e2",
            "organizationId": "7d23e5ca-19dc-4eaa-aac8-5e6b559f0d1d",
            "businessProfileId": "443ed2f5-c5b6-4a3f-9d11-5cfed621154a",
            "organizationName": "ABC Partner",
            "externalReferenceId": "",
            "createdDateTime": "2018-10-30T21:03:42.4579542Z",
            "updatedDateTime": "2018-10-30T21:03:42.4579542Z",
            "expirationDateTime": "2018-11-03T00:00:00Z",
            "status": "New",
            "substatus": "Pending",
            "qualification": "Direct",
            "type": "Independent",
            "customerProfile": {
                "name": "Fabrikam Customer Inc",
                "address": {
                    "addressLine1": "One Microsoft Way",
                    "addressLine2": "",
                    "city": "Redmond",
                    "state": "WA",
                    "postalCode": "98052",
                    "country": "US"
                },
                "size": "1to9employees",
                "team": [
                    {
                        "contactPreference": {
                            "locale": "en-US",
                            "disableNotifications": false
                        },
                        "firstName": "Sue",
                        "lastName": "Smith",
                        "phoneNumber": "1234567890",
                        "email": "sue.smith@fabrikam.com"
                    }
                ],
                "ids": {}
            },
            "consent": {
                "consentToContact": true
            },
            "details": {
                "notes": "We are interested in deploying Microsoft 365 and are looking for support in training our employees. Can you help?",
                "requirements": {
                    "industries": [
                        {
                            "id": "Education"
                        }
                    ],
                    "products": [
                        {
                            "id": "Microsoft365"
                        }
                    ],
                    "services": [
                        {
                            "id": "LearningAndCertification"
                        }
                    ]
                }
            }
            "links": {
                "relatedReferrals": {
                    "uri": "/referrals?engagementId=65edc0b5-3485-41b7-a17e-dfa9ef4706e2&api-version=v1.0",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/referrals/c5fbb3b6-be74-4795-9fb5-4324c73fed37?api-version=v1.0",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Referral"
            }
        },
        {
            "id": "61c65491-2f2c-461a-84b4-3654499bc1d9",
            "engagementId": "b1c40bb4-6d36-4eca-baa3-e1460cf2a454",
            "organizationId": "7d23e5ca-19dc-4eaa-aac8-5e6b559f0d1d",
            "businessProfileId": "4bd11569-41e0-4a5b-b5dc-0b253ead6d1c",
            "organizationName": "ABC Partner",
            "createdDateTime": "2018-10-29T21:24:52.040469Z",
            "updatedDateTime": "2018-10-29T21:24:52.040469Z",
            "expirationDateTime": "2018-11-06T00:00:00Z",
            "status": "New",
            "substatus": "Pending",
            "qualification": "SalesQualified",
            "type": "Independent",
            "customerProfile": {
                "name": "Contoso Customer Inc",
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
                        "contactPreference": {
                            "locale": "en-US",
                            "disableNotifications": false
                        },
                        "firstName": "Sue",
                        "lastName": "Smith",
                        "phoneNumber": "1234567890",
                        "email": "sue.smith@contoso.com"
                    },
                    {
                        "contactPreference": {
                            "locale": "en-US",
                            "disableNotifications": false
                        },
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
                "dealValue": 50000,
                "currency": "USD",
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
                            "name": "Dynamics 365 for Field Service",
                            "type": "Category",
                            "id": "Dynamics365forFieldService"
                        }
                    ]
                }
            },
            "team": [
                {
                    "contactPreference": {
                        "locale": "en-US",
                        "disableNotifications": false
                    },
                    "firstName": "John",
                    "lastName": "Doe",
                    "phoneNumber": "1231231234",
                    "email": "john.doe@microsoft.com"
                }
            ],
            "inviteContext": {
                "notes": "Hi ABC Partner, hoping you can help this customer. Thanks, John @ Microsoft",
                "invitedBy": {
                    "organizationId": "msft"
                }
            },
            "links": {
                "relatedReferrals": {
                    "uri": "/referrals?engagementId=b1c40bb4-6d36-4eca-baa3-e1460cf2a454&api-version=v1.0",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/referrals/61c65491-2f2c-461a-84b4-3654499bc1d9?api-version=v1.0",
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
            "uri": "/referrals?api-version=v1.0",
            "method": "GET",
            "headers": [
                {
                    "key": "MS-ContinuationToken",
                    "value": "g2q9mn5G/SJYYddorHEJ2ZLfGt9Z8XgT9kvVPbTWpBy4o6nrABKProJryRimedhKImLrIX85wa8ZViryeGjik386S+byTR1XwtDk3erWTYwoG+7Rpq+dAB2kSqj0pIPCcDd1fTOnVSRkwl+8Rk6FeMSj86BO2OW6P+1GwYzXfuecUvYJaodMS7eRM7dZFHQMR5OEVI21STM8TYVCE1aityEDBv18Y/6mRJbirj9zTcfJNPAUSEWrqmQoEoKoeV9PMQkVaWYx8KnWhrBXmpD2gM3vY1GvgPVZlhVy73g5X+G3JVZ0ol0rlPRTFHcrKXF143lEZPbnaeOCPc/Y1c3aJ8umE/LBKBjMv5Cwgq2ZtqdyignVbsCdSg/a5O43xCCmLDNVN+phhI0mvCZkWphqiMZAuH0myt6zHznMWVLTCnILsGtW4g8KDYyyK37wdW7j03+jd7SqWw8jvGSQARZxTcEhrZQ8G0tlPgwTk9ufDs6GPhE7FastVOGdzzD60aLn"
                }
            ]
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

In the above example pageSize=2 is passed in the querystring and will only return two results. If there are more items a "MS-ContinuationToken" key/value is returned. To get the next page of records pass the MS-ContinuationToken in the header.

**Request example**

```http
GET https://api.partner.microsoft.com/v1.0/engagements/referrals&pageSize=2&self=true&status=Active HTTP/1.1
Authorization: Bearer <token>
Host: api.partner.microsoft.com
Content-Type: application/json
ContinuationToken: 8GWNiKD4N/PCmdR5cpsz8Sxc9GYLmFJnanfGLSaQB2e5Rrxtp4OGy37p4nsnWM0Mp7PW4ZzNriCnUSNS8DohFta2M6j09OpKmVx7js/uEiMUE1AryHHgr+fdW8QU8xdeIDG5bSe72VbqEDUTUYLZgTcBeZWBcZLt30mHSW4A5tmJl4VWywKlgEdH6PpfjBQB0Z0EnW14isS7+zDAHOc4Jq+9j8/nDkSE7zEz/Ot+BTHGB2ky+ILLhQ39QQq+elGEcjLtFmrNWyYDUFR5HBe7c+IppL+Kk2lwAekVPuOeq3CfksYkCQgxiPgb8s/oOheCJBeu7rl7KhPnIkHUN2XzagLfBzJLAsPobgoiVzTHtqc9n47kuktHqmAhSv37V4RlxoADmUSzpUs6xT6sfwWBFAEeSlzvBVekvDe1S10sChID4xpaJxcBxMfXQT739E82iVHlWbdDJhAWrKlq1mlIO0ERCxYpr3N32mhNImo/Qs0=

```
