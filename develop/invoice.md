---
title: Invoice
description: Describes invoice related resources.
ms.assetid: FDD151CC-3473-46DF-A422-265DCBC8A498
ms.date: 12/15/2017
ms.localizationpriority: medium
---

# Invoice


**Applies To**

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
| documentType    | string                                                         | The document type of the invoice: "Credit Note", "Invoice".                                                                                                                           |
| amendsOf        | string                                                         | The reference number of the document of which this document is an amendment.                                                                                                                                  |
| invoiceType     | string                                                         | The type of invoice: "recurring", “one\_time".                                                                                                                                                        |
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
| balanceAmount            | number                                                         | The balance of the invoice. This is the total amount of unpaid bills. |
| currencyCode             | string                                                         | A code that indicates the currency used for the balance amount.       |
| currencySymbol           | string                                                         | The currency symbol used.                                             |
| accountingDate           | string in UTC date-time format                                 | The date the balance amount was last updated.                         |
| firstInvoiceCreationDate | string in UTC date-time format                                 | The date the first invoice for the customer was created.              |
| lastPaymentDate          | string in UTC date-time format                                 | The date of the last payment.                                         |
| lastPaymentAmount        | number                                                         | The amount of the last payment.                                       |
| latestInvoiceDate        | string in UTC date-time format                                 | The date the last invoice for the customer was created.               |
| details                  | array of [InvoiceSummaryDetail](#invoicesummarydetail) objects | The invoice summary detail.                                           |
| links                    | [ResourceLinks](utility-resources.md#resourcelinks)            | The resource links.                                                   |
| attributes               | [ResourceAttributes](utility-resources.md#resourceattributes)  | The metadata attributes.                                              |

 

## <span id="InvoiceSummaryDetail"></span><span id="invoicesummarydetail"></span><span id="INVOICESUMMARYDETAIL"></span>InvoiceSummaryDetail


Represent a summary of the individual details for an invoice type (for example, recurring, one\_time). 

| Property            | Type                                                           | Description                                                                          |
|---------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------|
| invoiceType         | string                                                         | The type of invoice: "recurring", “one\_time".                                       |
| summary             | [InvoiceSummary](#invoicesummary) object                       | The summary of the invoice per invoice type.                                         |
 

 
## <span id="InvoiceSummaries"></span><span id="invoicesummaries"></span><span id="INVOICESUMMARIES"></span>InvoiceSummaries


Represent a collection of type [InvoiceSummary](#invoicesummary) that contain the individual details for an invoice type per currency.  

| Property            | Type                                                           | Description                                                                          |
|---------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------|
| collectionOfSummary | array of [InvoiceSummary](#invoicesummary) objects             | The summary of the invoice per invoice type per currency.                            |



## <span id="LicenseBasedLineItem"></span><span id="licensebasedlineitem"></span><span id="LICENSEBASEDLINEITEM"></span>LicenseBasedLineItem


Represents an invoice billing line item for licensed based subscriptions.

| Property                 | Type                                                           | Description                                                           |
|--------------------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| amount                   | string                                                         | Gets or sets the total amount. Total amount = unit price * quantity.  |
| attributes               | string                                                         | Gets the attributes.                                                  |
| billingCycleType         | string                                                         | Gets or sets the billing cycle type.                                  |
| billingProvider          | string                                                         | Gets the billing provider.                                            |
| chargeEndDate            | string in UTC date-time format                                 | Gets or sets the end date for the charge.                             |
| chargeStartDate          | string in UTC date-time format                                 | Gets or sets the start date for the charge.                           |
| chargeType               | string                                                         | Gets or sets the type of charge.                                      |
| currency                 | string                                                         | Gets or sets the currency used for this line item.                    |
| customerId               | string                                                         | Gets or sets the customer unique identifier in the Microsoft billing platform.  |
| customerName             | string in UTC date-time format                                 | Gets or sets the customer name.                                       |
| domainName               | string                                                         | Gets or sets domain name.                                             |
| durableOfferId           | string                                                         | Gets or sets the durable offer unique identifier.                     |
| invoiceLineItemType      | string                                                         | Gets the type of invoice line item.                                   |
| mpnId                    | number                                                         | Gets or sets the MPN Id associated to this line item. For direct resellers, this is the MPN Id of the reseller. For indirect resellers, this is the MPN Id of the VAR (Value Added Reseller).                                   |
| offerId                  | string                                                         | Gets or sets the offer unique identifier.                             |
| offerName                | string                                                         | Gets or sets the offer name.                                          |
| orderId                  | string                                                         | Gets or sets the order unique identifier.                             |
| partnerId                | string                                                         | Gets or sets the partner Azure active directory tenant ID.            |
| quantity                 | number                                                         | Gets or sets the number of units associated with this line item.      |
| subscriptionDescription  | string                                                         | Gets or sets the subscription description.                            |
| subscriptionEndDate      | string in UTC date-time format                                 | Gets or sets the date when subscription expires.                      |
| subscriptionId           | string                                                         | Gets or sets the subscription unique identifier.                      |
| subscriptionName         | string                                                         | Gets or sets the subscription name.                                   |
| subscriptionStartDate    | string in UTC date-time format                                 | Gets or sets the date when the subscription starts.                   |
| subtotal                 | number                                                         | Gets or sets the amount after discount.                               |
| syndicationPartnerSubscriptionNumber | string                                             | Gets or sets the syndication partner subscription number.             |
| tax                      | number                                                         | Gets or sets the taxes charged.                                       |
| tier2MpnId               | number                                                         | Gets or sets the MPN Id of the Tier 2 partner associated to this line item. |
| totalForCustomer         | number                                                         | Gets or sets the total amount after discount and tax.                 |
| totalOtherDiscount       | number                                                         | Gets or sets the discount associated with this purchase.              |
| unitPrice                | number                                                         | Gets or sets the unit price.                                          |



## <span id="UsageBasedLineItem"></span><span id="usagebasedlineitem"></span><span id="USAGEBASEDLINEITEM"></span>UsageBasedLineItem


Represents an invoice billing line item for usage based subscriptions.

| Property                 | Type                                                           | Description                                                           |
|--------------------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| attributes               | string                                                         | Gets the attributes.                                                  |
| billingCycleType         | string                                                         | Gets or sets the billing cycle type.                                  |
| billingProvider          | string                                                         | Gets the billing provider.                                            |
| chargeEndDate            | string in UTC date-time format                                 | Gets or sets the end date for the charge.                             |
| chargeStartDate          | string in UTC date-time format                                 | Gets or sets the start date for the charge.                           |
| chargeType               | string                                                         | Gets or sets the type of charge.                                      |
| consumedQuantity         | number                                                         | Gets or sets the total units consumed.                                |
| consumptionDiscount      | string                                                         | Gets or sets the discount on consumption.                             |
| consumptionPrice         | string                                                         | Gets or sets the price of quantity consumed.                          |
| currency                 | string                                                         | Gets or sets the currency associated with the prices.                 |
| customerCompanyName      | string                                                         | Gets or sets the customer company name.                               |
| customerId               | string                                                         | Gets or sets the customer unique identifier.                          |
| detailLineItemId         | number                                                         | Gets or sets the detail line item ID. Uniquely identifies the line items for cases where calculation is different for units consumed. Example: Total consumed = 1338, 1024 is charged with one rate, 314 is charge with a different rate.        |
| domainName               | string                                                         | Gets or sets domain name.                                             |
| includedQuantity         | number                                                         | Gets or sets the units included in the order.                         |
| invoiceLineItemType      | string                                                         | Gets the type of invoice line item.                                   |
| invoiceNumber            | string                                                         | Gets or sets the invoice number.                                      |
| listPrice                | number                                                         | Gets or sets the price of each unit.                                  |
| mpnId                    | number                                                         | Gets or sets the MPN Id associated to this line item. For direct resellers, this is the MPN Id of the reseller. For indirect resellers, this is the MPN Id of the VAR (Value Added Reseller).                                   |
| orderId                  | string                                                         | Gets or sets the order unique identifier.                             |
| overageQuantity          | number                                                         | Gets or sets the quantity consumed above allowed usage.               |
| partnerBillableAccountId | string                                                         | Gets or sets the partner billable account ID.                         |
| partnerId                | string                                                         | Gets or sets the partner Azure active directory tenant ID.            |
| partnerName              | string                                                         | Gets or sets the partner's name.                                      |
| postTaxEffectiveRate     | number                                                         | Gets or sets the effective price after taxes.                         |
| postTaxTotal             | number                                                         | Gets or sets the total charges after tax. Pretax Charges + Tax Amount |
| preTaxCharges            | number                                                         | Gets or sets the price charged before taxes.                          |
| preTaxEffectiveRate      | number                                                         | Gets or sets the effective price before taxes.                        |
| region                   | string                                                         | Gets or sets the region associated with the resource instance.        |
| resourceGuid             | string                                                         | Gets or sets the resource identifier.                                 |
| resourceName             | string                                                         | Gets or sets the resource name. Example: Database (GB/month).         |
| serviceName              | string                                                         | Gets or sets the service name. Example: Azure Data Service.           |
| serviceType              | string                                                         | Gets or sets the service type. Example: Azure SQL Azure DB.           |
| sku                      | string                                                         | Gets or sets the service SKU.                                         |
| subscriptionDescription  | string                                                         | Gets or sets the subscription description.                            |
| subscriptionId           | string                                                         | Gets or sets the subscription unique identifier.                      |
| subscriptionName         | string                                                         | Gets or sets the subscription name.                                   |
| taxAmount                | number                                                         | Gets or sets the amount of tax charged.                               |
| tier2MpnId               | number                                                         | Gets or sets the MPN Id of the Tier 2 partner associated to this line item. |
| unit                     | string                                                         | Gets or sets the unit of measure for Azure usage.                     |



## <span id="InvoiceStatement"></span><span id="invoicestatement"></span><span id="INVOICESTATEMENT"></span>InvoiceStatement


Represents the operations available on an invoice statement in application/pdf.

| Property                 | Type                                                           | Description                                                           |
|--------------------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| httpResponseMessage      | object                                                         | ByteArrayContent with contentType = application/pdf.                  |
