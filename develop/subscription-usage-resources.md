---
title: Subscription usage resources
description: Subscription usage resources describe subscriptions with usage-based billing. These subscriptions have daily and monthly usage records, along with a usage summary for each pay period.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice:  partnercenter-sdk
---

# Subscription usage resources

**Applies to:**

- Partner Center
- Partner Center for Microsoft Cloud Germany
- Partner Center for Microsoft Cloud for US Government

You can use the following subscription usage resources to get usage information for a specific subscription with usage-based billing. These subscriptions have daily and monthly usage records, along with a usage summary for each pay period.

## SubscriptionDailyUsageRecord

*The **SubscriptionDailyUsageRecord** resource is obsolete and may produce inaccurate results. We recommend that you update your applications to use the APIs described in [Get a customer's utilization records for Azure](get-a-customer-s-utilization-record-for-azure.md) and [Get prices for Microsoft Azure](get-prices-for-microsoft-azure.md) instead.*

The **SubscriptionDailyUsageRecord** resource describes how much a subscription is used in a single day.

| Property         | Type               | Description                                                                                   |
|------------------|--------------------|-----------------------------------------------------------------------------------------------|
| DateUsed         | string             | The day, in date-time format, that the subscription was used.                                 |
| ResourceId       | string             | GUID. The unique ID of the resource.                                                          |
| ResourceName     | string             | The name of the resource.                                                                     |
| TotalCost        | decimal             | The estimated total cost of using the resources in the subscription on the specified day.     |
| CurrencyLocale   | string             | The locale in which the subscription was used, determines the currency to use on the invoice. |
| LastModifiedDate | string             | The day, in date-time format, that this record was last modified.                             |
| Attributes       | ResourceAttributes | The metadata attributes corresponding to the resource.                                        |

## SubscriptionMonthlyUsageRecord

The **SubscriptionMonthlyUsageRecord** resource describes how much a subscription is used in a single month.

| Property         | Type               | Description                                                                                   |
|------------------|--------------------|-----------------------------------------------------------------------------------------------|
| Status           | string             | The status of the subscription: "none", "active", "suspended", or "deleted".                  |
| PartnerOnRecord  | string             | "The MPN ID of the partner on record."                                                        |
| OfferId          | string             | GUID. The id of the offer related to this subscription.                                       |
| Id               | string             | GUID. The id of the subscription or resource.                                                 |
| Name             | string             | The name of the subscription or resource.                                                     |
| TotalCost        | decimal             | The estimated total cost of using the resources in the subscription in the specified month.   |
| CurrencyLocale   | string             | The locale in which the subscription was used, determines the currency to use on the invoice. Available for Microsoft Azure (MS-AZR-0145P) subscriptions. |
| CurrencyCode     | string             | Gets or sets the currency code. Available for Azure plan subscription resources.                                         |
| USDTotalCost     | decimal             | Gets or sets the estimated total cost in USD. Available for Azure plans.                                         |
| LastModifiedDate | string             | The day, in date-time format, that this record was last modified.                             |
| Attributes       | ResourceAttributes | The metadata attributes corresponding to the resource.                                        |

## SubscriptionUsageSummary

The **SubscriptionUsageSummary** resource describes how much a specific subscription was used in the current billing period.

| Property         | Type               | Description                                                                                                            |
|------------------|--------------------|------------------------------------------------------------------------------------------------------------------------|
| ResourceId       | string             | GUID. The id of the subscription or resource. In the context of CustomerMonthlyUsageRecord this id is the customer id. |
| ResourceName     | string             | The name of the subscription or resource. In the context of CustomerMonthlyUsageRecord this name is the customer name. |
| BillingStartDate | date               | The start date of the current billing period, in date-time format.                                                     |
| BillingEndDate   | date               | The end date of the current billing period, in date-time format.                                                       |
| TotalCost        | double             | The estimated total cost of using the resources in the subscription during the specified billing period.               |
| CurrencyLocale   | string             | The locale in which the subscription was used, determines the currency to use on the invoice. Available for Microsoft Azure (MS-AZR-0145P) subscriptions. |
| CurrencyCode   | string             | Gets or sets the currency code. Available for Azure plans.                                         |
| USDTotalCost   | decimal             | Gets or sets the estimated total cost in USD. Available for Azure plan subscription resources.                                         |
| LastModifiedDate | string             | The day, in date-time format, that this record was last modified.                                                      |
| Links            | ResourceLinks      | The resource links corresponding to the SubscriptionUsageSummary.                                                      |
| Attributes       | ResourceAttributes | The metadata attributes corresponding to the SubscriptionUsageSummary.                                                 |
