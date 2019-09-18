---
title: Get invoice's unbilled reconciliation line items (AKA open billing line items)
description: How to get a collection of unbilled reconciliation line item details for specified period.
ms.date: 09/10/2019
ms.localizationpriority: medium
---

# Get invoice's unbilled reconciliation line items

Applies to:

- Partner Center
- Partner Center operated by 21Vianet
- Partner Center for Microsoft Cloud Germany
- Partner Center for Microsoft Cloud for US Government

How to get a collection of unbilled invoice line item details.

>[!NOTE]
>Please use **“onetime”** to query all onetime invoice line item line items, instead of **“all”** (to be deprecated). Alternatively, follow the links in estimate links call.

## Prerequisites

- Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.
- An invoice identifier. This identifies the invoice for which to retrieve the line items.

## C\#

To get the line items for the specified invoice, retrieve the invoice object:

1. Call the [**ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) method to get an interface to invoice operations for the specified invoice.
2. Call the [**Get**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) or [**GetAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) method to retrieve the invoice object.

The invoice object contains all of the information for the specified invoice:

- **Provider** identifies the source of the unbilled detail information (for example, **OneTime**).
- **InvoiceLineItemType** specifies the type (for example, **BillingLineItem**).

To get a collection of line items that correspond to an **InvoiceDetail** instance:

1. Pass the instance's BillingProvider and InvoiceLineItemType to the [**By**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by) method
2. Call the [**Get**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) or [**GetAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) method to retrieve the associated line items.
3. Create an enumerator to traverse the collection. For an example, see the following sample code.

The following sample code uses a `foreach` loop to process the **InvoiceLineItems** collection. A separate collection of line items is retrieved for each **InvoiceLineItemType**.

``` csharp
// IAggregatePartner partnerOperations;
// string currencyCode;
// string period;
// int pageMaxSizeReconLineItems = 2000;

// all the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

var seekBasedResourceCollection = scopedPartnerOperations.Invoices.ById("unbilled").By("onetime", "billinglineitems", currencyCode, period, pageMaxSizeReconLineItems).Get();

var fetchNext = true;

ConsoleKeyInfo keyInfo;

var itemNumber = 1;
while (fetchNext)
{
    Console.Out.WriteLine("\tLine line items count: " + seekBasedResourceCollection.Items.Count());

    seekBasedResourceCollection.Items.ToList().ForEach(item =>
    {
        // Instance of type OneTimeInvoiceLineItem
        if (item is OneTimeInvoiceLineItem)
        {
            Type t = typeof(OneTimeInvoiceLineItem);
            PropertyInfo[] properties = t.GetProperties();

            foreach (PropertyInfo property in properties)
            {
                // Insert code here to work with the line item properties
            }
        }
        itemNumber++;
    });

    Console.Out.WriteLine("\tPress any key to fetch next data. Press the Escape (Esc) key to quit: \n");
    keyInfo = Console.ReadKey();

    if (keyInfo.Key == ConsoleKey.Escape)
    {
        break;
    }

    fetchNext = !string.IsNullOrWhiteSpace(seekBasedResourceCollection.ContinuationToken);

    if (fetchNext)
    {
        if (seekBasedResourceCollection.Links.Next.Headers != null && seekBasedResourceCollection.Links.Next.Headers.Any())
        {
            seekBasedResourceCollection = scopedPartnerOperations.Invoices.ById("unbilled").By("onetime", "billinglineitems", currencyCode, period, pageMaxSizeReconLineItems).Seek(seekBasedResourceCollection.ContinuationToken, SeekOperation.Next);
        }
    }
}
```

For a similar example, see:

- [Console test app](console-test-app.md)
- Project: Partner Center SDK Samples
- Class: GetUnBilledReconLineItemsPaging.cs

## REST request

### Request syntax

Use the first syntax to return a full list of every line item for the given invoice. For large invoices, use the second syntax with a specified size and 0-based offset to return a paged list of line items. Use the third syntax to get the next page of recon line items using `seekOperation = "Next"`.

 | Method  | Request URI                                                                                                                                                     |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=billinglineitems&currencycode={currencycode}&period={period} HTTP/1.1                              |
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=billinglineitems&currencycode={currencycode}&period={period}&size={size} HTTP/1.1  |
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=billinglineitems&currencycode={currencycode}&period={period}&size={size}&seekOperation=Next                               |

#### URI parameters

Use the following URI and query parameters when creating the request.

| Name                   | Type   | Required | Description                                                                     |
|------------------------|--------|----------|---------------------------------------------------------------------------------|
| invoice-id             | string | Yes      | A string that identifies the invoice. Use ‘unbilled’ to get unbilled estimates. |
| provider               | string | Yes      | The provider: "OneTime".                                                |
| invoice-line-item-type | string | Yes      | The type of invoice detail: "BillingLineItems".               |
| currencyCode           | string | Yes      | The currency code for the unbilled line items.                                  |
| period                 | string | Yes      | The period for unbilled recon. example: current, previous.                      |
| size                   | number | No       | The maximum number of items to return. Default size is 2000                     |
| seekOperation          | string | No       | Set seekOperation=Next to get the next page of recon line items.                |

### Request headers

See [Partner Center REST headers](headers.md) for more information.

### Request body

None.

## REST Response

If successful, the response contains the collection of line item details.

> [!NOTE]
> For the line item ChargeType, the value "Purchase" is mapped to "New" and the value "Refund" is mapped to "Cancel".

### Response success and error codes

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center REST error codes](error-codes.md).

## REST request and response examples

### Request and response example 1

- Provider: **OneTime**
- InvoiceLineItemType: **BillingLineItems**
- Period: **Previous**

#### Request example 1

```http
GET https://api.partnercenter.microsoft.com/v1//invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=billinglineitems&currencycode=usd&period=previous&size=2000 HTTP/1.1
Authorization: Bearer <token> 
Accept: application/json
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

#### Response example 1

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
    "totalCount": 2,
    "items": [
        {
            "partnerId": "0c924e8d-4852-4692-a4d7-7dd0dc09ad80",
            "customerId": "org:d7f565f5-5367-492f-a465-9e2057c5e3c3",
            "customerName": "TEST_TEST_GTM1",
            "customerDomainName": "TESTTESTGTM1.ccsctp.net",
            "customerCountry": "US",
            "invoiceNumber": "",
            "mpnId": "1234567",
            "resellerMpnId": 0,
            "orderId": "HJVtMZMkgQ2miuCiNv0RSr51zQDans0m1",
            "orderDate": "2019-02-04T17:59:52.9460102Z",
            "productId": "DZH318Z0BXWC",
            "skuId": "0002",
            "availabilityId": "DZH318Z0BP8B",
            "productName": "Test WAF-as-a-Service",
            "skuName": "Test WaaS - Medium Plan",
            "chargeType": "New",
            "unitPrice": 820,
            "effectiveUnitPrice": 820,
            "unitType": "",
            "quantity": 1,
            "subtotal": 820,
            "taxTotal": 0,
            "totalForCustomer": 0,
            "currency": "USD",
            "publisherName": "Test Networks, Inc.",
            "publisherId": "21223810",
            "subscriptionDescription": "",
            "subscriptionId": "12345678-9cf0-4a1f-9514-7fcc7fe9d1fe",
            "chargeStartDate": "2019-02-04T09:22:40.1767993-08:00",
            "chargeEndDate": "2019-03-03T09:22:40.1767993-08:00",
            "termAndBillingCycle": "1 Month Subscription",
            "alternateId": "123456ad566",
            "priceAdjustmentDescription": "[\"15.0% Partner earned credit for services managed\"]",
            "discountDetails": "",
            "pricingCurrency": "USD",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-08-01T00:00:00Z",
            "billableQuantity": 3.1618,

            "attributes": {
                "objectType": "OneTimeInvoiceLineItem"
            }
        },
        {
            "partnerId": "0c924e8d-4852-4692-a4d7-7dd0dc09ad80",
            "customerId": "org:d7f565f5-5367-492f-a465-9e2057c5e3c3",
            "customerName": "TEST_TEST_GTM1",
            "customerDomainName": "TESTTESTGTM1.ccsctp.net",
            "customerCountry": "US",
            "invoiceNumber": "",
            "mpnId": "1234567",
            "resellerMpnId": 0,
            "orderId": "Oi2kwDPEOyGEFUkESk3QR4XSxcpvwp1x1",
            "orderDate": "2019-02-04T17:59:53.1628078Z",
            "productId": "DZH318Z0BXWC",
            "skuId": "0005",
            "availabilityId": "DZH318Z0BH9R",
            "productName": "Test WAF-as-a-Service",
            "skuName": "Test WaaS - Large Plan",
            "chargeType": "New",
            "unitPrice": 2598,
            "effectiveUnitPrice": 2598,
            "unitType": "",
            "quantity": 1,
            "subtotal": 2598,
            "taxTotal": 0,
            "totalForCustomer": 0,
            "currency": "USD",
            "publisherName": "Test Networks, Inc.",
            "publisherId": "21223810",
            "subscriptionDescription": "",
            "subscriptionId": "12345678-28db-48c2-8c30-04d7c9455746",
            "chargeStartDate": "2019-02-04T09:22:34.6455294-08:00",
            "chargeEndDate": "2019-03-03T09:22:34.6455294-08:00",
            "termAndBillingCycle": "1 Month Subscription",
            "alternateId": "123456ad566",
            "priceAdjustmentDescription": "[\"15.0% Partner earned credit for services managed\",\"100.0% Tier 1 Discount\"]",
            "discountDetails": "",
            "pricingCurrency": "USD",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-08-01T00:00:00Z",
            "billableQuantity": 0.737083,
           
            "attributes": {
                "objectType": "OneTimeInvoiceLineItem"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=billinglineitems&currencycode=usd&period=previous&size=2000",
            "method": "GET",
            "headers": []
        },
        "next": {
            "uri": "/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=billinglineitems&currencycode=usd&period=previous&size=2000&seekOperation=Next",
            "method": "GET",
            "headers": [
                {
                    "key": "MS-ContinuationToken",
                    "value": "AQAAAA=="
                }
            ]
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

### Request and response example 2

- Provider: **OneTime**
- InvoiceLineItemType: **BillingLineItems**
- Period: **Previous**
- SeekOperation: **Next**

#### Request example 2

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/unbilled/lineitems?provider=onetime&invoiceLineItemType=billinglineitems&currencyCode=usd&period=previous&size=2000&seekoperation=next HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-ContinuationToken: d19617b8-fbe5-4684-a5d8-0230972fb0cf,0705c4a9-39f7-4261-ba6d-53e24a9ce47d_a4ayc/80/OGda4BO/1o/V0etpOqiLx1JwB5S3beHW0s=,0d81c700-98b4-4b13-9129-ffd5620f72e7
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

#### Response example 2

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
    "totalCount": 1,
    "items": [
        {
            "partnerId": "0c924e8d-4852-4692-a4d7-7dd0dc09ad80",
            "customerId": "org:d7f565f5-5367-492f-a465-9e2057c5e3c3",
            "customerName": "TEST_TEST_GTM1",
            "customerDomainName": "TESTTESTGTM1.ccsctp.net",
            "customerCountry": "US",
            "invoiceNumber": "",
            "mpnId": "1234567",
            "resellerMpnId": 0,
            "orderId": "Oi2kwDPEOyGEFUkESk3QR4XSxcpvwp1x1",
            "orderDate": "2019-02-04T17:59:53.1628078Z",
            "productId": "DZH318Z0BXWC",
            "skuId": "0005",
            "availabilityId": "DZH318Z0BH9R",
            "productName": "Test WAF-as-a-Service",
            "skuName": "Test WaaS - Large Plan",
            "chargeType": "New",
            "unitPrice": 2598,
            "effectiveUnitPrice": 2598,
            "unitType": "",
            "quantity": 1,
            "subtotal": 2598,
            "taxTotal": 0,
            "totalForCustomer": 0,
            "currency": "USD",
            "publisherName": "Test Networks, Inc.",
            "publisherId": "21223810",
            "subscriptionDescription": "",
            "subscriptionId": "12345678-28db-48c2-8c30-04d7c9455746",
            "chargeStartDate": "2019-02-04T09:22:34.6455294-08:00",
            "chargeEndDate": "2019-03-03T09:22:34.6455294-08:00",
            "termAndBillingCycle": "1 Month Subscription",
            "alternateId": "123456ad566",
            "discountDetails": "",            
            "attributes": {
                "objectType": "OneTimeInvoiceLineItem"
            }
        }
    ],
    "links": {
        "self": {
             "uri": "/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=billinglineitems&currencycode=usd&period=previous&size=2000",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
