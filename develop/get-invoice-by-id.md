---
title: Get invoice by ID
description: Retrieves a given invoice using the invoice ID.
ms.assetid: 60EAA1F1-AFE2-4FC3-A475-4DBEA58583D1
ms.author: v-thpr
ms.date: 12/15/2017
ms.topic: article
ms.prod: partner-center
ms.technology: partner-center-sdk
---

# Get invoice by ID


**Applies To**

-   Partner Center
-   Partner Center operated by 21Vianet
-   Partner Center for Microsoft Cloud Germany
-   Partner Center for Microsoft Cloud for US Government

Retrieves a given invoice using the invoice ID.

## <span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>Prerequisites


-   Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with App+User credentials only.
-   A valid Invoice ID.

## <span id="C_"></span><span id="c_"></span>C#


To get an invoice by ID, use your **IPartner.Invoices** collection and call the **ById()** method, then call the **Get()** or **GetAsync()** methods.

```CSharp
// IPartner scopedPartnerOperations;
// var selectedInvoiceId as string;

var invoice = scopedPartnerOperations.Invoices.ById(selectedInvoiceId).Get();
```

**Sample**: [Console test app](console-test-app.md). **Project**: PartnerSDK.FeatureSample **Class**: GetInvoice.cs

## <span id="Request"></span><span id="request"></span><span id="REQUEST"></span>Request


**Request syntax**

| Method  | Request URI                                                                   |
|---------|-------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id} HTTP/1.1 |

 

**URI parameter**

Use the following query parameter to get the invoice.

| Name           | Type       | Required | Description                                                                                      |
|----------------|------------|----------|--------------------------------------------------------------------------------------------------|
| **invoice-id** | **string** | Y        | The value is a **invoice-id** that allows the reseller to filter the results for a given invoice |

 

**Request headers**

-   See [Headers](headers.md) for more information.

**Request body**

None

**Request example**

```
GET https://api.partnercenter.microsoft.com/v1/invoices/<invoice-id> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 8ac25aa5-9537-4b6d-b782-aa0c8e979e99
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
```

## <span id="Response"></span><span id="response"></span><span id="RESPONSE"></span>Response


If successful, this method returns an **Invoice** object in the response.

**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Error Codes](error-codes.md).

**Response example**

```
HTTP/1.1 200 OK
Content-Length: 676
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
MS-RequestId: 8ac25aa5-9537-4b6d-b782-aa0c8e979e99
Date: Thu, 24 Mar 2016 05:22:14 GMT

{
    "id":<invoice-id>,
    "invoiceDate":"2015-08-11T00:00:00",
    "totalCharges":3822.14,
    "paidAmount":0.0,
    "currencyCode":"USD",
    "pdfDownloadLink":<pdfDownloadLink>,
    "invoiceDetails":[{
        "invoiceLineItemType":"billing_line_items",
        "billingProvider":"office",
        "links":{
            "self":{
                "uri":"/invoices/<invoice-id>/lineitems/Office/BillingLineItems",
                "method":"GET",
                "headers":[]
            }
        },
        "attributes":{
            "objectType":"InvoiceDetail"
        }
    }],
    "links":{
        "self":{
            "uri":"/invoices/<invoice-id>",
            "method":"GET",
            "headers":[]
        }
    },
    "attributes":{
        "objectType":"Invoice"
    }
}
```

 

 




