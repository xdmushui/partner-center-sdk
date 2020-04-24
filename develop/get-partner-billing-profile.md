---
title: Get partner billing profile
description: Gets an object representing the partner's billing profile.
ms.assetid: E5BAC2C4-8C58-4B5D-8FA9-C445896EEC4A
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice:  partnercenter-sdk
ms.localizationpriority: medium
---

# Get partner billing profile

**Applies To**

- Partner Center
- Partner Center operated by 21Vianet
- Partner Center for Microsoft Cloud Germany
- Partner Center for Microsoft Cloud for US Government

Gets an object representing the partner's billing profile.

## Prerequisites

- Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with App+User credentials only.

## C\#

To get a partner billing profile, use your **IAggregatePartner.Profiles** collection and call the **BillingProfile** property. Finally, call the [**Get()**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.profiles.ibillingprofile.get) or [**GetAsync()**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.profiles.ibillingprofile.getasync) methods.

``` csharp
// IAggregatePartner partnerOperations;

BillingProfile billingProfile = partnerOperations.Profiles.BillingProfile.Get();
```

**Sample**: [Console test app](console-test-app.md). **Project**: PartnerCenterSDK.FeaturesSamples **Class**: GetBillingProfile.cs

## REST request

### Request syntax

| Method  | Request URI                                                              |
|---------|--------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/billing HTTP/1.1 |

### Request headers

For more information, see [Partner Center REST headers](headers.md).

### Request body

None.

### Request example

```http
GET https://api.partnercenter.microsoft.com/v1/profiles/billing HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a0dd6cde-b24c-413c-af24-416446dc5599
MS-CorrelationId: 1bb03149-88d2-4bc2-9cc1-d6e83890fa9e
```

## REST response

If successful, this method returns a **BillingProfile** object in the response body.

### Response success and error codes

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Error Codes](error-codes.md).

### Response example

```http
HTTP/1.1 200 OK
Content-Length: 568
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 1bb03149-88d2-4bc2-9cc1-d6e83890fa9e
MS-RequestId: a0dd6cde-b24c-413c-af24-416446dc5599
Date: Tue, 22 Mar 2016 17:10:02 GMT

{
    "companyName":"TEST_TEST_BugBash1",
    "address":{
        "country":"US",
        "city":"Redmond",
        "state":"WA",
        "addressLine1":"1 Microsoft Way",
        "addressLine2":"","postalCode":"98052"
    },
    "primaryContact":{
        "firstName":"James",
        "lastName":"Burk",
        "phoneNumber":"2066017143"
    },
    "purchaseOrderNumber":"9888",
    "taxId":"12-345678",
    "billingCurrency":"USD",
    "profileType":"BillingProfile",
    "links":{
        "self":{
            "uri":"/profiles/billing",
            "method":"GET",
            "headers":[]
        }
    },
    "attributes":{
        "etag":<etag>,
        "objectType":"BillingProfile"
    }
}
```
