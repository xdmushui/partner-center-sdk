---
title: Get confirmation of customer acceptance of Microsoft Cloud Agreement
description: This article explains how to get confirmation of customer acceptance of the Microsoft Cloud Agreement.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice:  partnercenter-sdk
ms.localizationpriority: medium
aauthor: khakiali
ms.author: alikhaki
---

# Get confirmation of customer acceptance of Microsoft Cloud Agreement

**Applies To**

- Partner Center

> [!NOTE]
> The **Agreement** resource is currently supported by Partner Center in the Microsoft public cloud only. It isn't applicable to:
>
> - Partner Center operated by 21Vianet
> - Partner Center for Microsoft Cloud Germany
> - Partner Center for Microsoft Cloud for US Government

## Prerequisites

- If you are using the Partner Center .NET SDK, version 1.9 or newer is required.

- If you are using the Partner Center Java SDK, version 1.8 or newer is required.

- Credentials as described in [Partner Center authentication](./partner-center-authentication.md). This scenario supports only supports app + user authentication.

- A customer ID (`customer-tenant-id`). If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard). Select **CSP** from the Partner Center menu, followed by **Customers**. Select the customer from the customer list, then select **Account**. On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section. The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).

## .NET (version 1.4 or newer)

To retrieve confirmation(s) of customer acceptance that was previously provided:

- Use the **IAggregatePartner.Customers** collection and call **ById** method with the specified customer identifier.

- Fetch the **Agreements** property and filter the results to Microsoft Cloud Agreement by calling **ByAgreementType** method.

- Call **Get** or **GetAsync** method.

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

string agreementType = "MicrosoftCloudAgreement";

var cloudAgreements = partnerOperations.Customers.ById(selectedCustomerId).Agreements.ByAgreementType(agreementType).Get();
```

A complete sample can be found in the [GetCustomerAgreements](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetCustomerAgreements.cs) class from the [console test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) project.

## .NET (version 1.9 - 1.13)

To retrieve confirmation of customer acceptance provided previously:

Use the **IAggregatePartner.Customers** collection and call the **ById** method with the specified customer's identifier. Then, get the **Agreements** property, followed by calling the **Get** or **GetAsync** methods.

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var agreements = partnerOperations.Customers.ById(selectedCustomerId).Agreements.Get();
```

## Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

To retrieve confirmation of customer acceptance provided previously:

Use the **IAggregatePartner.getCustomers** function and call the **byId** function with the specified customer's identifier. Then, get the **getAgreements** function, followed by calling the **get** function.

```java
// IAggregatePartner partnerOperations;
// String selectedCustomerId;

ResourceCollection<Agreement> agreements = partnerOperations.getCustomers().byId(selectedCustomerId).getAgreements().get();
```

A complete sample can be found in the [GetCustomerAgreements](https://github.com/microsoft/Partner-Center-Java-Samples/blob/master/sdk/src/main/java/com/microsoft/store/partnercenter/samples/agreements/GetCustomerAgreements.java) class from the [console test app](https://github.com/Microsoft/Partner-Center-Java-Samples) project.

## PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

To retrieve confirmation of customer acceptance provided previously:

Use the [**Get-PartnerCustomerAgreement**](https://docs.microsoft.com/powershell/module/partnercenter/get-partnercustomeragreement) command.

```powershell
Get-PartnerCustomerAgreement -CustomerId '14876998-c0dc-46e6-9d0c-65a57a6c32ec'
```

## REST request

To retrieve confirmation of customer acceptance provided previously, see the following instructions.

Create a new **Agreement** resource with the relevant certification information.

### Request syntax

| Method | Request URI                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| GET    | [*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/agreements HTTP/1.1 |

#### URI parameter

Use the following query parameter to specify the customer you are confirming.

| Name             | Type | Required | Description                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| CustomerTenantId | GUID | Y        | The value is a GUID formatted **CustomerTenantId** that allows you to specify a customer. |

### Request headers

For more information, see [Partner Center REST headers](headers.md).

### Request body

None.

### Request example

```http
GET https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/agreements HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## REST response

If successful, this method returns a collection of **Agreement** resources in the response body.

### Response success and error codes

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center REST error codes](error-codes.md).

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
                "email":"SomeEmail@Outlook.com"
                "phoneNumber":"1234567890"
            },
            "templateId":"998b88de-aa99-4388-a42c-1b3517d49490",
            "dateAgreed":"2018-07-28T00:00:00",
            "type":"MicrosoftCloudAgreement",
            "agreementLink":"https://docs.microsoft.com/partner-center/agreements"
        },
        {
            "primaryContact":
            {
                "firstName":"Tania",
                "lastName":"Carr",
                "email":"SomeEmail@Outlook.com"
                "phoneNumber:"1234567890"
            },
            "templateId":"998b88de-aa99-4388-a42c-1b3517d49490",
            "dateAgreed":"2017-08-01T00:00:00",
            "type":"MicrosoftCloudAgreement",
            "agreementLink":"https://docs.microsoft.com/partner-center/agreements"
        }
    ]
}
```
