---
title: Get a download link for the Microsoft Customer Agreement template (preview)
description: Get a download link for Microsoft Customer Agreement template.
ms.date: 09/19/2019
ms.localizationpriority: medium
---

# Get a download link for the Microsoft Customer Agreement template (preview)

Applies to:

- Partner Center

The **AgreementDocument** resource is currently supported by Partner Center only in the *Microsoft public cloud*. This resource doesn't apply to:

- Partner Center operated by 21Vianet
- Partner Center for Microsoft Cloud Germany
- Partner Center for Microsoft Cloud for US Government

This article describes how to get a link to download the Microsoft Customer Agreement template, based on the customer's country and language.

## Prerequisites

- If you are using the Partner Center .NET SDK, version 1.14 or newer is required.
- Credentials as described in [Partner Center authentication](./partner-center-authentication.md). This scenario supports App+User authentication.
- The country to which the Microsoft Customer Agreement template applies.
- The language in which the Microsoft Customer Agreement template should be localized.

# [.NET](#tab/dotnet)

To retrieve a link to download the Microsoft Customer Agreement template:

1. Retrieve the agreement metadata for the Microsoft Customer Agreement. You must obtain the **templateId** of the Microsoft Customer Agreement. For more information, see [Get agreement metadata for Microsoft Customer Agreement](get-customer-agreement-metadata.md).

```csharp
// IAggregatePartner partnerOperations;

string agreementType = "MicrosoftCustomerAgreement";

AgreementMetaData microsoftCustomerAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get();.Items.Single();
```

2. Use the IAggregatePartner.AgreementTemplates collection and call the ById method with the specified **templateId** of the Microsoft Customer Agreement. Then, get the Document property, followed by calling the ByCountry method with the specified country, followed by calling the ByLanguage method with the specific language. Finally, call the **Get** or **GetAsync** method.

```csharp
// IAggregatePartner partnerOperations;

var agreementDocument = partnerOperations.AgreementTemplates.ById(microsoftCustomerAgreementDetails.TemplateId).Document.ByCountry("US").ByLanguage("en-US").Get();
```

A complete sample can be found in the [GetAgreementDocument](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDocument.cs) class from the [console test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) project.

# [REST](#tab/rest)

## REST request

To retrieve a link to download the Microsoft Customer Agreement template:

1. Retrieve the agreement metadata for the Microsoft Customer Agreement. You must obtain the **templateId** of the Microsoft Customer Agreement. For more information, see [Get agreement metadata for Microsoft Customer Agreement](get-customer-agreement-metadata.md).
2. Create a REST request to fetch an [**AgreementDocument** resource](./agreement-document-resources.md). For an example, see the [request syntax](#request-syntax) example. You must specify the following information:
    - The **templateId** of the Microsoft Customer Agreement,
    - The country to which the Microsoft Customer Agreement template applies.
    - The language in which the Microsoft Customer Agreement template should be localized.

### Request syntax

Use the following request syntax for this resource:

| Method | Request URI |
|--------|---------------------------------------------------------------------|
| GET | [*\{baseURL\}*](partner-center-rest-urls.md)/v1/agreementtemplates/{agreement-template-id}/document?language={language}&country={country} HTTP/1.1 |

### URI parameters

You can use the following URI parameters with your request:

| Name                   | Type   | Required | Description                                 |
|------------------------|--------|----------|---------------------------------------------|
| agreement-template-id  | string | Yes      | Unique identifier of the agreement type. You can obtain the templateId for Microsoft Customer Agreement by retrieving the agreement metadata for Microsoft Customer Agreement. For more information, see [Get agreement metadata for Microsoft Customer Agreement](./get-customer-agreement-metadata.md). |
| country                | string | No       | Indicates the country to which the agreement template applies. The query defaults to *US* if a parameter isn't specified. For a list of supported country codes, please refer to [List of supported countries and languages](#list-of-supported-countries-and-languages).|
| language               | string | No       | Indicates the language in which the agreement template should be localized. The query defaults to *en-US* if a parameter isn't specified. For list of supported country codes, please refer to [List of supported countries and languages](#list-of-supported-countries-and-languages).|

### Request headers

For more information, see [Partner Center REST headers](headers.md).

### Request body

None.

### Request example

```http
GET https://api.partnercenter.microsoft.com/v1/agreementtemplates/117a77b0-9360-443b-8795-c6dedc750cf9/document?language=en-US&country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## REST response

If successful, this method returns an [**AgreementDocument** resource](./agreement-document-resources.md) in the response body.

The resource has a **downloadUri** property, which contains a URL string that can be used to download the agreement template. A different link is returned each time you make a query. This link expires after five minutes.

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
    "displayUri":"https://wopihost.int.l2o.microsoft.com/v1/officehost/agreement/files/Preview...",
    "downloadUri":"https://l2oagreementintbn2.blob.core.windows.net/agreementscontainer/Preview...",
    "language":"en-US",
    "country":"US"
}
```

## List of supported countries and languages

*This list of supported countries and languages is still being finalized.* For the purposes of previewing the API, you can use the following countries and languages at this time:


| Country                   | Country code   | Supported language code(s) |
|------------------------|--------|----------|
| United States of America | US | en-US |
