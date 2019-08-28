---
title: Get confirmation of customer acceptance of Microsoft Customer Agreement (Preview)
description: This topic explains how to get confirmation of customer acceptance of the Microsoft Customer Agreement. 
ms.date: 8/27/2019
ms.localizationpriority: medium
---

# Get confirmation of customer acceptance of Microsoft Customer Agreement (Preview)

**Applies To**

- Partner Center

> [!NOTE]  
> The **Agreement** resource is currently supported by Partner Center in the Microsoft public cloud only. It is not applicable to:
> - Partner Center operated by 21Vianet
> - Partner Center for Microsoft Cloud Germany
> - Partner Center for Microsoft Cloud for US Government

## Prerequisites

- Credentials as described in [Partner Center authentication](./partner-center-authentication.md). This scenario supports only supports app + user authentication.
- A customer ID (customer-tenant-id).

## Examples

To retrieve confirmation of customer acceptance provided previously

# [REST](#tab/rest)

## <span id="Request"/><span id="request"/><span id="REQUEST"/>REST Request

To retrieve confirmation of customer acceptance for Microsoft Customer Agreement provided previously, create a REST request to retrieve the [Agreements](./agreement-resources.md) collection for a given customer. Use the **agreementType** query parameter to scope the result to Microsoft Customer Agreement only.

**Request syntax**

| Method | Request URI                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| GET    | [*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/agreements?agreementType={agreement-type} HTTP/1.1 |

**URI parameter**

| Name             | Type | Required | Description                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| customer-tenant-id | GUID | Yes | The value is a GUID formatted **CustomerTenantId** that allows you to specify a customer. |
| agreement-type | string | No | Use this parameter to scope the query response to specific agreement type. The supported values are:<br/> "MicrosoftCloudAgreement" – Includes agreement metadata of type *MicrosoftCloudAgreement* only.<br/> "MicrosoftCustomerAgreement" – Includes agreement metadata of type *MicrosoftCustomerAgreement* only.<br/> "\*" – Returns all agreement metadata.<br/><br/>If the URI parameter isn't specified, the query defaults to "MicrosoftCloudAgreement" to ensure backward compability.<br/><br/>Microsoft may introduce agreement metadata with new agreement type at any point in time. Do not use "\*" unless your code has the necessary logic to handle unexpected agreement types. |

**Request headers**

- See [Partner Center REST headers](headers.md) for more information.

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

## <span id="Response"/><span id="response"/><span id="RESPONSE"/>REST Response

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
                "email":"SomeEmail@Outlook.com"
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
