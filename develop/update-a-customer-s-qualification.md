---
title: Update a customer's qualification
description: Updates a customer's qualification, including the address associated with the profile.
ms.date: 09/12/2018
ms.localizationpriority: medium
---

# Update a customer's qualification


**Applies To**

-   Partner Center
-   Partner Center operated by 21Vianet
-   Partner Center for Microsoft Cloud Germany
-   Partner Center for Microsoft Cloud for US Government

Updates a customer's qualification.


## <span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>Prerequisites

-   Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with App+User credentials only.
-   A customer ID (customer-tenant-id).


## <span id="C_"></span><span id="c_"></span>C#

To update a customer's qualification, retrieve the qualification and update the properties as necessary. First, with an existing  [**Customer**](https://docs.microsoft.com/en-us/dotnet/api/microsoft.store.partnercenter.models.customers.customer?view=partnercenter-dotnet-latest), use the following.

``` csharp
// CustomerQualification is an enum

var gccCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.Update(CustomerQualification.Education);
```

**Sample**: [Console test app](console-test-app.md). **Project**: PartnerSDK.FeatureSamples **Class**: CustomerQualificationOperations.cs


## <span id="_Request"></span><span id="_request"></span><span id="_REQUEST"></span> Request

**Request syntax**

| Method  | Request URI                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| **PUT** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer_id}/qualification HTTP/1.1 |


**URI parameter**

Use the following query parameter to update the qualification.

| Name                   | Type     | Required | Description                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **customer-tenant-id** | **guid** | Y        | The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller. |
| **code**               | **int**  | N        | Needed for Government Community Cloud.  For more information, visit HERE.                                                                                                                                                       |


**Request headers**

-   See [Headers](headers.md) for more information.

**Request body**

[Customer Qualification](https://docs.microsoft.com/en-us/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification?view=partnercenter-dotnet-latest)

**Request example**

```http
PUT https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualification HTTP/1.1
Accept: application/json
Content-Type: application/json
cache-control: no-cache
Authorization: Bearer <token>
User-Agent: PostmanRuntime/7.3.0
Host: api.partnercenter.microsoft.com
cookie:
accept-encoding: gzip, deflate
content-length: 1
Connection: close

1
```

## <span id="_Response"></span><span id="_response"></span><span id="_RESPONSE"></span> Response


If successful, this method returns updated [qualification](https://docs.microsoft.com/en-us/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification?view=partnercenter-dotnet-latest) in the response body.

**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Error Codes](error-codes.md).

**Response example**

```http
HTTP/1.1 200 OK
Content-Length: 14
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
X-Locale: en-US,en-US
MS-CV: mEFQl0suzEGQRSIt.0
MS-ServerId: 00000A
Date: Fri, 19 Oct 2018 16:46:23 GMT
Connection: close

"education"
```
