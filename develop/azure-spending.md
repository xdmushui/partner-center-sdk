---
title: Azure spending
description: CSP partners can use Partner Center APIs to view and manage their Azure spending. They can also programmatically view their customers' Azure spending against their budget.
ms.assetid: 
ms.date: 09/24/2019
ms.localizationpriority: medium
---

# Azure spending

Applies to:

- Partner Center
- Partner Center operated by 21Vianet
- Partner Center for Microsoft Cloud Germany
- Partner Center for Microsoft Cloud for US Government

Cloud Solution Provider (CSP) partners can view and manage their Azure spending through Partner Center APIs. They can also programmatically view their customers' spending against an Azure spending budget.

For more information, see [scenarios in which CSP partners can use the Partner Center APIs to manage customer and partner accounts and orders](scenarios.md), specifically the [background section](scenarios.md#background).

## Partner usage management

- [Get a partner usage summary](get-a-partner-usage-summary.md) using the **PartnerUsageSummary** resource
- [Get usage records for all customers](get-a-customer-s-usage-records.md) using the **CustomerMonthlyUsageRecord** resource

## Customer usage management

- [Get a customer's usage summary](get-a-customer-usage-summary.md) using the **CustomerUsageSummary** resource
- [Get all subscription usage records for a customer](get-a-customer-subscription-s-usage-records.md) using the **SubscriptionMonthlyUsageRecord** resource

## Subscription usage management

- [Get a subscription usage summary](get-a-customer-subscription-usage-summary.md) using the **SubscriptionUsageSummary** resource
- [Get all monthly usage records for a subscription](get-all-monthly-usage-records-for-a-subscription.md) using the **AzureResourceMonthlyUsageRecord** resource
- [Get usage data for a subscription by resource](get-a-customer-subscription-resource-usage-records.md) using the **ResourceUsageRecord** resource
- [Get usage data for a subscription by meter](get-a-customer-subscription-meter-usage-records.md) using the **MeterUsageRecord** resource

## Azure spending budget management

- [Get a customer's usage budget](get-a-customer-s-usage-spending-budget.md) using the **CustomerUsageSummary** resource
- [Update a customer's usage budget](update-a-customer-s-usage-spending-budget.md) using the **CustomerUsageSummary** resource
