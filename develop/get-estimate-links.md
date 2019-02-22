---
title: Get estimate links
description: How to get a collection of estimate links to query recon line item details.
ms.assetid: 3EE2F67D-8D99-4FAB-A2D6-D33BAD1F324F
ms.date: 02/20/2019
ms.localizationpriority: medium
---

# Get Estimate Links


**Applies To**

- Partner Center
- Partner Center operated by 21Vianet
- Partner Center for Microsoft Cloud Germany
- Partner Center for Microsoft Cloud for US Government

How to get a collection of invoice line item details for the specified invoice.

## <span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>Prerequisites


- Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.
- An invoice identifier. This identifies the invoice for which to retrieve the line items.

## <span id="C_"/><span id="c_"/>C#


To get the line items for the specified invoice, first retrieve the invoice object. To begin, call the [**ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) method to get an interface to invoice operations for the specified invoice. Then call the [**Get**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) or [**GetAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) method to retrieve the invoice object. The invoice object contains all of the information for the specified invoice.

The Provider identifies the source of the unbilled detail information (e.g. All), and the InvoiceLineItemType specifies the type (e.g. UsageLineItem).

The example code that follows uses a foreach loop to process the ReconLineItems collection. A separate collection of line items is retrieved for each InvoiceLineItemType.

To get a collection of line items that correspond to an InvoiceDetail instance, pass the instance's BillingProvider and InvoiceLineItemType to the [**By**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by) method, and then call the [**Get**](#) or [**GetAsync**](#) method to retrieve the associated line items.

Finally, create an enumerator to traverse the collection as shown in the following example.

``` csharp
// IAggregatePartner partnerOperations;
// string curencyCode;

 // all the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
 IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

 // including vNext header
 PartnerService.Instance.AdditionalHeaders = new List<KeyValuePair<string, string>> { new KeyValuePair<string, string>("version", "vNext") };

// read estimate links for currencycode
var estimateLinks = scopedPartnerOperations.Invoices.Estimates.Links.ByCurrency(curencyCode).Get();  
```

For a similar example, see **Sample**: [Console test app](console-test-app.md). **Project**: Partner Center SDK Samples **Class**: GetUnBilledConsumptionReconLineItemsPaging.cs

## <span id="Request"/><span id="request"/><span id="REQUEST"/>REST Request


**Request syntax**
 | Method  | Request URI                                                                                                                                                     |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/estimates/links?currencycode={currencycode} HTTP/1.1                              |                                

**URI parameters**

Use the following URI and query parameters when creating the request.

| Name                   | Type   | Required | Description                                                       |
|------------------------|--------|----------|-------------------------------------------------------------------|
| currencyCode           | string | Yes      | The currency code for the unbilled line items.                    |

 
**Request headers**

- See [Partner Center REST headers](headers.md) for more information.

**Request body**

None.

## <span id="Response"/><span id="response"/><span id="RESPONSE"/>REST Response


If successful, the response contains the collection of line item details.

**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center REST error codes](error-codes.md).

## <span id="Request_Response_Examples"/><span id="request_response_examples"/><span id="REQUEST_RESPONSE_EXAMPLES"/>Request/Response Examples


**Request example 1**

```http
GET https://api.partnercenter.microsoft.com/v1/invoices?currencycode=usd HTTP/1.1
Authorization: Bearer <token> 
Accept: application/json
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
version: vNext
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

**Response example 1**

```http
HTTP/1.1 200 OK
Content-Length: 2484
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CV: bpqyomePDUqrSSYC.0
MS-ServerId: 202010406
Date: Wed, 20 Feb 2019 19:59:27 GMT

{
    "totalCount": 4,
    "items": [
        {
            "title": "Third Party Daily Rated Usage UnBilled",
            "description": "This recon includes third party consumption based unbilled data only.",
            "period": "Current",
            "link": {
                "uri": "/invoices/unbilled/lineitems?provider=external&invoicelineitemtype=usagelineitems&currencycode=usd&period=current&size=2000",
                "method": "GET",
                "headers": []
            }
        },
        {
            "title": "Third Party Daily Rated Usage UnBilled",
            "description": "This recon includes third party consumption based unbilled data only.",
            "period": "Previous",
            "link": {
                "uri": "/invoices/unbilled/lineitems?provider=external&invoicelineitemtype=usagelineitems&currencycode=usd&period=previous&size=2000",
                "method": "GET",
                "headers": []
            }
        },
        {
            "title": "Non-Consumption Unbilled",
            "description": "This recon includes first and third party non-consumption based unbilled data only.",
            "period": "Current",
            "link": {
                "uri": "/invoices/unbilled/lineitems?provider=all&invoicelineitemtype=billinglineitems&currencycode=usd&period=current&size=2000",
                "method": "GET",
                "headers": []
            }
        },
        {
            "title": "Non-Consumption Unbilled",
            "description": "This recon includes first and third party non-consumption based unbilled data only.",
            "period": "Previous",
            "link": {
                "uri": "/invoices/unbilled/lineitems?provider=all&invoicelineitemtype=billinglineitems&currencycode=usd&period=previous&size=2000",
                "method": "GET",
                "headers": []
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}