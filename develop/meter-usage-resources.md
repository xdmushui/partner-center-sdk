---
title: Meter usage resources
description: Describes the estimated monetary cost of a subscription's meter level usage in the current billing cycle.
ms.assetid: 61B98AB8-D802-4EC1-91FB-B7A2B95DE20C
ms.date: 09/18/2019
ms.localizationpriority: medium
---

# Meter usage resources


**Applies To**

- Partner Center

Describes the estimated monetary cost of a subscription's meter level usage in the current billing cycle.

## <span id="MeterUsageRecord"/><span id="meterusagerecord"/><span id="METERUSAGERECORD"/>MeterUsageRecord

| Property         | Type               | Description                                                                                   |
|------------------|--------------------|-----------------------------------------------------------------------------------------------|
| SubscriptionId           | string             | Gets or sets the subscription Id (For "Azure 145P" this is commerce subscription id. For "Azure Plan" this is azure plan id).                  |
| MeterId  | string             | Gets or sets the meter Id.                                                        |
| MeterName          | string             | Gets or sets the meter name.                                       |
| Category               | string             | Gets or sets the Azure resource category.                                                 |
| Subcategory             | string             |  Gets or sets the Azure resource sub-category.                                                     |
| QuantityUsed        | decimal             | Gets or sets the quantity of the Azure resource used.   |
| Unit   | string             | Gets or sets the unit of measure for the Azure resource. |
| TotalCost   | decimal             | Gets or sets the estimated total cost of usage. |
| CurrencyLocale   | string             | The locale in which the subscription was used, determines the currency to use on the invoice **Available for Azure 145P**. |
| CurrencyCode   | string             | Gets or sets the currency code. **Available for  Azure Plan**.                                         |
| USDTotalCost   | decimal             | Gets or sets the estimated total cost in USD. **Available for Azure Plan**.                                         |
| LastModifiedDate | string             | The day, in date-time format, that this record was last modified.                             |
| Attributes       | ResourceAttributes | The metadata attributes corresponding to the resource.                                        |                                           |

 

 

 




