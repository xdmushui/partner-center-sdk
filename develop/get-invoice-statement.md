---
title: Get invoice statement
description: Retrieves an invoice statement using the invoice ID.
ms.assetid: 60EAA1F1-AFE2-4FC3-A475-4DBEA58583D1
ms.author: v-thpr
ms.date: 12/15/2017
ms.topic: article
ms.prod: partner-center
ms.technology: partner-center-sdk
---

# Get invoice statement


**Applies To**

-   Partner Center
-   Partner Center operated by 21Vianet
-   Partner Center for Microsoft Cloud Germany
-   Partner Center for Microsoft Cloud for US Government

Retrieves an invoice statement using the invoice ID.

## <span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>Prerequisites


-   Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with App+User credentials only.
-   A valid Invoice ID.

## <span id="C_"></span><span id="c_"></span>C#


To get an invoice statement by ID, use your **IPartner.Invoices** collection and call the **ById()** method using the invoice ID, then call the **Documents()** and **Statement()** methods to access the invoice statement. Finally, call the **Get()** or **GetAsync()** methods.

```CSharp
// IPartner scopedPartnerOperations;
// string selectedInvoiceId;

var invoiceStatement = scopedPartnerOperations.Invoices.ById(selectedInvoiceId).Documents.Statement.Get();
```

**Sample**: [Console test app](console-test-app.md). **Project**: PartnerSDK.FeatureSample **Class**: GetInvoiceStatement.cs 

## <span id="Request"></span><span id="request"></span><span id="REQUEST"></span>REST Request


**Request syntax**

| Method  | Request URI                                                                                       |
|---------|---------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/documents/statement HTTP/1.1  |

 

**URI parameter**

Use the following query parameter to get the invoice statement.

| Name       | Type       | Required | Description                                                                                        |
|------------|------------|----------|----------------------------------------------------------------------------------------------------|
| invoice-id | string     | Yes      | The value is an invoice-id that allows the reseller to filter the results for a given invoice. |

 

**Request headers**

-   See [Headers](headers.md) for more information.

**Request body**

None

**Request example**

```
GET https://api.partnercenter.microsoft.com/v1/invoices/<invoice-id>/documents/statement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 8ac25aa5-9537-4b6d-b782-aa0c8e979e99
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
```

## <span id="Response"></span><span id="response"></span><span id="RESPONSE"></span>REST Response


If successful, this method returns an [InvoiceStatement](invoice.md#invoicestatement) resource in the response body.

**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Error Codes](error-codes.md).

**Response example**

```
HTTP/1.1 200 OK
Content-Length: 219753
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
MS-RequestId: a45e6643-1caf-4429-8f90-07c03d85bc2b
Date: Thu, 24 Mar 2016 05:21:01 GMT

{
    _content	{System.Net.Http.ByteArrayContent}	System.Net.Http.HttpContent {System.Net.Http.ByteArrayContent}
    _content	{byte[219753]}	byte[]
    _headers	{Content-Type: application/pdf Content-Disposition: attachment; filename=Invoice_G000024132.pdf}
}
```

 

 




