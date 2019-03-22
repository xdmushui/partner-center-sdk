---
title: Update a customer's qualification
description: Updates a customer's qualification, including the address associated with the profile.
ms.date: 11/08/2018
ms.localizationpriority: medium
---

# Update a customer's qualification


**Applies To**

- Partner Center

Updates a customer's qualification.

A partner can update a customer’s qualification to be "Education" or "GovernmentCommunityCloud". Other values, "None" and "Nonprofit", cannot be set.

## <span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>Prerequisites

- Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with App+User credentials only.
- A customer ID (customer-tenant-id).


## <span id="C_"/><span id="c_"/>C#

To update a customer's qualification to "Education", call **[Update](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification.update)** on an existing  [**Customer**](https://docs.microsoft.com/en-us/dotnet/api/microsoft.store.partnercenter.models.customers.customer?view=partnercenter-dotnet-latest).

``` csharp
// CustomerQualification is an enum

var eduCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.Update(CustomerQualification.Education);
```

**Sample**: [Console test app](console-test-app.md). **Project**: PartnerSDK.FeatureSamples **Class**: CustomerQualificationOperations.cs

To update a customer's qualification to **GovernmentCommunityCloud** on an existing customer without a qualification.  The partner is also are required to include the customer's [**ValidationCode**](utility-resources.md#validationcode). 
``` csharp
// CustomerQualification is an enum
// GCC validation is type ValidationCode

var gccCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.Update(CustomerQualification.GovernmentCommunityCloud, gccValidation);
```


## <span id="_Request"/><span id="_request"/><span id="_REQUEST"/> REST Request

**Request syntax**

| Method  | Request URI                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| **PUT** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer_id}/qualification?code={validationCode} HTTP/1.1 |


**URI parameter**

Use the following query parameter to update the qualification.

| Name                   | Type | Required | Description                                                                                                                                            |
|------------------------|------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **customer-tenant-id** | GUID | Yes      | The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller. |
| **validationCode**     | int  | No       | Only needed for Government Community Cloud.                                                                                                            |


**Request headers**

- See [Headers](headers.md) for more information.

**Request body**

The integer value from the [**CustomerQualification**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification) enum.

**Request example**

```http
PUT https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualification?code=<validation-code> HTTP/1.1
Accept: application/json
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68

3
```

## <span id="_Response"/><span id="_response"/><span id="_RESPONSE"/> REST Response

If successful, this method returns updated [**Qualification**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) property in the response body.

**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Error Codes](error-codes.md).

**Response example**

```http
HTTP/1.1 200 OK
Content-Length: 14
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
"governmentcommunitycloud"
```

## Related topics

- [Get a customer's qualification](get-a-customer-s-qualification.md)
- [Get a partner's validation codes](get-a-partner-s-validation-codes.md)