---
title: Get a collection of invoices
description: How to retrieve a collection of the partner's invoices.
ms.assetid: B5392987-3D2E-493B-9F97-A20055D5D46A
ms.author: v-thpr
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


To get a collection of all available invoices, use the [**Invoices**](https://review.docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.ipartner.invoices) property to get an interface to invoice operations, and then call the [**Get**](https://review.docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.get) or [**GetAsync**](https://review.docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.getasync) method to retrieve the collection.

To get a paged collection of invoices, first call the [**BuildIndexedQuery**](https://review.docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildindexedquery) method and pass it the page size to create an [**IQuery**](https://review.docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.query.iquery) object. Next, use the [**Invoices**](https://review.docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.ipartner.invoices) property to get an interface to invoice operations, and then pass the IQuery object to the [**Query**](https://review.docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.query) or [**QueryAsync**](https://review.docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.queryasync) method to send the request and get the first page.

Next, use the [**Enumerators**](https://review.docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.ipartner.enumerators) property to get an interface to the collection of supported resource collection enumerators, and then call [**Invoices.Create**](https://review.docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory.create) to create an enumerator for traversing the collection of invoices. Finally, use the enumerator to retrieve and work with each page of invoices as shown in the following code example. Each call to the [**Next**](https://review.docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.enumerators.iresourcecollectionenumerator.next) method sends a request for the next page of invoices based on the page size.

```
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

## <span id="Request"></span><span id="request"></span><span id="REQUEST"></span>Request


**Request syntax**

| Method  | Request URI                                                                                  |
|---------|----------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/invoices?size={size}&offset={offset} HTTP/1.1 |

 

**URI parameter**

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

## <span id="Response"></span><span id="response"></span><span id="RESPONSE"></span>Response


If successful, the response body contains the collection of [Invoice](invoice.md#invoice) resources.

**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center REST error codes](error-codes.md).

**Response example**

```
HTTP/1.1 200 OK
Content-Length: 2231
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 4a5002a2-0c1b-4e57-b491-dbcf19c0e7b8
MS-RequestId: 7b3e2e00-b330-4480-9d84-59ace713427f
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Mon, 24 Jul 2017 22:55:51 GMT

{
    "totalCount": 2,
    "items": [{
            "id": "D070002J8C",
            "invoiceDate": "2017-07-11T00:00:00Z",
            "totalCharges": 88029.46,
            "paidAmount": 0.0,
            "currencyCode": "USD",
            "currencySymbol": "$",
            "pdfDownloadLink": "/invoices/D070002J8C/documents/statement",
            "invoiceDetails": [{
                    "invoiceLineItemType": "billing_line_items",
                    "billingProvider": "office",
                    "links": {
                        "self": {
                            "uri": "/invoices/D070002J8C/lineitems/Office/BillingLineItems",
                            "method": "GET",
                            "headers": []
                        }
                    },
                    "attributes": {
                        "objectType": "InvoiceDetail"
                    }
                }, {
                    "invoiceLineItemType": "billing_line_items",
                    "billingProvider": "azure",
                    "links": {
                        "self": {
                            "uri": "/invoices/D070002J8C/lineitems/Azure/BillingLineItems",
                            "method": "GET",
                            "headers": []
                        }
                    },
                    "attributes": {
                        "objectType": "InvoiceDetail"
                    }
                }, {
                    "invoiceLineItemType": "usage_line_items",
                    "billingProvider": "azure",
                    "links": {
                        "self": {
                            "uri": "/invoices/D070002J8C/lineitems/Azure/UsageLineItems",
                            "method": "GET",
                            "headers": []
                        }
                    },
                    "attributes": {
                        "objectType": "InvoiceDetail"
                    }
                }
            ],
            "links": {
                "self": {
                    "uri": "/invoices/D070002J8C",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Invoice"
            }
        }, {
            "id": "D070002ISK",
            "invoiceDate": "2017-06-11T00:00:00Z",
            "totalCharges": 115761.32,
            "paidAmount": 0.0,
            "currencyCode": "USD",
            "currencySymbol": "$",
            "pdfDownloadLink": "/invoices/D070002ISK/documents/statement",
            "invoiceDetails": [{
                    "invoiceLineItemType": "billing_line_items",
                    "billingProvider": "office",
                    "links": {
                        "self": {
                            "uri": "/invoices/D070002ISK/lineitems/Office/BillingLineItems",
                            "method": "GET",
                            "headers": []
                        }
                    },
                    "attributes": {
                        "objectType": "InvoiceDetail"
                    }
                }, {
                    "invoiceLineItemType": "billing_line_items",
                    "billingProvider": "azure",
                    "links": {
                        "self": {
                            "uri": "/invoices/D070002ISK/lineitems/Azure/BillingLineItems",
                            "method": "GET",
                            "headers": []
                        }
                    },
                    "attributes": {
                        "objectType": "InvoiceDetail"
                    }
                }, {
                    "invoiceLineItemType": "usage_line_items",
                    "billingProvider": "azure",
                    "links": {
                        "self": {
                            "uri": "/invoices/D070002ISK/lineitems/Azure/UsageLineItems",
                            "method": "GET",
                            "headers": []
                        }
                    },
                    "attributes": {
                        "objectType": "InvoiceDetail"
                    }
                }
            ],
            "links": {
                "self": {
                    "uri": "/invoices/D070002ISK",
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

 

 




