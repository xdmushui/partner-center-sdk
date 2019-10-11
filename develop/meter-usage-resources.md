---
title: Meter usage record resource
description: The MeterUsageRecord resource describes the estimated monetary cost of a subscription's meter level usage in the current billing cycle.
ms.assetid: 
ms.date: 10/11/2019
ms.localizationpriority: medium
---

# Meter usage record resource

[!INCLUDE [<Preview content warning>](<../includes/preview.md>)]

Applies to:

- Partner Center

You can use the **MeterUsageRecord** resource to describe the estimated monetary cost of a subscription's meter level usage in the current billing cycle.

## MeterUsageRecord

| Property         | Type               | Description                                                                                   |
|------------------|--------------------|-----------------------------------------------------------------------------------------------|
| SubscriptionId           | string             | Gets or sets the subscription identifier. For **Azure 145P offers**, this value is the commerce subscription identifier. For Azure plan subscription resources, this value is the Azure plan identifier.                  |
| MeterId  | string             | Gets or sets the meter identifier.                                                        |
| MeterName          | string             | Gets or sets the meter name.                                       |
| Category               | string             | Gets or sets the Azure resource category.                                                 |
| Subcategory             | string             |  Gets or sets the Azure resource sub-category.                                                     |
| QuantityUsed        | decimal             | Gets or sets the quantity of the Azure resource used.   |
| Unit   | string             | Gets or sets the unit of measure for the Azure resource. |
| TotalCost   | decimal             | Gets or sets the estimated total cost of usage. |
| CurrencyLocale   | string             | The locale in which the subscription was used. This property determines the currency that is used on the invoice. This property is available  for **Azure 145P**. |
| CurrencyCode   | string             | Gets or sets the currency code. This property is available for Azure plan subscription resources.                                         |
| USDTotalCost   | decimal             | Gets or sets the estimated total cost in USD. This property is available for Azure plan subscription resources.                                         |
| LastModifiedDate | string             | The day (in date-time format) that this record was last modified.                             |
| Attributes       | ResourceAttributes | The metadata attributes corresponding to the resource.                                        |                                           |
