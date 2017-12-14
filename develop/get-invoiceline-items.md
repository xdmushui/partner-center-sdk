---
title: Get invoice line items
description: How to get a collection of invoice line item details for the specified invoice.
ms.assetid: 3EE2F67D-8D99-4FAB-A2D6-D33BAD1F324F
ms.author: v-thpr
ms.date: 12/15/2017
ms.topic: article
ms.prod: partner-center
ms.technology: partner-center-sdk
---

# Get invoice line items


**Applies To**

-   Partner Center
-   Partner Center operated by 21Vianet
-   Partner Center for Microsoft Cloud Germany
-   Partner Center for Microsoft Cloud for US Government

How to get a collection of invoice line item details for the specified invoice.

## <span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>Prerequisites


-   Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.
-   An invoice identifier. This identifies the invoice for which to retrieve the line items.

## <span id="C_"></span><span id="c_"></span>C#


To get the line items for the specified invoice, first retrieve the invoice object. To begin, call the [**ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) method to get an interface to invoice operations for the specified invoice. Then call the [**Get**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) or [**GetAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) method to retrieve the invoice object. The invoice object contains all of the information for the specified invoice.

Next, use the invoice object's [**InvoiceDetails**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.invoices.invoice.invoicedetails) property to get access to a collection of [**InvoiceDetail**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.invoices.invoicedetail) objects, each of which contains a [**BillingProvider**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.invoices.invoicedetail.billingprovider) and an [**InvoiceLineItemType**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.invoices.invoicedetail.invoicelineitemtype). The BillingProvider identifies the source of the invoice detail information (e.g. Office, Azure), and the InvoiceLineItemType specifies the type (e.g. UsageLineItem).

The example code that follows uses a foreach loop to process the InvoiceDetails collection. A separate collection of line items is retrieved for each InvoiceDetail instance.

To get a collection of line items that correspond to an InvoiceDetail instance, pass the instance's BillingProvider and InvoiceLineItemType to the [**By**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by) method, and then call the [**Get**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicelineitemcollection.get) or [**GetAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicelineitemcollection.getasync) method to retrieve the associated line items.

Finally, create an enumerator to traverse the collection as shown in the following example.

```
// IAggregatePartner partnerOperations;
// int invoicePageSize;
// string invoiceId;

// Retrieve the invoice. 
var invoiceOperations = partnerOperations.Invoices.ById(invoiceId);
var invoice = invoiceOperations.Get();

foreach (var invoiceDetail in invoice.InvoiceDetails)
{
    Console.WriteLine(string.Format("Getting invoice line item for product {0} and line item type {1}", 
        invoiceDetail.BillingProvider, 
        invoiceDetail.InvoiceLineItemType));

    // Is this an unpaged or paged request?
    bool isUnPaged = (this.invoicePageSize <= 0);

    // If the scenario is unpaged, get all the invoice line items, otherwise get the first page.
    var invoiceLineItemsCollection = 
        (isUnPaged) 
        ? invoiceOperations.By(invoiceDetail.BillingProvider, invoiceDetail.InvoiceLineItemType).Get() 
        : invoiceOperations.By(invoiceDetail.BillingProvider, invoiceDetail.InvoiceLineItemType).Get(this.invoicePageSize, 0);

    // Create an enumerator for traversing the line items collection.
    var invoiceLineItemEnumerator = 
        partnerOperations.Enumerators.InvoiceLineItems.Create(invoiceLineItemsCollection);
    
    while (invoiceLineItemEnumerator.HasValue)
    {
        // invoiceLineItemEnumerator.Current contains a collection
        // of line items.
        Console.WriteLine(String.Format("invoiceLineItemEnumerator.Current has {0} line items.", 
            invoiceLineItemEnumerator.Current.TotalCount)); 
        //
        // Insert code here to work with the line items.
        //
        Console.WriteLine();
        Console.Write("Press any key to retrieve the next invoice line items page");
        Console.ReadKey();

        // Get the next list of invoice line items.
        invoiceLineItemEnumerator.Next();
    }
}
```

For a similar example, see **Sample**: [Console test app](console-test-app.md). **Project**: Partner Center SDK Samples **Class**: GetInvoiceLineItems.cs

## <span id="Request"></span><span id="request"></span><span id="REQUEST"></span>Request


**Request syntax**

Use the first syntax to return a full list of every line item for the given invoice. For large invoices, use the second syntax with a specified size and 0-based offset to return a paged list of line items.

| Method  | Request URI                                                                                                                                                     |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems/{billing-provider}/{invoice-line-item-type} HTTP/1.1                             |
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems/{billing-provider}/{invoice-line-item-type}?size={size}&offset={offset} HTTP/1.1 |

 

**URI parameters**

Use the following URI and query parameters when creating the request.

| Name                   | Type   | Required | Description                                                       |
|------------------------|--------|----------|-------------------------------------------------------------------|
| invoice-id             | string | Yes      | A string that identifies the invoice.                             |
| billing-provider       | string | Yes      | The billing provider: "Office", "Azure" or "AzureDataMarket".     |
| invoice-line-item-type | string | Yes      | The type of invoice detail: "BillingLineItems", "UsageLineItems". |
| size                   | number | No       | The maximum number of items to return.                            |
| offset                 | number | No       | The zero-based index of the first line item to return.            |

 

**Request headers**

-   See [Partner Center REST headers](headers.md) for more information.

**Request body**

None

## <span id="Response"></span><span id="response"></span><span id="RESPONSE"></span>Response


If successful, the response contains the collection of line item details.

**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center REST error codes](error-codes.md).

## <span id="Request_Response_Examples"></span><span id="request_response_examples"></span><span id="REQUEST_RESPONSE_EXAMPLES"></span>Request/Response Examples


**Request example** (BillingProvider: Office, InvoiceLineItemType: BillingLineItems)

```
GET https://api.partnercenter.microsoft.com/v1/invoices/D070002ISK/lineitems/Office/BillingLineItems?size=2&amp;offset=0 HTTP/1.1
Authorization: Bearer <token> 
Accept: application/json
MS-RequestId: 1eb2ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda03fe54
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

**Response example** (BillingProvider: Office, InvoiceLineItemType: BillingLineItems)

```
HTTP/1.1 200 OK
Content-Length: 2484
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda03fe54
MS-RequestId: 1eb2ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CV: bpqyomePDUqrSSYC.0
MS-ServerId: 202010406
Date: Thu, 07 Sep 2017 23:31:09 GMT

﻿{
    "totalCount": 2,
    "items": [{
            "partnerId": "3b33e682-00c3-41ee-9dd2-a548adf56438",
            "customerId": "74221236-D09C-4870-AC1D-33E155E9AEBE",
            "customerName": "TSTAGIN1CUST190",
            "mpnId": 4391507,
            "tier2MpnId": -1,
            "orderId": "567735045559164136",
            "subscriptionId": "4KIKawEAAAAAAAEA",
            "syndicationPartnerSubscriptionNumber": "1F58ACD7-FE51-4705-9567-D009C9ADA150",
            "offerId": "AAA5B3F0-0EE2-431B-A42F-3F18F3C6D540",
            "durableOfferId": "2F707C7C-2433-49A5-A437-9CA7CF40D3EB",
            "offerName": "EXCHANGE ONLINE (PLAN 2)",
            "domainName": "TStagin1Cust190.onmicrosoft.com",
            "billingCycleType": "MONTHLY",
            "subscriptionName": "EXCHANGE ONLINE (PLAN 2)",
            "subscriptionDescription": "EXCHANGE ONLINE (PLAN 2)",
            "subscriptionStartDate": "2017-05-12T00:00:00",
            "subscriptionEndDate": "2018-06-10T00:00:00",
            "chargeStartDate": "2017-05-12T00:00:00",
            "chargeEndDate": "2017-06-09T00:00:00",
            "chargeType": "PURCHASE FEE",
            "unitPrice": 0.0,
            "quantity": 3,
            "amount": 0.0,
            "totalOtherDiscount": 0.0,
            "subtotal": 0.0,
            "tax": 0.0,
            "totalForCustomer": 0.0,
            "currency": "USD",
            "invoiceLineItemType": "billing_line_items",
            "billingProvider": "office",
            "attributes": {
                "objectType": "LicenseBasedLineItem"
            }
        }, {
            "partnerId": "3b33e682-00c3-41ee-9dd2-a548adf56438",
            "customerId": "74221236-D09C-4870-AC1D-33E155E9AEBE",
            "customerName": "TSTAGIN1CUST190",
            "mpnId": 4391507,
            "tier2MpnId": -1,
            "orderId": "567735045564795186",
            "subscriptionId": "Ik4YawEAAAAAAAEA",
            "syndicationPartnerSubscriptionNumber": "D8A8F773-9D3E-4244-8797-3182075F09FA",
            "offerId": "618B53FE-9B99-428B-9745-F706AEAF3979",
            "durableOfferId": "69C67983-CF78-4102-83F6-3E5FD246864F",
            "offerName": "SHAREPOINT ONLINE (PLAN 2)",
            "domainName": "TStagin1Cust190.onmicrosoft.com",
            "billingCycleType": "MONTHLY",
            "subscriptionName": "SHAREPOINT ONLINE (PLAN 2)",
            "subscriptionDescription": "SHAREPOINT ONLINE (PLAN 2)",
            "subscriptionStartDate": "2017-05-13T00:00:00",
            "subscriptionEndDate": "2018-06-10T00:00:00",
            "chargeStartDate": "2017-05-13T00:00:00",
            "chargeEndDate": "2017-06-09T00:00:00",
            "chargeType": "PURCHASE FEE",
            "unitPrice": 0.0,
            "quantity": 1,
            "amount": 0.0,
            "totalOtherDiscount": 0.0,
            "subtotal": 0.0,
            "tax": 0.0,
            "totalForCustomer": 0.0,
            "currency": "USD",
            "invoiceLineItemType": "billing_line_items",
            "billingProvider": "office",
            "attributes": {
                "objectType": "LicenseBasedLineItem"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/invoices/D070002ISK/lineitems/Office/BillingLineItems?size=2&amp;offset=0",
            "method": "GET",
            "headers": []
        },
        "next": {
            "uri": "/invoices/D070002ISK/lineitems/Office/BillingLineItems?size=2&amp;offset=2",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

**Request example** (BillingProvider: Azure, InvoiceLineItemType: BillingLineItems)

```
GET https://api.partnercenter.microsoft.com/v1/invoices/D070002ISK/lineitems/Azure/BillingLineItems?size=2&amp;offset=0 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 1eb2ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda03fe54
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

**Response example** (BillingProvider: Azure, InvoiceLineItemType: BillingLineItems)

```
HTTP/1.1 200 OK
Content-Length: 2769
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda03fe54
MS-RequestId: 1eb2ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CV: mkcG2RWgd0qXi6MP.0
MS-ServerId: 201022015
Date: Fri, 08 Sep 2017 00:19:09 GMT

﻿{
    "totalCount": 2,
    "items": [{
            "detailLineItemId": 1,
            "sku": "7UD-00001",
            "includedQuantity": 0.0,
            "overageQuantity": 0.0008,
            "listPrice": 0.0003,
            "currency": "USD",
            "pretaxCharges": 0.0,
            "taxAmount": 0.0,
            "postTaxTotal": 0.0,
            "pretaxEffectiveRate": 0.0,
            "postTaxEffectiveRate": 0.0,
            "chargeType": "ASSESS USAGE FEE FOR CURRENT CYCLE",
            "invoiceLineItemType": "billing_line_items",
            "partnerId": "3B33E682-00C3-41EE-9DD2-A548ADF56438",
            "partnerName": "TEST_TEST_BUGBASH1",
            "partnerBillableAccountId": "3957834781",
            "customerId": "5F7CE186-F9B5-4532-BF66-1823B50498E2",
            "domainName": "FESTSHOUKAI.onmicrosoft.com",
            "customerCompanyName": "フェスト商会",
            "mpnId": 4391507,
            "tier2MpnId": -1,
            "invoiceNumber": "D070002ISK",
            "subscriptionId": "5B32D6C3-2AD3-4013-990A-9804D4E9B051",
            "subscriptionName": "MICROSOFT AZURE",
            "subscriptionDescription": "MICROSOFT AZURE",
            "billingCycleType": "MONTHLY",
            "orderId": "567735045903866440",
            "serviceName": "DATA MANAGEMENT",
            "serviceType": "",
            "resourceGuid": "12DA282F-7E96-49E2-983A-9A65DA2A4866",
            "resourceName": "STANDARD IO - TABLE READ OPERATION UNITS (IN 10,000S)",
            "region": "",
            "consumedQuantity": 0.0008,
            "chargeStartDate": "2017-05-10T00:00:00",
            "chargeEndDate": "2017-06-09T00:00:00",
            "unit": "10,000S",
            "billingProvider": "azure",
            "attributes": {
                "objectType": "UsageBasedLineItem"
            }
        }, {
            "detailLineItemId": 1,
            "sku": "7UD-00001",
            "includedQuantity": 0.0,
            "overageQuantity": 143.036111,
            "listPrice": 0.0595,
            "currency": "USD",
            "pretaxCharges": 8.51,
            "taxAmount": 0.0,
            "postTaxTotal": 8.51,
            "pretaxEffectiveRate": 0.05949546,
            "postTaxEffectiveRate": 0.05949546,
            "chargeType": "ASSESS USAGE FEE FOR CURRENT CYCLE",
            "invoiceLineItemType": "billing_line_items",
            "partnerId": "3B33E682-00C3-41EE-9DD2-A548ADF56438",
            "partnerName": "TEST_TEST_BUGBASH1",
            "partnerBillableAccountId": "3957834781",
            "customerId": "5F7CE186-F9B5-4532-BF66-1823B50498E2",
            "domainName": "FESTSHOUKAI.onmicrosoft.com",
            "customerCompanyName": "フェスト商会",
            "mpnId": 4391507,
            "tier2MpnId": -1,
            "invoiceNumber": "D070002ISK",
            "subscriptionId": "5B32D6C3-2AD3-4013-990A-9804D4E9B051",
            "subscriptionName": "MICROSOFT AZURE",
            "subscriptionDescription": "MICROSOFT AZURE",
            "billingCycleType": "MONTHLY",
            "orderId": "567735045903866440",
            "serviceName": "STORAGE",
            "serviceType": "LOCALLY REDUNDANT",
            "resourceGuid": "3F2B1E1C-C886-4EC6-AD6F-DD0EF38819C9",
            "resourceName": "STANDARD IO - TABLE (GB)",
            "region": "",
            "consumedQuantity": 143.036111,
            "chargeStartDate": "2017-05-10T00:00:00",
            "chargeEndDate": "2017-06-09T00:00:00",
            "unit": "GB",
            "billingProvider": "azure",
            "attributes": {
                "objectType": "UsageBasedLineItem"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/invoices/D070002ISK/lineitems/Azure/BillingLineItems?size=2&amp;offset=0",
            "method": "GET",
            "headers": []
        },
        "next": {
            "uri": "/invoices/D070002ISK/lineitems/Azure/BillingLineItems?size=2&amp;offset=2",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

**Request example** (BillingProvider: Azure, InvoiceLineItemType: UsageLineItems)

```
GET https://api.partnercenter.microsoft.com/v1/invoices/D070002ISK/lineitems/Azure/UsageLineItems?size=2&amp;offset=0 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 606429d6-99dc-49c5-bc17-b155c22c9e81
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda03fe54
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

**Response example** (BillingProvider: Azure, InvoiceLineItemType: UsageLineItems)

```
HTTP/1.1 200 OK
Content-Length: 2322
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda03fe54
MS-RequestId: 606429d6-99dc-49c5-bc17-b155c22c9e81
MS-CV: 2ClpjdfSLEOot0no.0
MS-ServerId: 202010406
Date: Fri, 08 Sep 2017 00:46:26 GMT

﻿{
    "totalCount": 2,
    "items": [{
            "customerBillableAccount": "5028553399",
            "usageDate": "2017-06-09T00:00:00",
            "invoiceLineItemType": "usage_line_items",
            "partnerId": "3B33E682-00C3-41EE-9DD2-A548ADF56438",
            "partnerName": "TEST_TEST_BUGBASH1",
            "partnerBillableAccountId": "3957834781",
            "customerId": "5F7CE186-F9B5-4532-BF66-1823B50498E2",
            "domainName": "FESTSHOUKAI.onmicrosoft.com",
            "customerCompanyName": "フェスト商会",
            "mpnId": 4391507,
            "tier2MpnId": -1,
            "invoiceNumber": "D070002ISK",
            "subscriptionId": "5B32D6C3-2AD3-4013-990A-9804D4E9B051",
            "subscriptionName": "MICROSOFT AZURE",
            "subscriptionDescription": "MICROSOFT AZURE",
            "billingCycleType": "MONTHLY",
            "orderId": "567735045903866440",
            "serviceName": "DATA MANAGEMENT",
            "serviceType": "",
            "resourceGuid": "12DA282F-7E96-49E2-983A-9A65DA2A4866",
            "resourceName": "STANDARD IO - TABLE READ OPERATION UNITS (IN 10,000S)",
            "region": "",
            "consumedQuantity": 0.0002,
            "chargeStartDate": "2017-05-10T00:00:00",
            "chargeEndDate": "2017-06-09T00:00:00",
            "unit": "10,000S",
            "billingProvider": "azure",
            "attributes": {
                "objectType": "DailyUsageLineItem"
            }
        }, {
            "customerBillableAccount": "5028553399",
            "usageDate": "2017-06-09T00:00:00",
            "invoiceLineItemType": "usage_line_items",
            "partnerId": "3B33E682-00C3-41EE-9DD2-A548ADF56438",
            "partnerName": "TEST_TEST_BUGBASH1",
            "partnerBillableAccountId": "3957834781",
            "customerId": "5F7CE186-F9B5-4532-BF66-1823B50498E2",
            "domainName": "FESTSHOUKAI.onmicrosoft.com",
            "customerCompanyName": "フェスト商会",
            "mpnId": 4391507,
            "tier2MpnId": -1,
            "invoiceNumber": "D070002ISK",
            "subscriptionId": "5B32D6C3-2AD3-4013-990A-9804D4E9B051",
            "subscriptionName": "MICROSOFT AZURE",
            "subscriptionDescription": "MICROSOFT AZURE",
            "billingCycleType": "MONTHLY",
            "orderId": "567735045903866440",
            "serviceName": "STORAGE",
            "serviceType": "LOCALLY REDUNDANT",
            "resourceGuid": "3F2B1E1C-C886-4EC6-AD6F-DD0EF38819C9",
            "resourceName": "STANDARD IO - TABLE (GB)",
            "region": "",
            "consumedQuantity": 4.38427,
            "chargeStartDate": "2017-05-10T00:00:00",
            "chargeEndDate": "2017-06-09T00:00:00",
            "unit": "GB",
            "billingProvider": "azure",
            "attributes": {
                "objectType": "DailyUsageLineItem"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/invoices/D070002ISK/lineitems/Azure/UsageLineItems?size=2&amp;offset=0",
            "method": "GET",
            "headers": []
        },
        "next": {
            "uri": "/invoices/D070002ISK/lineitems/Azure/UsageLineItems?size=2&amp;offset=2",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

 

 




