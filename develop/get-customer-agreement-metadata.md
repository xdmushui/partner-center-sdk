---
title: Get agreement metadata for Microsoft Customer Agreement
description: This topic explains how to get agreement metadata for Microsoft Customer Agreement.
ms.date: 8/27/2019
ms.localizationpriority: medium
---

# Get agreement metadata for Microsoft Customer Agreement (Preview)

**Applies To**

- Partner Center

> [!NOTE]
> The **AgreementMetaData** resource is currently supported by Partner Center in the Microsoft public cloud only. It is not applicable to:
> - Partner Center operated by 21Vianet
> - Partner Center for Microsoft Cloud Germany
> - Partner Center for Microsoft Cloud for US Government

## Prerequisites

- Credentials as described in [Partner Center authentication](./partner-center-authentication.md). This scenario supports app + user authentication.

## Examples

To retrieve agreement metadata for Microsoft Customer Agreement

# [REST](#tab/rest)

## <span id="Request"/><span id="request"/><span id="REQUEST"/>REST Request

To retrieve agreement metadata for Microsoft Customer Agreement, create a REST request to retrieve the **AgreementMetaData** collection. Use the *agreementType=MicrosoftCustomerAgreement* URI parameter to scope the result to only Microsoft Customer Agreement only.

**Request syntax**

| Method | Request URI                                                         |
|--------|---------------------------------------------------------------------|
| GET    | [*\{baseURL\}*](partner-center-rest-urls.md)/v1/agreements HTTP/1.1 |

**Request headers**

- See [Partner Center REST headers](headers.md) for more information.

** URI parameters**

| Name                   | Type     | Required | Description                                                             |
|------------------------|----------|----------|-------------------------------------------------------------------------|
| agreementType | string | No | Use this parameter to scope the query response to specific agreement type. The supported values are:<br/> "MicrosoftCloudAgreement" – Includes agreement metadata of type *MicrosoftCloudAgreement* only.<br/> "MicrosoftCustomerAgreement" – Includes agreement metadata of type *MicrosoftCustomerAgreement* only.<br/> "\*" – Returns all agreement metadata.<br/><br/>If the URI parameter isn't specified, the query defaults to "MicrosoftCloudAgreement" to ensure backward compability.<br/><br/>Microsoft may introduce agreement metadata with new agreement type at any point in time. Do not use "\*" unless your code has the necessary logic to handle unexpected agreement types. |


**Request body**

None.

**Request example**

```http
GET https://api.partnercenter.microsoft.com/v1/agreements?agreementType=MicrosoftCustomerAgreement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

If successful, this method returns a collection of **AgreementMetaData** resources in the response body.

**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center REST error codes](error-codes.md).

## <span id="Response"/><span id="response"/><span id="RESPONSE"/>REST Response

**Response example**

```http
HTTP/1.1 200 OK
Content-Length: 620
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
{
    "totalCount": 1,
    "items": [
        {
            "templateId": "117a77b0-9360-443b-8795-c6dedc750cf9",
            "agreementType": "MicrosoftCustomerAgreement",
            "agreementLink": "https://aka.ms/customeragreement",
            "versionRank": 0
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
