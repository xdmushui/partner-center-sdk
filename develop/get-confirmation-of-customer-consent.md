---
title: Get confirmation of customer acceptance of Microsoft Cloud Agreement
description: This topic explains how to get confirmation of customer acceptance of the Microsoft Cloud Agreement. 
ms.date: 8/02/2018
ms.localizationpriority: medium
---

# Get confirmation of customer acceptance of Microsoft Cloud agreement

**Applies To**

-   Partner Center

> [!NOTE]  
> The **Agreement** resource is currently supported by Partner Center in the Microsoft public cloud only. It is not applicable to:
> -   Partner Center operated by 21Vianet
> -   Partner Center for Microsoft Cloud Germany
> -   Partner Center for Microsoft Cloud for US Government

## <span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>Prerequisites

 - If you are using Partner Center SDK, version 1.9 or newer is required. 
 - Credentials as described in [Partner Center authentication](./partner-center-authentication.md). This scenario supports authentication with App+User credentials only. 
 - A customer ID (customer-tenant-id). 

## <span id="Examples"></span><span id="examples"><span id="EXAMPLES"></span>Examples

### C#

To retrieve confirmation of customer acceptance provided previously, use the **IAggregatePartner.Customers** collection and call the **ById** method with the specified customer's ID. Then, get the **Agreements** property, followed by calling the **Get** or **GetAsync** methods.

```csharp
// IAggregatePartner partnerOperations;
// String selectedCustomerId;

var agreements = partnerOperations.Customers.ById(selectedCustomerId).Agreements.Get();
```

**Sample:** Console test app. **Project:** PartnerSDK.FeatureSamples **Class:** GetCustomerAgreement.cs  

### Java 

To retrieve confirmation of customer acceptance provided previously, use the **IAggregatePartner.getCustomers** function and call the **byId** function with the specified customer's identifier. Then, get the **getAgreements** function, followed by calling the **get** function.

```java
// IAggregatePartner partnerOperations;
// String selectedCustomerId;

ResourceCollection<Agreement> agreements = partnerOperations.getCustomers().byId(selectedCustomerId).getAgreements().get();
```

### PowerShell

To retrieve confirmation of customer acceptance provided previously, execute the [**Get-PartnerCustomerAgreement**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerAgreement.md) command.

```powershell
Get-PartnerCustomerAgreement -CustomerId '14876998-c0dc-46e6-9d0c-65a57a6c32ec'
```

## <span id="_Request"></span><span id="_request"></span><span id="_REQUEST"></span>REST Request

To confirm or re-confirm that a customer has accepted the Microsoft Cloud Agreement, create a new **Agreement** resource with the relevant certification information.  

**Request syntax**

| Method | Request URI                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| GET    | [*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/agreements HTTP/1.1 |



**URI parameter**

Use the following query parameter to specify the customer you are confirming.

| Name             | Type | Required | Description                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| CustomerTenantId | GUID | Y        | The value is a GUID formatted **CustomerTenantId** that allows you to specify a customer. |



**Request headers**

-   See [Partner Center REST headers](headers.md) for more information.


**Request body**

None.


**Request example**

```http
GET https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/agreements HTTP/1.1
Authorization: Bearer <token> 
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```


## <span id="Response"></span><span id="response"></span><span id="RESPONSE"></span>REST Response

If successful, this method returns a collection of **Agreement** resources in the response body.


**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center REST error codes](error-codes.md).

**Response example**

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
            "agreementLink":"https://docs.microsoft.com/en-us/partner-center/agreements"
        },
        {
            "primaryContact":
            {
                "firstName":"Tania",
                "lastName":"Carr",
                "email":"SomeEmail@Outlook.com"
                “phoneNumber:"1234567890"
            },
            "templateId":"998b88de-aa99-4388-a42c-1b3517d49490",
            "dateAgreed":"2017-08-01T00:00:00",
            "type":"MicrosoftCloudAgreement",
            "agreementLink":"https://docs.microsoft.com/en-us/partner-center/agreements"
        }
    ]
}
```