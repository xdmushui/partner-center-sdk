---
title: Get a customer's company profile
description: Gets the company profile of a customer.
ms.assetid: 762C0F38-2229-464D-9CD6-6AD82135A65C
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice:  partnercenter-sdk
ms.localizationpriority: medium
---

# Get a customer's company profile

**Applies To**

- Partner Center
- Partner Center operated by 21Vianet
- Partner Center for Microsoft Cloud Germany
- Partner Center for Microsoft Cloud for US Government

Gets the company profile of a customer.

## <span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>Prerequisites

- Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with App+User credentials only.
- A customer ID (customer-tenant-id). If you do not have a customer's ID, you can look up the ID in Partner Center by choosing the customer from the customers list, selecting Account, then saving their Microsoft ID.

## <span id="Examples"/><span id="examples"><span id="EXAMPLES"/>Examples

### C#

To get the company profile for a customer, call the [**IAggregatePartner.Customers.ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer. Then get the customer's [**ICustomerProfileCollection**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection) interface from the [**Profiles**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomer.profiles) property, in order to access its Company property. Next, get the [**ICustomerReadonlyProfile**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1) interface from the [**ICustomerProfileCollection.Company**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection.company) property, and call its [**Get()**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.get) or [**GetAsync()**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.getasync) methods.

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;

var companyProfile = partnerOperations.Customers.ById(customerId).Profiles.Company.Get();
```

**Sample**: [Download the Partner Center SDK](https://go.microsoft.com/fwlink/p/?LinkId=746681). **Project**: PartnerSdk.FeatureSamples **Class**: GetCustomerCompanyProfile.cs

### Java

[!INCLUDE [<Partner Center Java SDK support details>](<../includes/java-sdk-support.md>)]

To get the company profile for a customer, call the **IAggregatePartner.getCustomers().byId** function with the customer identifier to identify the customer. Then get the customer's **ICustomerProfileCollection** interface from the [**getProfiles**] function, in order to access its Company property. Next, get the **ICustomerReadonlyProfile** interface from the **ICustomerProfileCollection.getCompany** function, and call the **get** function.

```java
// IAggregatePartner partnerOperations;
// String customerId;

CustomerCompanyProfile companyProfile = partnerOperations.getCustomers().byId(customerId).getProfiles().getCompany().get();
```

## <span id="Request"/><span id="request"/><span id="REQUEST"/>Request

**Request syntax**

| Method  | Request URI                                                             |
|---------|-------------------------------------------------------------------------|
| **GET** | *{baseURL}*/v1/customers/{customer-tenant-id}/profiles/company HTTP/1.1 |

**URI parameter**

Use the following query parameter to get the company profile.

| Name                   | Type     | Required | Description                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **customer-tenant-id** | **guid** | Y        | The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller. |


**Request headers**

- See [Partner Center REST Headers](headers.md) for more information.

**Request body**

None

**Request example**

```http
GET https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/profiles/company HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 0b6f039c-e4b5-4b9e-bdac-b39077bb60da
MS-CorrelationId: ffa9174c-dbcb-47de-b70d-10e640a7f1b4
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <span id="Response"/><span id="response"/><span id="RESPONSE"/>Response


If successful, this method returns information in the response body.

**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center REST Error Codes](error-codes.md).

**Response example**

```http
HTTP/1.1 200 OK
Content-Length: 488
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ffa9174c-dbcb-47de-b70d-10e640a7f1b4
MS-RequestId: 0b6f039c-e4b5-4b9e-bdac-b39077bb60da
MS-CV: /e74N8OrkE29ycwZ.0
MS-ServerId: 101112202
Date: Wed, 04 Jan 2017 19:48:51 GMT

{
    "tenantId": "4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04",
    "domain": "dtdemocspcustomer005.onmicrosoft.com",
    "companyName": "DT Demo CSP Customer 005",
    "address": {
        "country": "US",
        "region": "WA",
        "city": "Redmond ",
        "addressLine1": "1 Microsoft Way",
        "postalCode": "98052",
        "phoneNumber": "4155551212"
    },
    "email": "daniel@hotmail.com.tw",
    "links": {
        "self": {
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/profiles/company",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "CustomerCompanyProfile"
    }
}
```