---
title: Invoice
description: Describes invoice related resources.
ms.assetid: FDD151CC-3473-46DF-A422-265DCBC8A498
ms.author: v-thpr
ms.date: 12/15/2017
ms.topic: article
ms.prod: partner-center
ms.technology: partner-center-sdk
---

# Invoice


<span class="sidebar_heading" style="font-weight: bold;">Applies
To</span>

-   Partner Center
-   Partner Center operated by 21Vianet
-   Partner Center for Microsoft Cloud Germany
-   Partner Center for Microsoft Cloud for US Government

Describes invoice related resources.

## <span id="Invoice"></span><span id="invoice"></span><span id="INVOICE"></span>Invoice


| Property        | Type                                                           | Description                                                                                                                                                                                          |
|-----------------|----------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id              | string                                                         | The invoice identifier.                                                                                                                                                                              |
| invoiceDate     | string in UTC date-time format                                 | The date the invoice was generated.                                                                                                                                                                  |
| totalCharges    | number                                                         | The total charges. Includes charges for transactions and any adjustments.                                                                                                                            |
| paidAmount      | number                                                         | The amount paid by the partner. Negative if a payment was received.                                                                                                                                  |
| currencyCode    | string                                                         | A code that indicates the currency used for all invoice item amounts and totals.                                                                                                                     |
| currencySymbol  | string                                                         | The currency symbol used for all invoice item amounts and totals.                                                                                                                                    |
| pdfDownloadLink | string                                                         | A link to download the invoice in PDF format. This link is not returned as part of the search results, and is populated only if the invoice is accessed by ID. This link auto-expires in 30 minutes. |
| invoiceDetails  | array of [InvoiceDetail](#invoicedetail) objects               | The invoice details.                                                                                                                                                                                 |
| amendments      | array of [Invoice](#invoice) objects                           | The amendments to this invoice.                                                                                                                                                                      |
| links           | [ResourceLinks](utility-resources.md#resourcelinks)           | The resource links.                                                                                                                                                                                  |
| attributes      | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes.                                                                                                                                                                             |

 

## <span id="InvoiceDetail"></span><span id="invoicedetail"></span><span id="INVOICEDETAIL"></span>InvoiceDetail


An invoice contains a collection of billed items, and each item is
represented by an InvoiceDetail resource.

| Property            | Type                                                           | Description                                                                       |
|---------------------|----------------------------------------------------------------|-----------------------------------------------------------------------------------|
| invoiceLineItemType | string                                                         | The type of invoice detail: "none", "usage\_line\_items", "billing\_line\_items". |
| billingProvider     | string                                                         | The billing provider: "none", "office", "azure" or "azure\_data\_market".         |
| links               | [ResourceLinks](utility-resources.md#resourcelinks)           | The resource links.                                                               |
| attributes          | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes.                                                          |

 

## <span id="InvoiceLineItem"></span><span id="invoicelineitem"></span><span id="INVOICELINEITEM"></span>InvoiceLineItem


Each individual charge within an invoice is represented as an
InvoiceLineItem.

| Property            | Type                                                           | Description                                                                          |
|---------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------|
| invoiceLineItemType | string                                                         | The type of invoice line item: "none", "usage\_line\_items", "billing\_line\_items". |
| billingProvider     | string                                                         | The billing provider: "none", "office", "azure" or "azure\_data\_market".            |
| attributes          | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes.                                                             |

 

## <span id="InvoiceSummary"></span><span id="invoicesummary"></span><span id="INVOICESUMMARY"></span>InvoiceSummary


Describes a summary of the balance and total charges of an invoice.

| Property                 | Type                                                           | Description                                                           |
|--------------------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| balanceAmount.           | number                                                         | The balance of the invoice. This is the total amount of unpaid bills. |
| currencyCode             | string                                                         | A code that indicates the currency used for the balance amount.       |
| currencySymbol           | string                                                         | The currency symbol used.                                             |
| accountingDate           | string in UTC date-time format                                 | The date the balance amount was last updated.                         |
| firstInvoiceCreationDate | string in UTC date-time format                                 | The date the first invoice for the customer was created.              |
| links                    | [ResourceLinks](utility-resources.md#resourcelinks)           | The resource links.                                                   |
| attributes               | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes.                                              |

 

 

 




