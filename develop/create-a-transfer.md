---
title: Create a transfer
description: How to create a transfer of subscriptions for a customer.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice:  partnercenter-sdk
ms.localizationpriority: medium
---

# Create a transfer

**Applies to:**

- Partner Center
- Partner Center operated by 21Vianet
- Partner Center for Microsoft Cloud Germany
- Partner Center for Microsoft Cloud for US Government

## Prerequisites

- Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.

- A customer ID (`customer-tenant-id`). If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard). Select **CSP** from the Partner Center menu, followed by **Customers**. Select the customer from the customer list, then select **Account**. On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section. The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).

## REST request

### Request syntax

| Method   | Request URI                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **POST** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/transfers HTTP/1.1                    |

### URI parameter

Use the following path parameter to identify the customer.

| Name            | Type     | Required | Description                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| **customer-id** | string   | Yes      | A GUID formatted customer-id that identifies the customer.             |

### Request headers

For more information, see [Partner Center REST headers](headers.md).

### Request body

This table describes the [TransferEntity](transfer-entity-resources.md) properties in the request body.

| Property              | Type          | Required  | Description                                                                                |
|-----------------------|---------------|-----------|--------------------------------------------------------------------------------------------|
| id                    | string        | No    | A transferEntity identifier that is supplied upon successful creation of the transferEntity.                               |
| createdTime           | DateTime      | No    | The date the transferEntity was created, in date-time format. Applied upon successful creation of the transferEntity.      |
| lastModifiedTime      | DateTime      | No    | The date the transferEntity was last updated, in date-time format. Applied upon successful creation of the transferEntity. |
| lastModifiedUser      | string        | No    | The user who last updated the transferEntity. Applied upon successful creation of transferEntity.                          |
| customerName          | string        | No    | Optional. The name of the customer whose subscriptions are being transferred.                                              |
| customerTenantId      | string        | No    | A GUID formatted customer-id that identifies the customer. Applied upon successful creation of the transferEntity.         |
| partnertenantid       | string        | No    | A GUID formatted partner-id that identifies the partner.                                                                   |
| sourcePartnerName     | string        | No    | Optional. The name of the partner's organization who is initiating the transfer.                                           |
| sourcePartnerTenantId | string        | Yes   | A GUID formatted partner-id that identifies the partner initiating the transfer.                                           |
| targetPartnerName     | string        | No    | Optional. The name of the partner's organization to whom the transfer is targeted.                                         |
| targetPartnerTenantId | string        | Yes   | A GUID formatted partner-id that identifies the partner to whom the transfer is targeted.                                  |
| lineItems             | Array of objects | Yes| An Array of [TransferLineItem](transfer-entity-resources.md#transferlineitem) resources.                                   |
| status                | string        | No    | The status of the transferEntity. Possible values are "Active" (can be deleted/submitted) and "Completed" (has already been completed). Applied upon successful creation of the transferEntity.|

This table describes the [TransferLineItem](transfer-entity-resources.md#transferlineitem) properties in the request body.

|      Property       |            Type             | Required | Description                                                                                     |
|---------------------|-----------------------------|----------|-------------------------------------------------------------------------------------------------|
| id                   | string                     | No       | A unique identifier for a transfer line item. Applied upon successful creation of the transferEntity.|
| subscriptionId       | string                     | Yes      | The subscription identifier.                                                                         |
| quantity             | int                        | No       | The number of licenses or instances.                                                                 |
| billingCycle         | Object                     | No       | The type of billing cycle set for the current period.                                                |
| friendlyName         | string                     | No       | Optional. The friendly name for the item defined by the partner to help disambiguate.                |
| partnerIdOnRecord    | string                     | No       | PartnerId on Record (MPNID) on the purchase that happens when the transfer is accepted.              |
| offerId              | string                     | No       | The offer identifier.                                                                                |
| addonItems           | List of **TransferLineItem** objects | No | A collection of transferEntity line items for addons that will be transferred along with the base subscription that is being transferred. Applied upon successful creation of the transferEntity.|
| transferError        | string                     | No       | Applied after transferEntity is accepted in case of an error.                                        |
| status               | string                     | No       | The status of the lineitem in the transferEntity.                                                    |

### Request example

```http
POST /v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/transfers HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4fa6dad6-a89f-4875-8247-7294a10ae1cf
MS-CorrelationId: 0e93c70c-977c-4a88-9580-7cf084c73286
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Expect: 100-continue

{
    "sourcePartnerTenantId": "da6c51b5-1246-4a42-b4ab-cbf38df54537",
    "targetPartnerTenantId": "656218b1-80c9-40b2-83ae-3a2703b55271",
    "lineItems": [
        {
            "subscriptionId": "7291BFBF-1772-4C5B-A624-18B6152CD8CB",
            "partnerIdOnRecord": "517285"
        },
        {
            "subscriptionId": "6C0B221B-8DF9-4F4A-A5BB-4C9CBB7B27B0",
            "partnerIdOnRecord": "517285"
        }
    ]
}
```

## REST response

If successful, this method returns the populated [TransferEnity](transfer-entity-resources.md) resource in the response body.

### Response success and error codes

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Error Codes](error-codes.md).

### Response example

```http
HTTP/1.1 201 Created
Content-Length: 138
Content-Type: application/json; charset=utf-8
MS-RequestId: 4fa6dad6-a89f-4875-8247-7294a10ae1cf
MS-CorrelationId: 0e93c70c-977c-4a88-9580-7cf084c73286
X-Locale: en-US,en-US
{
    "id": "67c5b05b-09b5-47ba-9047-5056fe2afa4f",
    "status": "Active",
    "createdTime": "2020-03-24T20:44:14.9602781Z",
    "lastModifiedTime": "2020-03-24T20:44:15Z",
    "customerTenantId": "823c6c3f-9259-4d51-bae2-5dd06743177f",
    "partnertenantid": "da6c51b5-1246-4a42-b4ab-cbf38df54537",
    "sourcePartnerTenantId": "da6c51b5-1246-4a42-b4ab-cbf38df54537",
    "targetPartnerTenantId": "656218b1-80c9-40b2-83ae-3a2703b55271",
    "lastModifiedUser": "d0648481-b615-45c9-8cd1-ff87940dbdc4",
    "lineItems": [
        {
            "id": 0,
            "subscriptionId": "7291BFBF-1772-4C5B-A624-18B6152CD8CB",
            "offerId": "50E9A47A-7B4D-4970-9D90-CAE927F53753",
            "billingCycle": "annual",
            "friendlyName": "Dynamics 365 for Sales Enterprise Attach to Qualifying Dynamics 365 Base Offer",
            "quantity": 1,
            "addonItems": [
                {
                    "id": 0,
                    "subscriptionId": "D738C6C9-DDBD-46E9-B316-65F9D9B3ECB4",
                    "offerId": "2BCF9FE8-8B65-4FCF-9240-419203FB8CF4",
                    "billingCycle": "annual",
                    "friendlyName": "Dynamics 365 - Additional Production Instance (Qualified Offer)",
                    "quantity": 4
                }
            ]
        },
        {
            "id": 0,
            "subscriptionId": "6C0B221B-8DF9-4F4A-A5BB-4C9CBB7B27B0",
            "offerId": "455DDD41-32ED-4E2D-B3A2-BBCB22CAA467",
            "billingCycle": "annual",
            "friendlyName": "Dynamics 365 Customer Engagement Plan Patch",
            "quantity": 8,
            "addonItems": []
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/823c6c3f-9259-4d51-bae2-5dd06743177f/transfers/67c5b05b-09b5-47ba-9047-5056fe2afa4f",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "TransferEntity"
    }
}
```
