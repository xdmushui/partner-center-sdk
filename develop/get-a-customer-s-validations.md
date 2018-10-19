---
title: Get a partner's Government Community Cloud validations
description: How to get a partner's Government Community Cloud validations.
ms.assetid: 1C9E986B-2887-460B-9D71-4520BB18C32A
ms.date: 09/12/2018
ms.localizationpriority: medium
---


# Get a partner's validation codes

**Applies To**

-   Partner Center
-   Partner Center operated by 21Vianet
-   Partner Center for Microsoft Cloud Germany
-   Partner Center for Microsoft Cloud for US Government

How to get a collection of a partner's Government Community Cloud validation. Validations are required to access the government community cloud.

If you are interested in having your organization or your customers organization approved for Office 365 Government GCC for CSP, please see [Office 365 Government GCC for CSP Partner and Customer Eligibility Criteria](https://docs.microsoft.com/partner-center/csp-gcc-validate).  


## <span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>Prerequisites

-   Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.
-   Confirmed validation after filling out form [here](https://products.office.com/en-US/government/eligibility-validation?ReqType=CSPPartner).
-   A customer with a Government Community Cloud qualification.
-   A customer identifier.


## <span id="C_"></span><span id="c_"></span>C#

To get a list of all of a partner's validations, first use the [**IAggregatePartner.Validations**](https://docs.microsoft.com/en-us/dotnet/api/microsoft.store.partnercenter.validations.ivalidations?view=partnercenter-dotnet-latest) method with the customer identifier to identify the customer. Then use the [**Validations**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomer.validations) property to retrieve an interface to validation collection operations. Finally, call the [**Get**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) or [**GetAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) methods to retrieve the customer's validations collection.

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;

var gccValidations = partnerOperations.Validations.GetValidationCodes();
```


## <span id="Request"></span><span id="request"></span><span id="REQUEST"></span>Request

**Request syntax**

| Method  | Request URI                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/all/validations HTTP/1.1 |


**Request headers**

-   See [Partner Center REST headers](headers.md) for more information.

**Request body**

None.

**Request example**

```http
GET https://api.partnercenter.microsoft.com/v1/customers/all/validations HTTP/1.1
Accept: application/json
Content-Type: application/json
cache-control: no-cache
Authorization: Bearer <token>
Host: api.partnercenter.microsoft.com
cookie: MarketplaceSelectedLocale=en-US; LocalizationRouteName=artemissite
accept-encoding: gzip, deflate
Connection: close
```


## <span id="Response"></span><span id="response"></span><span id="RESPONSE"></span>Response

If successful, this method returns a [Validation](validations.md) resources in the response body.

**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center REST error codes](error-codes.md).

**Response example**

```http
HTTP/1.1 200 OK
Content-Length: 434
Content-Type: application/json
MS-CorrelationId: 283b9b70-963a-4159-9920-f2bdf7ab7fce
MS-RequestId: 7266f5f6-30ca-4672-9eb6-6c9d6dd0e9d3
X-Locale: en-US,en-US
MS-CV: wR5itJ70YEWmVtNh.0
MS-ServerId: 000000
Date: Fri, 19 Oct 2018 17:52:05 GMT
Connection: close

[
  {
    "partnerId": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d",
    "organizationName": "Contoso, Inc.",
    "validationId": "12345",
    "maxCreates": 5,
    "remainingCreates": 4,
    "eTag": "W/\"datetime'2018-10-10T18%3A49%3A58.727348Z'\""
  },
  {
    "partnerId": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d",
    "organizationName": "Contoso, Inc. Finance Department",
    "validationId": "987654",
    "maxCreates": 5,
    "remainingCreates": 5,
    "eTag": "W/\"datetime'2018-10-19T17%3A51%3A45.6584512Z'\""
  }
]
```
