---
title: Get a collection of invoices
description: How to retrieve a collection of the partner's invoices.
ms.assetid: B5392987-3D2E-493B-9F97-A20055D5D46A
ms.author: mhopkins
ms.date: 12/15/2017
ms.topic: article
ms.prod: partner-center
ms.technology: partner-center-sdk
---

# Get a collection of invoices


**Applies To**

-   Partner Center
-   Partner Center operated by 21Vianet
-   Partner Center for Microsoft Cloud Germany
-   Partner Center for Microsoft Cloud for US Government

How to retrieve a collection of the partner's invoices.

## <span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>Prerequisites


-   Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.

## <span id="C_"></span><span id="c_"></span>C#


To get a collection of all available invoices, use the [**Invoices**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.ipartner.invoices) property to get an interface to invoice operations, and then call the [**Get**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.get) or [**GetAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.getasync) method to retrieve the collection.

To get a paged collection of invoices, first call the [**BuildIndexedQuery**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildindexedquery) method and pass it the page size to create an [**IQuery**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.query.iquery) object. Next, use the [**Invoices**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.ipartner.invoices) property to get an interface to invoice operations, and then pass the IQuery object to the [**Query**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.query) or [**QueryAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.queryasync) method to send the request and get the first page.

Next, use the [**Enumerators**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.ipartner.enumerators) property to get an interface to the collection of supported resource collection enumerators, and then call [**Invoices.Create**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create) to create an enumerator for traversing the collection of invoices. Finally, use the enumerator to retrieve and work with each page of invoices as shown in the following code example. Each call to the [**Next**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.enumerators.iresourcecollectionenumerator-1.next) method sends a request for the next page of invoices based on the page size.

``` csharp
// IAggregatePartner partnerOperations;
// int invoicePageSize;

// Is this an unpaged or paged request?
bool isUnpaged = (this.invoicePageSize <= 0);

// If the scenario is unpaged, get all the invoices, otherwise get the first page.
var invoicesPage = (isUnpaged) 
                 ? partnerOperations.Invoices.Get() 
                 : partnerOperations.Invoices.Query(QueryFactory.Instance.BuildIndexedQuery(this.invoicePageSize));

// Create an invoice enumerator for traversing the invoice pages.
var invoicesEnumerator = partnerOperations.Enumerators.Invoices.Create(invoicesPage);
int lineCounter = 1;

while (invoicesEnumerator.HasValue)
{
    // Print the current invoice results page.
    var invoices = invoicesEnumerator.Current.Items;
    
    foreach (var i in invoices)
    {
        Console.WriteLine(String.Format("{0,3}. {1}  {2}  {3,16:C2}", 
            lineCounter++, 
            i.Id, 
            i.InvoiceDate.ToString("yyyy&#39;-&#39;MM&#39;-&#39;dd&#39;T&#39;HH&#39;:&#39;mm&#39;:&#39;ss&#39;Z&#39;"),
            i.TotalCharges));
    }

    Console.WriteLine();
    Console.Write("Press any key to retrieve the next invoices page");
    Console.ReadKey();

    // Get the next page of invoices.
    invoicesEnumerator.Next();
}
```

For a slightly different example, see **Sample**: [Console test app](console-test-app.md). **Project**: Partner Center SDK Samples **Class**: GetPagedInvoices.cs

## <span id="Request"></span><span id="request"></span><span id="REQUEST"></span>REST Request


**Request syntax**

| Method  | Request URI                                                                                  |
|---------|----------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/invoices?size={size}&offset={offset} HTTP/1.1  |

 

**URI parameters**

Use the following query parameters when creating the request.

| Name   | Type | Required | Description                                                                            |
|--------|------|----------|----------------------------------------------------------------------------------------|
| size   | int  | No       | The number of invoice resources to return in the response. This parameter is optional. |
| offset | int  | No       | The zero-based index of the first invoice to return.                                   |

 

**Request headers**

-   See [Partner Center REST headers](headers.md) for more information.

**Request body**

None

**Request example**

```
GET https://api.partnercenter.microsoft.com/v1/invoices?size=200&amp;offset=0 HTTP/1.1
Authorization: Bearer <token> 
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

## <span id="Response"></span><span id="response"></span><span id="RESPONSE"></span>REST Response


If successful, the response body contains the collection of [Invoice](invoice.md#invoice) resources.

**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center REST error codes](error-codes.md).

**Response example**

``` json
HTTP/1.1 200 OK
Content-Length: 256
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
MS-RequestId: a45e6643-1caf-4429-8f90-07c03d85bc2b
Date: Thu, 24 Mar 2016 05:21:01 GMT
{
    "totalCount": 2,
    "items": [
        {
            "id": "D02005YFHI",
            "invoiceDate": "2017-01-21T00:00:00Z",
            "totalCharges": 24606.35,
            "paidAmount": 1000,
            "currencyCode": "GBP",
            "currencySymbol": "£",
            "pdfDownloadLink": "/invoices/D02005YFHI/documents/statement",
            "invoiceDetails": [
                {
                    "invoiceLineItemType": "billing_line_items",
                    "billingProvider": "office",
                    "links": {
                        "self": {
                            "uri": "/invoices/Recurring-D02005YFHI/lineitems/Office/BillingLineItems",
                            "method": "GET",
                            "headers": []
                        }
                    },
                    "attributes": {
                        "objectType": "InvoiceDetail"
                    }
                }
            ],
            "documentType": "invoice",
            "invoiceType": "Recurring",
            "links": {
                "self": {
                    "uri": "/invoices/Recurring-D02005YFHI",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Invoice"
            }
        },
        {
            "id": "G000024130",
            "invoiceDate": "2018-02-08T01:22:47.603895Z",
            "totalCharges": 586366,
            "paidAmount": 0,
            "currencyCode": "CHF",
            "currencySymbol": "CHF",
            "pdfDownloadLink": "/invoices/G000024130/documents/statement",
            "invoiceDetails": [
                {
                    "invoiceLineItemType": "billing_line_items",
                    "billingProvider": "one_time",
                    "links": {
                        "self": {
                            "uri": "/invoices/OneTime-G000024130/lineitems/OneTime/BillingLineItems",
                            "method": "GET",
                            "headers": []
                        }
                    },
                    "attributes": {
                        "objectType": "InvoiceDetail"
                    }
                }
            ],
            "amendments": [
                {
                    "id": "G000024131",
                    "invoiceDate": "2018-02-08T18:44:37.5381456Z",
                    "totalCharges": 107661.12,
                    "paidAmount": 0,
                    "currencyCode": "CHF",
                    "currencySymbol": "CHF",
                    "invoiceDetails": [
                        {
                            "invoiceLineItemType": "billing_line_items",
                            "billingProvider": "one_time",
                            "attributes": {
                                "objectType": "InvoiceDetail"
                            }
                        }
                    ],
                    "documentType": "adjustment_note",
                    "amendsOf": "G000024130",
                    "invoiceType": "OneTime",
                    "attributes": {
                        "objectType": "Invoice"
                    }
                }
            ],
            "documentType": "void_note",
            "invoiceType": "OneTime",
            "links": {
                "self": {
                    "uri": "/invoices/OneTime-G000024130",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Invoice"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/invoices?size=2&amp;offset=0",
            "method": "GET",
            "headers": []
        },
        "next": {
            "uri": "/invoices?size=2&amp;offset=2",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

 

 




