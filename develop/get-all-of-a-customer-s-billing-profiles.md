---
title: Get a customer's billing profile
description: Gets the billing profile of a customer.In the Partner Center dashboard, this operation can be performed by first selecting a customer.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice:  partnercenter-sdk
author: dineshvu
ms.author: dineshvu
---

# Get a customer's billing profile

**Applies To**

- Partner Center
- Partner Center operated by 21Vianet
- Partner Center for Microsoft Cloud Germany
- Partner Center for Microsoft Cloud for US Government

Gets the billing profile of a customer.

In the Partner Center dashboard, this operation can be performed by first [selecting a customer](get-a-customer-by-name.md). Then, under the customer's name in the left sidebar, select **Account**. The billing profile can be found under the **Bill-to info** heading.

## Prerequisites

- Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.

- A customer ID (`customer-tenant-id`). If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard). Select **CSP** from the Partner Center menu, followed by **Customers**. Select the customer from the customer list, then select **Account**. On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section. The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).

## C\#

To get a customer's billing profile, use your [**IPartner.Customers**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection and call the [**ById()**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method. Then call the [**Profiles**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomer.profiles) property, followed by the [**Billing**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection.billing) property. Finally, call the [**Get()**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.get) or [**GetAsync()**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.getasync) methods.

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;

var billingProfile = partnerOperations.Customers.ById(selectedCustomerId).Profiles.Billing.Get();
```

**Sample**: [Console test app](console-test-app.md). **Project**: PartnerSDK.FeatureSamples **Class**: GetCustomerBillingProfile.cs

## REST request

### Request syntax

| Method  | Request URI                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/profiles/billing HTTP/1.1 |

### URI parameter

Use the following query parameter to get the billing profile.

| Name                   | Type     | Required | Description                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **customer-tenant-id** | **guid** | Y        | The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller. |

### Request headers

For more information, see [Partner Center REST headers](headers.md).

### Request body

None

### Request example

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/profiles/billing HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a5581a74-2778-4e34-9172-18baa4877081
MS-CorrelationId: 51d521b3-62db-4682-b75d-fb8ab09113b2
```

## REST response

If successful, this method returns a collection of [Profile](profile-resources.md) resources in the response body.

### Response success and error codes

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Error Codes](error-codes.md).

### Response example

```http
HTTP/1.1 200 OK
Content-Length: 1206
Content-Type: application/json
MS-CorrelationId: 51d521b3-62db-4682-b75d-fb8ab09113b2
MS-RequestId: a5581a74-2778-4e34-9172-18baa4877081
Date: Mon, 23 Nov 2015 18:13:43 GMT

{
    "id": "<billing-profile-id>",
    "firstName": "FirstName",
    "lastName": "LastName",
    "email": "email@sample.com",
    "culture": "en-US",
    "language": "en",
    "companyName": "CompanyName",
    "defaultAddress": {
        "country": "US",
        "city": "Redmond",
        "state": "WA",
        "addressLine1": "1 Microsoft Way",
        "postalCode": "98052",
        "firstName": "FirstName",
        "lastName": "LastName",
        "phoneNumber": "4255555555"
    },
    "links": {
        "self": {
            "uri": "/v1/customers/<customer-tenant-id>/profiles/billing",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "etag": "<etag>",
        "objectType": "CustomerBillingProfile"
    }
}
```
