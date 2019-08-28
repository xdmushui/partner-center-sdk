---
title: Get a download link for Microsoft Customer Agreement template (Preview)
description: This topic explains how to get a download link for Microsoft Customer Agreement template.
ms.date: 8/27/2019
ms.localizationpriority: medium
---

# Get a download link for Microsoft Customer Agreement template (Preview)

**Applies To**

- Partner Center

> [!NOTE]
> The **AgreementDocument** resource is currently supported by Partner Center in the Microsoft public cloud only. It is not applicable to:
> - Partner Center operated by 21Vianet
> - Partner Center for Microsoft Cloud Germany
> - Partner Center for Microsoft Cloud for US Government

Retrieve a link to download the Microsoft Customer Agreement template based on customer's country and language.

## Prerequisites

- Credentials as described in [Partner Center authentication](./partner-center-authentication.md). This scenario supports app + user authentication.
- Country for which the Microsoft Customer Agreement template is applicable to.
- Language for which the Microsoft Customer Agreement template should be localized in.

## Examples

To retrieve a link to download the Microsoft Customer Agreement template based on customer's country and language

# [REST](#tab/rest)

## <span id="Request"/><span id="request"/><span id="REQUEST"/>REST Request

1. Retrieve the agreement metadata for the Microsoft Customer Agreement. See [Get agreement metadata for Microsoft Customer Agreement](get-customer-agreement-metadata.md) for details. This step is required to obtain the **templateId** of the Microsoft Customer Agreement.
2. Create a REST request to fetch an **AgreementDocument** resource, specifying the following:
    - The **templateId** of the Microsoft Customer Agreement,
    - The country for which the template is applicable to, and
    - The language for which the template should be localized in.

**Request syntax**

| Method | Request URI |
|--------|---------------------------------------------------------------------|
| GET | [*\{baseURL\}*](partner-center-rest-urls.md)/v1/agreementtemplates/{agreement-template-id}/document?language={language}&country={country} HTTP/1.1 |

**URI parameters**

| Name                   | Type   | Required | Description                                 |
|------------------------|--------|----------|---------------------------------------------|
| agreement-template-id  | string | No       | Unique identifier of the agreement type. You can obtain the templateId for Microsoft Customer Agreement by retrieving the agreement metadata for Microsoft Customer Agreement. See [Get agreement metadata for Microsoft Customer Agreement](./get-customer-agreement-metadata.md) for details. |
| country                | string | No       | Indicates what country for which the requested agreement template is applicable to. |
| language               | string | No       | Indicates what language the requested agreement template should be localized in. |

**Request headers**

- See [Partner Center REST headers](headers.md) for more information.

**Request body**

None.

**Request example**

```http
GET https://api.partnercenter.microsoft.com/v1/agreementtemplates/117a77b0-9360-443b-8795-c6dedc750cf9/document?language=en-US&country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <span id="Response"/><span id="response"/><span id="RESPONSE"/>REST Response

If successful, this method returns an [AgreementDocument](./agreement-document-resources.md) resource in the response body. The resource has a **downloadUri** property which contains a URL string that can be used to download the agreement template. Note the following:
 - A different link is returned each time you make a query.
 - The link will expire after five minutes.

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
    "displayUri":"https://wopihost.int.l2o.microsoft.com/v1/officehost/agreement/files/Preview...",
    "downloadUri":"https://l2oagreementintbn2.blob.core.windows.net/agreementscontainer/Preview...",
    "language":"en-US",
    "country":"US"
}
```
