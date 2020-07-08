---
title: Get confirmation of customer acceptance of Microsoft Customer Agreement
description: This article explains how to get confirmation of customer acceptance of the Microsoft Customer Agreement.
ms.date: 09/19/2019
ms.service: partner-dashboard
ms.subservice:  partnercenter-sdk
ms.localizationpriority: medium
author: amitravat
ms.author: amrava
---

# Get confirmation of customer acceptance of Microsoft Customer Agreement

**Applies to:**

- Partner Center

The **Agreement** resource is currently supported by Partner Center only in the *Microsoft public cloud*. This resource doesn't apply to:

- Partner Center operated by 21Vianet
- Partner Center for Microsoft Cloud Germany
- Partner Center for Microsoft Cloud for US Government

This article explains how you can retrieve confirmation(s) of a customer's acceptance of the Microsoft Customer Agreement.

## Prerequisites

- If you are using the Partner Center .NET SDK, version 1.14 or newer is required.

- Credentials as described in [Partner Center authentication](./partner-center-authentication.md). This scenario only supports App+User authentication.

- A customer ID (`customer-tenant-id`). If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard). Select **CSP** from the Partner Center menu, followed by **Customers**. Select the customer from the customer list, then select **Account**. On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section. The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).

## .NET

To retrieve confirmation(s) of customer acceptance that was previously provided:

- Use the **IAggregatePartner.Customers** collection and call **ById** method with the specified customer identifier.

- Fetch the **Agreements** property and filter the results to Microsoft Customer Agreement by calling **ByAgreementType** method.

- Call **Get** or **GetAsync** method.

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

string agreementType = "MicrosoftCustomerAgreement";

var customerAgreements = partnerOperations.Customers.ById(selectedCustomerId).Agreements.ByAgreementType(agreementType).Get();
```

A complete sample can be found in the [GetCustomerAgreements](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetCustomerAgreements.cs) class from the [console test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) project.

## REST request

To retrieve confirmation of customer acceptance that was previously provided:

1. Create a REST request to retrieve the [Agreements](./agreement-resources.md) collection for the customer.

2. Use the **agreementType** query parameter to scope the results to only the Microsoft Customer Agreement.

### Request syntax

Use the following request syntax:

| Method | Request URI                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| GET    | [*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/agreements?agreementType={agreement-type} HTTP/1.1 |

#### URI parameters

You can use the following URI parameters with your request:

| Name             | Type | Required | Description                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| customer-tenant-id | GUID | Yes | The value is a GUID formatted **CustomerTenantId** that allows you to specify a customer. |
| agreement-type | string | No | This parameter returns all agreement metadata. Use this parameter to scope the query response to specific agreement type. The supported values are: <ul><li>**MicrosoftCloudAgreement** that only includes agreement metadata of the type *MicrosoftCloudAgreement*.</li><li>**MicrosoftCustomerAgreement** that only includes agreement metadata of the type *MicrosoftCustomerAgreement*.</li><li>**\*** that returns all agreement metadata. (Don't use **\*** unless your code has the necessary logic to handle unexpected agreement types.)</li></ul> If the URI parameter isn't specified, the query defaults to **MicrosoftCloudAgreement** for backward compatibility. Microsoft may introduce agreement metadata with new agreement types at any time.  |

### Request headers

For more information, see [Partner Center REST headers](headers.md).

### Request body

None.

### Request example

```http
GET https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/agreements?agreementType=MicrosoftCustomerAgreement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## REST response

If successful, this method returns a collection of **Agreement** resources in the response body.

### Response success and error codes

Each response comes with an HTTP status code that indicates success or failure and additional debugging information.

Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center REST error codes](error-codes.md).

### Response example

```http
HTTP/1.1 200 OK
Content-Length: 620
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
{
    "totalCount": 2,
    "items":
    [
        {
            "primaryContact":
            {
                "firstName":"Tania",
                "lastName":"Carr",
                "email":"SomeEmail@example.com"
                "phoneNumber":"1234567890"
            },
            "templateId":"117a77b0-9360-443b-8795-c6dedc750cf9",
            "dateAgreed":"2019-08-26T00:00:00",
            "type":"MicrosoftCustomerAgreement",
            "agreementLink":"https://aka.ms/customeragreement"
        },
        {
            "primaryContact":
            {
                "firstName":"Tania",
                "lastName":"Carr",
                "email":"SomeEmail@example.com"
                "phoneNumber:"1234567890"
            },
            "templateId":"117a77b0-9360-443b-8795-c6dedc750cf9",
            "dateAgreed":"2019-08-27T00:00:00",
            "type":"MicrosoftCustomerAgreement",
            "agreementLink":"https://aka.ms/customeragreement"
        }
    ]
}
```
