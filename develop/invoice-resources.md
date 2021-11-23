---
title: Invoice resources
description: Multiple invoice-related resources are available through the Partner Center APIs. These resources are related to invoice and line item details.
ms.date: 01/27/2020
ms.service: partner-dashboard
ms.subservice:  partnercenter-sdk
---

# Invoice resources

**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

The following invoice-related resources are available through the Partner Center APIs.

## Invoice

| Property | Type | Description |
| -------- | ---- | ----------- |
| id | string | The invoice identifier. |
| invoiceDate | string in UTC date-time format | The date the invoice was generated. |
| billingPeriodStartDate | string in UTC date-time format | Billing period start date in UTC. |
| billingPeriodEndDate | string in UTC date-time format   | Billing period end date in UTC. |
| totalCharges | number | The total charges. Includes charges for transactions and any adjustments.     |
| paidAmount | number  | The amount paid by the partner. Negative if a payment was received.  |
| currencyCode | string  | A code that indicates the currency used for all invoice item amounts and totals. |
| currencySymbol  | string | The currency symbol used for all invoice item amounts and totals. |
| pdfDownloadLink | string  | A link to download the invoice in PDF format. This link isn't returned as part of the search results, and is populated only if the invoice is accessed by ID. This link auto-expires in 30 minutes. |
| invoiceDetails  | array of [InvoiceDetail](#invoicedetail) objects  | The invoice details.  |
| amendments      | array of [Invoice](#invoice) objects   | The amendments to this invoice.  |
| documentType    | string | The document type of the invoice: "Credit Note", "Invoice". |
| amendsOf        | string | The reference number of the document of which this document is an amendment.  |
| invoiceType     | string  | The type of invoice: "recurring", "one\_time".   |
| links           | [ResourceLinks](utility-resources.md#resourcelinks)  | The resource links.  |
| attributes      | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes.  |

## InvoiceDetail

An invoice contains a collection of billed items, and each item is
represented by an InvoiceDetail resource.

| Property            | Type                                                           | Description                                                                       |
|---------------------|----------------------------------------------------------------|-----------------------------------------------------------------------------------|
| invoiceLineItemType | string                                                         | The type of invoice detail: "none", "usage\_line\_items", "billing\_line\_items". |
| billingProvider     | string                                                         | The billing provider: "none", "office", "azure" or "azure\_data\_market".         |
| links               | [ResourceLinks](utility-resources.md#resourcelinks)           | The resource links.                                                               |
| attributes          | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes.                                                          |

## InvoiceLineItem

Each individual charge within an invoice is represented as an
InvoiceLineItem.

| Property            | Type                                                           | Description                                                                          |
|---------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------|
| invoiceLineItemType | string                                                         | The type of invoice line item: "none", "usage\_line\_items", "billing\_line\_items". |
| billingProvider     | string                                                         | The billing provider: "none", "office", "azure" or "azure\_data\_market".            |
| attributes          | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes.                                                             |

## InvoiceSummary

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

## InvoiceSummaryDetail

Represent a summary of the individual details for an invoice type (for example, recurring, one\_time).

| Property            | Type                                                           | Description                                                                          |
|---------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------|
| invoiceType         | string                                                         | The type of invoice: "recurring", "one\_time".                                       |
| summary             | [InvoiceSummary](#invoicesummary) object                       | The summary of the invoice per invoice type.                                         |

## InvoiceSummaries

Represent a collection of type [InvoiceSummary](#invoicesummary) that contain the individual details for an invoice type per currency.

| Property            | Type                                                           | Description                                                                          |
|---------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------|
| collectionOfSummary | array of [InvoiceSummary](#invoicesummary) objects             | The summary of the invoice per invoice type per currency.                            |

## LicenseBasedLineItem

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
| mpnId                    | number                                                         | Gets or sets the MPN ID associated to this line item. For direct resellers, this is the MPN ID of the reseller. For indirect resellers, this is the MPN ID of the Value Added Reseller (VAR).                                   |
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
| tier2MpnId               | number                                                         | Gets or sets the MPN ID of the Tier 2 partner associated to this line item. |
| totalForCustomer         | number                                                         | Gets or sets the total amount after discount and tax.                 |
| totalOtherDiscount       | number                                                         | Gets or sets the discount associated with this purchase.              |
| unitPrice                | number                                                         | Gets or sets the unit price.                                          |

## UsageBasedLineItem

Represents an invoice billing line item for usage-based subscriptions.

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
| customerName             | string                                                         | Gets or sets the customer name.                                       |
| customerId               | string                                                         | Gets or sets the customer unique identifier.                          |
| detailLineItemId         | number                                                         | Gets or sets the detail line item ID. Uniquely identifies the line items for cases where calculation is different for units consumed. Example: Total consumed = 1338, 1024 is charged with one rate, 314 is charge with a different rate.        |
| domainName               | string                                                         | Gets or sets domain name.                                             |
| includedQuantity         | number                                                         | Gets or sets the units included in the order.                         |
| invoiceLineItemType      | string                                                         | Gets the type of invoice line item.                                   |
| invoiceNumber            | string                                                         | Gets or sets the invoice number.                                      |
| listPrice                | number                                                         | Gets or sets the price of each unit.                                  |
| mpnId                    | number                                                         | Gets or sets the MPN ID associated to this line item. For direct resellers, this is the MPN ID of the reseller. For indirect resellers, this is the MPN ID of the Value Added Reseller (VAR).                                   |
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
| tier2MpnId               | number                                                         | Gets or sets the MPN ID of the Tier 2 partner associated to this line item. |
| unit                     | string                                                         | Gets or sets the unit of measure for Azure usage.                     |

## InvoiceStatement

Represents the operations available on an invoice statement in application/pdf.

| Property                 | Type                                                           | Description                                                           |
|--------------------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| httpResponseMessage      | object                                                         | ByteArrayContent with contentType = application/pdf.                  |

## OneTimeInvoiceLineItem

Represents an invoice billing line item for licensed-based subscriptions.

| Property | Type | Description |
| --- | --- | --- |
| PartnerId | string | Gets or sets the partner tenant ID. |
| CustomerId | string | Gets or sets the customer tenant ID. |
| CustomerName | string | Gets or sets the customer name. |
| CustomerDomainName | string | Gets or sets the customer domain name. |
| CustomerCountry | string | Gets or sets the customer country. |
| InvoiceNumber | string | Gets or sets the invoice number. |
| MpnId | string | Gets or sets the MPN ID associated to this line item. |
| ResellerMpnId | int | Gets or sets the MPN ID of the Tier 2 partner associated to this line item. |
| OrderDate | DateTime | Gets or sets the date when order created. |
| ProductId | string | Gets or sets the product unique identifier. |
| SkuId | string | Gets or sets the SKU unique identifier. |
| AvailabilityId | string | Gets or sets the availability unique identifier. |
| ProductName | string | Gets or sets the product name. |
| SkuName | string | Gets or sets the SKU name. |
| ChargeType | string | Gets or sets the type of charge. |
| UnitPrice | decimal | Gets or sets the unit price. |
| EffectiveUnitPrice | decimal | Gets or sets the effective unit price. |
| UnitType | string | Gets or sets the unit type. |
| Quantity | int | Gets or sets the number of units associated with this line item. |
| Subtotal | decimal | Gets or sets the amount after discount. |
| TaxTotal | decimal | Gets or sets the taxes charged. |
| TotalForCustomer | decimal | Gets or sets the total amount after discount and tax. |
| Currency | string | Gets or sets the currency used for this line item. |
| PublisherName | string | Gets or sets the publisher name associated with this purchase. |
| PublisherId | string | Gets or sets the publisher ID associated with this purchase. |
| SubscriptionDescription | string | Gets or sets the subscription description associated with this purchase. |
| SubscriptionId | string | Gets or sets the subscription ID associated with this purchase. |
| ChargeStartDate | DateTime | Gets or sets the charge start date associated with this purchase. |
| ChargeEndDate | DateTime | Gets or sets the charge end date associated with this purchase. |
| TermAndBillingCycle | string | Gets or sets the term and billing cycle associated with this purchase. |
| AlternateId | string | Gets or sets the Alternate ID (quote ID). |
| PriceAdjustmentDescription | string | Gets or sets the price adjustment description. |
| CreditReasonCode | string | Gets or sets the credit reason code. |
| DiscountDetails | string |  **Deprecated**. Gets or sets the discount details associated with this purchase. |
| PricingCurrency | string | Gets or sets the pricing currency code. |
| PCToBCExchangeRate | decimal | Gets or sets the pricing currency to the billing currency exchange rate. |
| PCToBCExchangeRateDate | DateTime | Gets or sets the exchange rate date at which the pricing currency to the billing currency exchange rate was determined. |
| BillableQuantity | decimal | Gets or sets the units purchased. For each design column named as **BillableQuantity**. |
| MeterDescription | string | Gets or sets the meter description for consumption line item. |
| ReservationOrderId | string | Gets or sets the reservation order identifier for an Azure RI Purchase. |
| BillingFrequency | string | Gets or sets the billing frequency. |
| InvoiceLineItemType | InvoiceLineItemType | Returns the type of invoice line item. |
| BillingProvider | BillingProvider | Returns the billing provider. |

## DailyRatedUsageLineItem

Represents unbilled, billed reconciliation line items for daily rated usage.

| Property | Type | Description |
| --- | --- | --- |
| PartnerId | string | Gets or sets the partner tenant ID. |
| PartnerName | string | Gets or sets the partner name. |
| CustomerId | string | Gets or sets the tenant ID of the customer that usage belongs to. |
| CustomerName | string | Gets or sets the name of the customer company that usage belongs to. |
| CustomerDomainName | string | Gets or sets the domain name of the customer that usage belongs to. |
| InvoiceNumber | string | Gets or sets the ID of the invoice that usage belongs to. |
| ProductId | string | Gets or sets the product unique identifier. |
| SkuId | string | Gets or sets the SKU unique identifier. |
| AvailabilityId | string | Gets or sets the availability unique identifier. |
| SkuName | string | Gets or sets the SKU name for the service. |
| ProductName | string | Gets or sets the name of the product. |
| PublisherName | string | Gets or sets the name of publisher. |
| PublisherId | string | Gets or sets the ID of the publisher. |
| SubscriptionId | string | Gets or sets the subscription ID. |
| SubscriptionDescription | string | Gets or sets the subscription description. |
| ChargeStartDate | DateTime | Gets or sets the charge start date. |
| ChargeEndDate | DateTime | Gets or sets the charge end date. |
| UsageDate | DateTime | Gets or sets the usage date. |
| MeterType | string | Gets or sets the meter type. |
| MeterCategory | string | Gets or sets the meter category. |
| MeterId | string | Gets or sets the  meter ID (GUID). |
| MeterSubCategory | string | Gets or sets the meter sub category. |
| MeterName | string | Gets or sets the meter name. |
| MeterRegion | string | Gets or sets the meter region. |
| UnitOfMeasure | string | Gets or sets the unit of measure. |
| ResourceLocation | string | Gets or sets the location of resource. |
| ConsumedService | string | Gets or sets the consumed service name. |
| ResourceGroup | string | Gets or sets the name of resource group. |
| ResourceUri | string | Gets or sets the uri of the resource instance that the usage is about. |
| Tags | string | Gets or sets the customer added tags. |
| AdditionalInfo | string | Gets or sets the service-specific metadata. For example, an image type for a virtual machine. |
| ServiceInfo1 | string | Gets or sets internal Azure Service Metadata. |
| ServiceInfo2 | string | Gets or sets service information, for example, an image type for a virtual machine and ISP name for ExpressRoute. |
| CustomerCountry | string | Gets or sets the country of the customer. |
| MpnId | string | Gets or sets the MPN ID associated to this line item. |
| ResellerMpnId | string | Gets or sets the Reseller MPN ID of the Tier 2 partner associated to this line item. |
| ChargeType | string | Gets or sets the type of charge. |
| UnitPrice | decimal | Gets or sets the price of unit. |
| Quantity | decimal | Gets or sets the quantity of usage. |
| UnitType | string | Gets or sets the unit type (such as 1 hour). |
| BillingPreTaxTotal | decimal | Gets or sets the extended cost or total cost before tax in local currency of the customer or billing currency. |
| BillingCurrency | string | Gets or sets ISO currency in which the meter is charged in local currency of the customer or billing currency. |
| PricingPreTaxTotal | decimal | Gets or sets the extended cost or total cost before tax in USD or catalog currency used for rating. |
| PricingCurrency | string | Gets or sets ISO currency in which the meter is charged in USD or catalog currency used for rating. |
| EntitlementId | string | Gets or sets the entitlement (Azure subscription) ID. |
| EntitlementDescription | string | Gets or sets the entitlement (Azure subscription) description. |
| PCToBCExchangeRate | string | Gets or sets the pricing currency to the billing currency exchange rate. |
| PCToBCExchangeRateDate | DateTime | Gets or sets the pricing currency to the billing currency exchange rate date. |
| EffectiveUnitPrice | decimal | Gets or sets the effective unit price. |
| RateOfPartnerEarnedCredit | decimal | Gets or sets the rate of partner earned credit. |
| HasPartnerEarnedCredit | bool | Gets or sets is partner earned credit applied. |
| RateOfCredit | decimal | Gets or sets the rate of credit for the given credit type. |
| CreditType | string | Gets or sets the type of credit. |
| InvoiceLineItemType | InvoiceLineItemType | Returns the type of invoice line item. |
| BillingProvider | BillingProvider | Returns the billing provider. |
