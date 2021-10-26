---
title: Transition a new commerce subscription
description: Upgrades a customer's new commerce subscription to a specified target subscription.
ms.date: 02/23/2021
ms.service: partner-dashboard
ms.subservice:  partnercenter-sdk
author: BrentSerbus
ms.author: brserbus
---

# Transition a new commerce subscription

**Applies To**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

**Appropriate roles**

- Global admin
- Admin agent

> [!Note] 
> New Commerce changes are currently available only to partners who are part of the M365/D365 new commerce experience technical preview.

Used to upgrade a customer's new commerce subscription to a target subscription. In order to transition a subscriptions, two API requests need to be made. First **GET eligible transitions** to get the SKUs available for upgrade. Then **POST transition** to execute the transition. These methods support both traditional and new commerce source subscriptions.  

## Get transition eligibilities

Returns a list of eligible transitions for a given customer, subscription and requested type.

### Prerequisites

- Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.

- A customer ID (`customer-tenant-id`). If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard). Select **CSP** from the Partner Center menu, followed by **Customers**. Select the customer from the customer list, then select **Account**. On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section. The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).

- A subscription ID for the initial subscription.

### REST request

#### Request syntax

| Method   | Request URI                                                                                                                         |
|----------|-------------------------------------------------------------------------------------------------------------------------------------|
| **GET**  | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/transitionEligibilities?eligibilityType={immediate, scheduled} HTTP/1.1 |

#### URI parameter

Use the following query parameters to return eligible transitions.

| Name                    | Type     | Required | Description                                       |
|-------------------------|----------|----------|---------------------------------------------------|
| **customer-tenant-id**  | **guid** | Y        | A GUID corresponding to the customer's tenant.             |
| **subscription-id** | **guid** | Y        | A GUID corresponding to the initial subscription. |
| **eligibilityType**       | **string** | N        | Describes when the transition is to be executed; can be immediate or scheduled. Default is `Immediate`.  |

#### Request headers

For more information, see [Partner Center REST headers](headers.md).

#### Request body

None

#### Request example

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/transitionEligibilities?eligibilityType=immediate HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
X-Locale: en-US
```

### REST response

If successful, this method returns a list of the eligible transitions for the given subscription in the response body.

#### Response success and error codes

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Error Codes](error-codes.md).

#### Eligibility errors

Error descriptions and meaning.

| Error description | Meaning  |
|-------------------------|----------|
|Subscription cannot be Transitioned - source subscription is not active. | Original sub status not Active |
|Subscription cannot be Transitioned - source subscription is not provisioned yet. | Original sub FulfillmentState is not success |
|Transition type is not compatible - AzureAD subscription mapping is required. | LegacyCannotConvertSubscriptionId error when calling GetSubscriptionUpgradeConflicts |
|Transition type is not compatible - conflicting subscriptions for license transfer exist. | If any AAD service has subscription ids from a different subscription, add it to the conflict list (includes purchases made with either legacy or modern purchase flow) |

#### Response example

```http
HTTP/1.1 200 OK
Content-Length: 138
Content-Type: application/json
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
Date: Fri, 26 Feb 2021 20:42:26 GMT

{
    "totalCount": 2,
    "items": [
        {
            "catalogItemId": "CFQ7TTC0KZCR:0001:CFQ7TTC0K71H",
            "title": "Microsoft 365 E5 Test Sku Title",
            "description": "Microsoft 365 E5 Test Sku Description",
            "quantity": 1,
            "eligibilities": [
{
                    "isEligible": true,
                    "transitionType": "transition_only",
                    "errors": []
                },
                
{
                    "isEligible": false,
                    "transitionType": "transition_with_license_transfer",
                    "errors": [
                        {
                            "code": 3,
                            "description": "Subscription cannot be transitioned because there are conflicting services."
                        }
                    ]
                }
            ],
            "attributes": {
                "objectType": "TransitionEligibility"
            }
        },
        {
            "catalogItemId": "CFQ7TTC0L4M3:0001:CFQ7TTC0K78T",
            "title": "Business Premium Test Sku Title",
            "description": "Business Premium Test Sku Description",
            "quantity": 1,
            "eligibilities": [
                {
                    "isEligible": false,
                    "transitionType": "transition_with_license_transfer",
                    "errors": [
                        {
                            "code": 3,
                            "description": "Subscription cannot be transitioned because there are conflicting services."
                        }
                    ]
                }
            ],
            "attributes": {
                "objectType": "TransitionEligibility"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```

## Post Transition

Posts a transition request for a given customer and subscription. Returns the transition with its initial status.

### Prerequisites

- Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.

- A customer ID (`customer-tenant-id`). If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard). Select **CSP** from the Partner Center menu, followed by **Customers**. Select the customer from the customer list, then select **Account**. On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section. The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).

- A subscription ID for the initial subscription.

### REST request

#### Request syntax

| Method   | Request URI                                                                                                                         |
|----------|-------------------------------------------------------------------------------------------------------------------------------------|
| **POST**  | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/transitions HTTP/1.1 |


#### URI parameter

Use the following query parameters to execute a transition.

| Name                    | Type     | Required | Description                                       |
|-------------------------|----------|----------|---------------------------------------------------|
| **customer-tenant-id**  | **guid** | Y        | A GUID corresponding to the customer's tenant.             |
| **subscription-id** | **guid** | Y        | A GUID corresponding to the initial subscription. |

#### Request headers

For more information, see [Partner Center REST headers](headers.md).

#### Request body

This table describes the [Transition](transition-resources.md#transition) properties in the request body.

| Property              | Type             | Required        | Description                                                                                               |
|-----------------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| fromCatalogItemId     | string           | No              | The catalog item you are transitioning from.                                                              |
| fromSubscriptionId    | string           | No              | The the subscription id you are transitioning from.                                                       |
| toCatalogItemId       | string           | Yes             | The catalog item you are transitioning to.                                                                |
| toSubscriptionId      | string           | No              | The the subscription id  you are transitioning to.                                                        |
| quantity              | integer          | No              | The number of licenses to transition over.                                                                |
| termDuration          | string           | No              | Specifiying the term duration of the subscription.                                                        |
| billingCycle          | string           | No              | Specifiying the billing cycle of the subscription.                                                        |
| transitionType        | string           | No              | The transition type. Possible values - `transition_only`, `transition_with_license_transfer`.             |

#### Request example

```http
POST https://api.partnercenter.microsoft.com/v1/customers/{customerId}/subscriptions/{subscriptionId}/transitions HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
X-Locale: en-US

{
    "fromCatalogItemId": "CFQ7TTC0LF8Q:0001:CFQ7TTC0K39X",
    "fromSubscriptionId": "e487e8dc-421e-4275-cb42-3c1c8daccf70",
    "toCatalogItemId": "CFQ7TTC0LF8R:0001:CFQ7TTC0KCSV",
    "toSubscriptionId": "0af52192-4a2a-4364-d25b-c8ecab3a5697",
    "quantity": 2,
    "termDuration": "P1M",
    "billingCycle": "Monthly",
    "transitionType": "transition_only"
}
```

### REST response

If successful, this method returns a [Transition](transition-resources.md#transition) resource with its initial status.

#### Response success and error codes

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Error Codes](error-codes.md).

#### Response example

```http
HTTP/1.1 200 OK
Content-Length: 138
Content-Type: application/json
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
Date: Fri, 26 Feb 2021 20:42:26 GMT

{
    "fromCatalogItemId": "CFQ7TTC0LF8Q:0001:CFQ7TTC0K39X",
    "fromSubscriptionId": "e487e8dc-421e-4275-cb42-3c1c8daccf70",
    "toCatalogItemId": "CFQ7TTC0LF8R:0001:CFQ7TTC0KCSV",
    "toSubscriptionId": "0af52192-4a2a-4364-d25b-c8ecab3a5697",
    "quantity": 2,
    "termDuration": "P1M",
    "billingCycle": "Monthly",
    "transitionType": "transition_only"
    "Events": [
        {
            "name": "Conversion",
            "status": "Started ",
            "timestamp": "2021-01-08T18:01:14.7488618Z",
            "attributes":
            {
                "objectType": "TransitionEvent"
            }
        }
    ],
    "attributes":
    {
        "objectType": "Transition"
    }
}
```
