---
title: Resource usage resources
description: Describes the estimated monetary cost of a subscription's resource level usage in the current billing cycle.
ms.assetid: 61B98AB8-D802-4EC1-91FB-B7A2B95DE20C
ms.date: 09/18/2019
ms.localizationpriority: medium
---

# Resource usage resources


**Applies To**

- Partner Center

Describes the estimated monetary cost of a subscription's resource level usage in the current billing cycle.

## <span id="ResourceUsageRecord"/><span id="resourceusagerecord"/><span id="RESOURCEUSAGERECORD"/>ResourceUsageRecord

| Property         | Type               | Description                                                                                   |
|------------------|--------------------|-----------------------------------------------------------------------------------------------|
| SubscriptionId           | string             | Gets or sets the subscription Id (For "Azure 145P" this is commerce subscription id. For "Azure Plan" this is azure plan id).                  |
| ResourceUri  | string             | Gets or sets the resource Uri."                                                        |
| ResourceType          | string             | Gets or sets the resource type.                                       |
| EntitlementId               | string             | Gets or sets the entitlement Id (AKA azure subscription id).                                                 |
| EntitlementName             | string             | Gets or sets the entitlement name.                                                     |
| ResourceGroupName        | double             | Gets or sets the resource group name.   |
| Name   | string             | The name of the resource. |
| ResourceName   | string             | Gets or sets the name of the resource.. |
| TotalCost   | decimal             | Gets or sets the estimated total cost of usage. |
| CurrencyCode   | string             | Gets or sets the currency code.                                          |
| USDTotalCost   | decimal             | Gets or sets the estimated total cost in USD.                                         |
| LastModifiedDate | string             | The day, in date-time format, that this record was last modified.                             |
| Attributes       | ResourceAttributes | The metadata attributes corresponding to the resource.                                        |                                           |

 

 

 




