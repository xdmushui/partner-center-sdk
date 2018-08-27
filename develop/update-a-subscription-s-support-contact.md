---
title: Update a subscription's support contact
description: How to update a subscription's support contact to one of the partner’s value added resellers.
ms.assetid: 6DE6EF60-6F8B-46F2-8278-CD706081B180
ms.author: mhopkins
ms.date: 12/15/2017
ms.topic: article
ms.prod: partner-center
ms.technology: partner-center-sdk
ms.localizationpriority: medium
---

# Update a subscription's support contact


**Applies To**

-   Partner Center
-   Partner Center for Microsoft Cloud Germany
-   Partner Center for Microsoft Cloud for US Government

How to update a subscription's support contact to one of the partner’s value added resellers.

## <span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>Prerequisites


-   Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with App+User credentials only.
-   A customer identifier.
-   A subscription identifier.
-   Information about the new support contact: tenant identifier, Microsoft Partner Network identifier, and name. The support contact must be one of the partner's value added resellers.

## <span id="C_"></span><span id="c_"></span>C#


To update a subscription's support contact, first instantiate and populate a [**SupportContact**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.subscriptions.supportcontact) object with the new values. Then use the [**IAggregatePartner.Customers.ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer. Next, get an interface to subscription operations by calling the [**Subscriptions.ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the subscription ID. Then, use the [**SupportContact**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.supportcontact) property to obtain an interface to support contact operations. Finally, call the [**Update**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionsupportcontact.update) or [**UpdateAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionsupportcontact.updateasync) method with the populated SupportContact object to update the support contact.

``` csharp
// IAggregatePartner partnerOperations.
// string customerId;
// string subscriptionId; 

// Instantiate a SupportContact object and populate it with the new support contact information.
var supportContact = new SupportContact()
{
    Name = "Support contact’s name",
    SupportTenantId = "Support contact’s tenant ID",
    SupportMpnId = "Support contact’s MPN ID"
};

// Update the support contact with a new object that has valid VAR values.
var updatedSupportContact = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionID).SupportContact.Update(supportContact);
```

**Sample**: [Console test app](console-test-app.md). **Project**: Partner Center SDK Samples **Class**: UpdateSubscriptionSupportContact.cs

## <span id="_Request"></span><span id="_request"></span><span id="_REQUEST"></span> Request


**Request syntax**

| Method  | Request URI                                                                                                                    |
|---------|--------------------------------------------------------------------------------------------------------------------------------|
| **PUT** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/supportcontact HTTP/1.1 |

 

**URI parameter**

Use the following path parameters to identify the customer and subscription.

| Name            | Type   | Required | Description                                                     |
|-----------------|--------|----------|-----------------------------------------------------------------|
| customer-id     | string | Yes      | A GUID formatted string that identifies the customer.           |
| subscription-id | string | Yes      | A GUID formatted string that identifies the trial subscription. |

 

**Request headers**

-   See [Partner Center REST headers](headers.md) for more information.

**Request body**

You must include a populated [SupportContact](subscriptions.md#supportcontact) resource in the request body. The support contact must be an existing reseller with a relationship to the partner.

**Request example**

```
PUT https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/C8D8FBAB-6A62-44DC-BE50-B7C74E43A296/supportcontact HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b72d732a-eed7-4a60-82d1-1b2e6cba0ed2
MS-CorrelationId: 84eff9e1-6a8c-42aa-8678-c00b0d3fb26f
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 320
Expect: 100-continue

{
    "SupportTenantId": "3B33E682-00C3-41EE-9DD2-A548ADF56438",
    "SupportMpnId": "4391507",
    "Name": "Trey Research",
    "Links": {
        "Self": {
            "Uri": "/customers/0C39D6D5-C70D-4C55-BC02-F620844F3FD1/subscriptions/C8D8FBAB-6A62-44DC-BE50-B7C74E43A296/supportcontact",
            "Method": "Get",
            "Headers": []
        }
    },
    "Attributes": {
        "ObjectType": "SupportContact"
    }
}
```

## <span id="_Response"></span><span id="_response"></span><span id="_RESPONSE"></span> Response


If successful, the response body contains the [SupportContact](subscriptions.md#supportcontact) resource.

**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center error codes](error-codes.md).

**Response example**

```http
HTTP/1.1 200 OK
Content-Length: 328
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b0cd9bcc-742e-4c76-9e34-a96d3bdc7673
MS-RequestId: 7591ca22-d4e3-409d-bfa6-09806eaff4f3
MS-CV: W8Tzj6NGckKHcq+E.0
MS-ServerId: 030020344
Date: Wed, 21 Jun 2017 01:01:17 GMT

﻿{
    "supportTenantId": "3B33E682-00C3-41EE-9DD2-A548ADF56438",
    "supportMpnId": "4391507",
    "name": "Trey Research",
    "links": {
        "self": {
            "uri": "/customers/0C39D6D5-C70D-4C55-BC02-F620844F3FD1/subscriptions/C8D8FBAB-6A62-44DC-BE50-B7C74E43A296/supportcontact",
            "method": "Get",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "SupportContact"
    }
}
```

 

 




