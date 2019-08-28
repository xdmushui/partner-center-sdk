---
title: Confirm customer acceptance of Microsoft Customer Agreement (Preview)
description: How to confirm customer acceptance of the Microsoft Customer Agreement. 
ms.date: 08/27/2019
ms.localizationpriority: medium
---

# Confirm customer acceptance of Microsoft Customer Agreement (Preview)

Applies to:

- Partner Center

> [!NOTE]  
> The **Agreement** resource is currently supported by Partner Center in the Microsoft public cloud only. It is not applicable to:
> - Partner Center operated by 21Vianet
> - Partner Center for Microsoft Cloud Germany
> - Partner Center for Microsoft Cloud for US Government

How to confirm customer acceptance of the Microsoft Cloud agreement.

## Prerequisites

- Credentials as described in [Partner Center authentication](./partner-center-authentication.md). This scenario supports app + user authentication only.
- A customer ID (customer-tenant-id).
- Date when customer accepted the Microsoft Customer Agreement.
- Information about the user from the organization who accepted the Microsoft Customer Agreement, including:
  - First name
  - Last name
  - Email address
  - Phone number (optional)

## Examples

To confirm or re-confirm that a customer has accepted the Microsoft Customer Agreement

# [REST](#tab/rest)

## <span id="Request"/><span id="request"/><span id="REQUEST"/>REST Request

1. Retrieve the agreement metadata for the Microsoft Customer Agreement. See [Get agreement metadata for Microsoft Customer Agreement](get-customer-agreement-metadata.md) for details. This step is required to obtain the **templateId** of the Microsoft Customer Agreement.
2. Create a new **Agreement** resource to confirm that a customer has accepted the Microsoft Customer Agreement using the following request syntax.

#### Request syntax

| Method | Request URI                                                                                        |
|--------|----------------------------------------------------------------------------------------------------|
| POST   | [*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/agreements HTTP/1.1 |

#### URI parameter

Use the following query parameter to specify the customer you are confirming.

| Name               | Type | Required | Description                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| customer-tenant-id | GUID | Yes | The value is a GUID formatted **customer-tenant-id** that allows you to specify a customer. |

#### Request headers

- See [Partner Center REST headers](headers.md) for more information.

#### Request body

This table describes the required properties in the request body.

| Name      | Type   | Description                                                                                  |  
|-----------|--------|----------------------------------------------------------------------------------------------|  
| Agreement | object | Details provided by partner to confirm customer acceptance of the Microsoft Customer Agreement. |  

#### Agreement

This table describes the minimum required fields to create an **Agreement** resource.

| Property       | Type   | Description                              |
|----------------|--------|------------------------------------------|
| primaryContact | [Contact](./utility-resources.md#contact) | Information about the user from the customer organization who accepted the Microsoft Cloud Agreement, including:  **firstName**, **lastName**, **email** and **phoneNumber** (optional) |
| dateAgreed     | string in UTC date time format |The date when the customer accepted the agreement. |
| templateId     | string | Unique identifier of the agreement type accepted by the customer. You can obtain the **templateId** for Microsoft Customer Agreement by retrieving the agreement metadata for Microsoft Customer Agreement. See [Get agreement metadata for Microsoft Cloud Agreement](./get-customer-agreement-metadata.md) for details. |
| type           | string | Agreement type accepted by the customer. Use "MicrosoftCloudAgreement" if customer accepted the Microsoft Customer Agreement. |
  
#### Request example

```http
POST https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/agreements HTTP/1.1
Authorization: Bearer <token>
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
{
    "primaryContact": {
        "firstName": "Tania",
        "lastName": "Carr",
        "email": "someone@example.com",
        "phoneNumber": "1234567890"
    },
    "templateId": "117a77b0-9360-443b-8795-c6dedc750cf9",
    "dateAgreed": "2018-06-14T00:00:00.000Z",
    "type": "MicrosoftCustomerAgreement"
}
```

### REST Response

If successful, this method returns an **Agreement** resource.

#### Response success and error codes

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center REST error codes](error-codes.md).

#### Response example

```http
HTTP/1.1 201 Created
Content-Length: 261
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
{
    "userId": "3d6f2c09-eb40-48ca-a4b3-d24c9c007531",
    "primaryContact": {
        "firstName": "Tania",
        "lastName": "Carr",
        "email": "someone@example.com",
        "phoneNumber": "1234567890"
    },
    "templateId": "117a77b0-9360-443b-8795-c6dedc750cf9",
    "dateAgreed": "2018-06-14T00:00:00.000Z",
    "type": "MicrosoftCustomerAgreement"
}
```
