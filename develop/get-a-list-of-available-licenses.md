---
title: Get a list of available licenses
description: How to get a list of licenses available to users of the specified customer.
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice:  partnercenter-sdk
author: amitravat
ms.author: amrava
---

# Get a list of available licenses

**Applies to:**

- Partner Center

This article describes how to get a list of licenses available to users of the specified customer.

The following examples return licenses available from **group1**, the default license group that represents licenses managed by Azure Active Directory (Azure AD). To get available licenses for a specified license group, see [Get a list of available licenses by license group](get-a-list-of-available-licenses-by-license-group.md).

## Prerequisites

- Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with App+User credentials only.

- A customer ID (`customer-tenant-id`). If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard). Select **CSP** from the Partner Center menu, followed by **Customers**. Select the customer from the customer list, then select **Account**. On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section. The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).

## C\#

To retrieve the list of licenses available from the default license group to users of a customer:

1. Use the [**IAggregatePartner.Customers.ById**/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.

2. Get the value of the [**SubscribedSkus**/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscribedskus) property to retrieve an interface to customer subscribed SKU collection operations.

3. Call the [**Get**/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.get) or [**GetAsync**/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.getasync) method to retrieve the list of licenses.

``` csharp
// string selectedCustomerId;
// IAggregatePartner partnerOperations;

var customerUserSubscribedSkus = partnerOperations.Customers.ById(selectedCustomerId).SubscribedSkus.Get();
```

For an example, see the following:

- Sample: [Console test app](console-test-app.md)
- Project: **Partner Center SDK Samples**
- Class: **GetCustomerSubscribedSkus.cs**

## REST request

### Request syntax

| Method  | Request URI                                                                                    |
|---------|------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscribedskus HTTP/1.1 |

#### URI parameter

Use the following path parameter to identify the customer.

| Name        | Type   | Required | Description                                           |
|-------------|--------|----------|-------------------------------------------------------|
| customer-id | string | Yes      | A GUID formatted string that identifies the customer. |

### Request headers

For more information, see [Partner Center REST headers](headers.md).

### Request body

None.

### Request example

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscribedskus HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 53308f82-1bf7-44e2-8dda-4517e4688bd4
MS-CorrelationId: 95660db2-7425-4021-babe-a26ddbcb0187
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## REST response

If successful, the response body contains a collection of [SubscribedSku](license-resources.md#subscribedsku) resources.

### Response success and error codes

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For a full list, see [Partner Center REST error codes](error-codes.md).

### Response example

```http
HTTP/1.1 200 OK
Content-Length: 4859
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 95660db2-7425-4021-babe-a26ddbcb0187
MS-RequestId: 53308f82-1bf7-44e2-8dda-4517e4688bd4
MS-CV: 7BQ0jitzXUCLwRM6.0
MS-ServerId: 020021921
Date: Fri, 09 Jun 2017 17:50:46 GMT

 {
    "totalCount": 2,
    "items": [{
            "availableUnits": 4,
            "activeUnits": 5,
            "consumedUnits": 1,
            "suspendedUnits": 0,
            "totalUnits": 5,
            "warningUnits": 0,
            "productSku": {
                "id": "efccb6f7-5641-4e0e-bd10-b4976e1bf68e",
                "name": "Enterprise Mobility + Security E3",
                "skuPartNumber": "EMS",
                "targetType": "User",
                "licenseGroupId": "group1"
            },
            "servicePlans": [{
                    "displayName": "Azure Information Protection Premium P1",
                    "serviceName": "RMS_S_PREMIUM",
                    "id": "6c57d4b6-3b23-47a5-9bc9-69f17b4947b3",
                    "capabilityStatus": "Enabled",
                    "targetType": "User"
                }, {
                    "displayName": "Microsoft Intune A Direct",
                    "serviceName": "INTUNE_A",
                    "id": "c1ec4a95-1f05-45b3-a911-aa3fa01094f5",
                    "capabilityStatus": "Enabled",
                    "targetType": "User"
                }, {
                    "displayName": "Microsoft Azure Active Directory Rights",
                    "serviceName": "RMS_S_ENTERPRISE",
                    "id": "bea4c11e-220a-4e6d-8eb8-8ea15d019f90",
                    "capabilityStatus": "Enabled",
                    "targetType": "User"
                }, {
                    "displayName": "Azure Active Directory Premium P1",
                    "serviceName": "AAD_PREMIUM",
                    "id": "41781fb2-bc02-4b7c-bd55-b576c07bb09d",
                    "capabilityStatus": "Enabled",
                    "targetType": "User"
                }, {
                    "displayName": "Microsoft Azure Multi-Factor Authentication",
                    "serviceName": "MFA_PREMIUM",
                    "id": "8a256a2b-b617-496d-b51b-e76466e88db0",
                    "capabilityStatus": "Enabled",
                    "targetType": "User"
                }
            ],
            "capabilityStatus": "Enabled",
            "attributes": {
                "objectType": "SubscribedSku"
            }
        },  {
            "availableUnits": 0,
            "activeUnits": 1,
            "consumedUnits": 1,
            "suspendedUnits": 0,
            "totalUnits": 1,
            "warningUnits": 0,
            "productSku": {
                "id": "f8a1db68-be16-40ed-86d5-cb42ce701560",
                "name": "Power BI Pro",
                "skuPartNumber": "POWER_BI_PRO",
                "targetType": "User",
                "licenseGroupId": "group1"
            },
            "servicePlans": [{
                    "displayName": "Exchange Foundation",
                    "serviceName": "EXCHANGE_S_FOUNDATION",
                    "id": "113feb6c-3fe4-4440-bddc-54d774bf0318",
                    "capabilityStatus": "Enabled",
                    "targetType": "Tenant"
                }, {
                    "displayName": "Power BI Pro",
                    "serviceName": "BI_AZURE_P2",
                    "id": "70d33638-9c74-4d01-bfd3-562de28bd4ba",
                    "capabilityStatus": "Enabled",
                    "targetType": "User"
                }
            ],
            "capabilityStatus": "Enabled",
            "attributes": {
                "objectType": "SubscribedSku"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
