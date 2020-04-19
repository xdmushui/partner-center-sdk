---
title: Meter usage record resource
description: You can use the MeterUsageRecord resource to describe the estimated monetary cost of a subscription's meter level usage in the current billing cycle.
ms.assetid: 
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice:  partnercenter-sdk
ms.localizationpriority: medium
---

# Meter usage record resource

**Applies to:**

- Partner Center

You can use the **MeterUsageRecord** resource to describe the estimated monetary cost of a subscription's meter level usage in the current billing cycle.

## MeterUsageRecord

| Property         | Type               | Description                                                                                   |
|------------------|--------------------|-----------------------------------------------------------------------------------------------|
| SubscriptionId           | string             | A GUID corresponding to the identifier of a Partner Center [subscription resource](subscription-resources.md#subscription), which represents a Microsoft Azure (MS-AZR-0145P) subscription or an Azure plan. For Microsoft Azure (MS-AZR-0145P) subscriptions,, this value is the commerce subscription identifier. For Azure plan subscription resources, this value is the Azure plan identifier.                  |
| MeterId  | string             | Gets or sets the meter identifier.                                                        |
| MeterName          | string             | Gets or sets the meter name.                                       |
| Category               | string             | Gets or sets the Azure resource category.                                                 |
| Subcategory             | string             |  Gets or sets the Azure resource sub-category.                                                     |
| QuantityUsed        | decimal             | Gets or sets the quantity of the Azure resource used.   |
| Unit   | string             | Gets or sets the unit of measure for the Azure resource. |
| TotalCost   | decimal             | Gets or sets the estimated total cost of usage. |
| CurrencyLocale   | string             | The locale in which the subscription was used. This property determines the currency that is used on the invoice. This property is available for Microsoft Azure (MS-AZR-0145P) subscriptions. |
| CurrencyCode   | string             | Gets or sets the currency code. This property is available for Azure plans.                                         |
| USDTotalCost   | decimal             | Gets or sets the estimated total cost in USD. This property is available for Azure plans.                                         |
| LastModifiedDate | string             | The day (in date-time format) that this record was last modified.                             |
| Attributes       | ResourceAttributes | The metadata attributes corresponding to the resource.                                        |                                           |
