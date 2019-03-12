---
title: Get invoice estimate links
description: How to get a collection of estimate links to query recon line item details.
ms.date: 02/20/2019
ms.localizationpriority: medium
---

# Get invoice estimate links


**Applies To**

- Partner Center
- Partner Center operated by 21Vianet
- Partner Center for Microsoft Cloud Germany
- Partner Center for Microsoft Cloud for US Government

How to get estimate (unbilled) links for invoice line items.

## <span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>Prerequisites


- Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.
- An invoice identifier. This identifies the invoice for which to retrieve the line items.

## <span id="C_"/><span id="c_"/>C#

To get the estimate (unbilled) links that helps to query unbilled line items for first and third party products for given currency.
The response contains the estimate self links per period (i.e. Current and Previous month).

``` csharp
// IAggregatePartner partnerOperations;
// string curencyCode;

 // all the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
 IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

// read estimate links for currencycode
var estimateLinks = scopedPartnerOperations.Invoices.Estimates.Links.ByCurrency(curencyCode).Get();  
```

For a similar example, see **Sample**: [Console test app](console-test-app.md). **Project**: Partner Center SDK Samples **Class**: GetEstimatesLinks.cs

## <span id="Request"/><span id="request"/><span id="REQUEST"/>REST Request

**Request syntax**  

| Method  | Request URI                                                                                                 |
|---------|-------------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/estimates/links?currencycode={currencycode} HTTP/1.1 |

**URI parameters**

Use the following URI and query parameters when creating the request.

| Name                   | Type   | Required | Description                                                       |
|------------------------|--------|----------|-------------------------------------------------------------------|
| currencyCode           | string | Yes      | The currency code for the unbilled line items.                    |

 
**Request headers**

- See [Partner Center REST headers](headers.md) for more information.

**Request body**

None.

**Request example**

```http
GET https://api.partnercenter.microsoft.com/v1/invoices?currencycode=usd HTTP/1.1
Authorization: Bearer <token> 
Accept: application/json
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

## <span id="Response"/><span id="response"/><span id="RESPONSE"/>REST Response

If successful, the response contains the links to retrieve unbilled estimates.

**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center REST error codes](error-codes.md).

**Response example**

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
            "title": "Unbilled Recon",
            "description": "This recon includes first and third party unbilled data only.",
            "period": "Current",
            "link": {
                "uri": "/invoices/unbilled/lineitems?provider=all&invoicelineitemtype=billinglineitems&currencycode=usd&period=current&size=2000",
                "method": "GET",
                "headers": []
            }
        },
        {
            "title": "Unbilled Recon",
            "description": "This recon includes first and third party unbilled data only.",
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
```
