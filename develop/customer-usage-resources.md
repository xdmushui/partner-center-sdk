---
title: Customer usage resources
description: Resources for customers with usage-based subscriptions and monthly use budgets (including CustomerMonthlyUsageRecord, CustomerUsageSummary, PartnerUsageSummary, and SpendingBudget).
ms.assetid: 268C7AF5-3A95-451F-8092-033A3E8126F2
ms.date: 10/23/2019
ms.localizationpriority: medium
---

# Customer usage resources

[!INCLUDE [<Preview content warning>](<../includes/preview.md>)]

Applies to:

- Partner Center
- Partner Center for Microsoft Cloud Germany
- Partner Center for Microsoft Cloud for US Government

Customers with usage-based subscriptions may have a monthly use budget. This budget sets a limit on the customer's maximum usage and allows the partner to track their usage over time.

> [!NOTE]
> Customer usage numbers are estimates (not final values), which should not be used for billing purposes.

## CustomerMonthlyUsageRecord

**CustomerMonthlyUsageRecord** represents the estimated monetary cost of a customer's usage in the current month.

| Property         | Type               | Description                                                              |
|------------------|--------------------|--------------------------------------------------------------------------|
| Budget           | SpendingBudget     | The spending budget allocated for the customer.                          |
| PercentUsed      | decimal             | The percentage used out of the allocated budget.                        |
| ResourceId       | string             | The unique identifier of the resource.                                   |
| ResourceName     | string             | The name of the resource.                                                |
| TotalCost        | decimal             | The estimated total cost of usage for the resources in the subscription.|
| CurrencyLocale   | string             | The customer's currency locale. Available for Microsoft Azure (MS-AZR-0145P) subscriptions.            |
| CurrencyCode     | string             | Gets or sets the currency code. Available for Azure plans.           |
| USDTotalCost     | decimal             | Gets or sets the estimated total cost in USD. Available for Azure plans.                                         |
| IsUpgraded       | bool             | Gets or sets a value indicating whether the customer's Azure subscription is upgraded. The value **true** represents customers who have an Azure plan.                         |
| LastModifiedDate | date               | The date the usage data was last modified.                               |
| Attributes       | ResourceAttributes | The metadata attributes corresponding to the usage record.               |

## CustomerUsageSummary

**CustomerUsageSummary** represents a summary of the customer's usage for an entire billing period.

| Property         | Type               | Description                                                                                                      |
|------------------|--------------------|------------------------------------------------------------------------------------------------------------------|
| Budget           | SpendingBudget     | The spending budget allocated for the customer.                                                                  |
| ResourceId       | string             | The unique identifier of the resource. In the context of CustomerMonthlyUsageRecord, this id is the customer id. |
| ResourceName     | string             | The name of the resource. In the context of CustomerMonthlyUsageRecord, this is the customer name.               |
| BillingStartDate | date               | The start date of the current billing period.                                                                    |
| BillingEndDate   | date               | The end date of the current billing period.                                                                      |
| TotalCost        | decimal             | The estimated total cost of usage for the resources in the subscription.                                         |
| CurrencyLocale   | string             | The customer's currency locale. Available for Microsoft Azure (MS-AZR-0145P) subscriptions.                                         |
| CurrencyCode     | string             | Gets or sets the currency code. Available for Azure plans.                                         |
| USDTotalCost     | decimal             | Gets or sets the estimated total cost in USD. Available for Azure plan subscription resources.                                         |
| LastModifiedDate | date               | The date the usage data was last modified.                                                                       |
| Links            | ResourceLinks      | The resource links corresponding to the usage summary.                                                           |
| Attributes       | ResourceAttributes | The metadata attributes corresponding to the usage summary.                                                      |

## PartnerUsageSummary

**PartnerUsageSummary** represents a partner-level summary of usage budgeting for all customers.

| Property         | Type               | Description                                                                                                      |
|------------------|--------------------|------------------------------------------------------------------------------------------------------------------|
| EmailsToNotify   | array of strings   | The list of email addresses for notifications.                                                                   |
| CustomerOverBudget | integer          | The number of customers that are over budget.                                                                    |
| CustomersTrendingOver | integer       | The number of customers that are close to going over budget.                                                     |
| CustomersWithUsageBasedSubscriptions  | integer | The number of customers with a usage-based subscription.                                               |
| ResourceId       | string             | The unique identifier of the resource. In the context of CustomerMonthlyUsageRecord, this id is the customer id. |
| ResourceName     | string             | The name of the resource. In the context of CustomerMonthlyUsageRecord, this is the customer name.               |
| BillingStartDate | date               | The start date of the current billing period.                                                                    |
| BillingEndDate   | date               | The end date of the current billing period.                                                                      |
| TotalCost        | decimal             | The estimated total cost of all customer usage based on current usage from the start of the billing period.      |
| CurrencyLocale   | string             | The currency locale.                                                                                             |
| LastModifiedDate | date               | The date the usage data was last modified.                                                                       |
| Links            | ResourceLinks      | The resource links corresponding to the usage summary.                                                           |
| Attributes       | ResourceAttributes | The metadata attributes corresponding to the usage summary.                                                      |

## SpendingBudget

**SpendingBudget** represents the budget allocated to this customer for usage-based subscriptions.

| Property   | Type               | Description                                                                                         |
|------------|--------------------|-----------------------------------------------------------------------------------------------------|
| Amount     | decimal             | The allocated budget. If the value is null, there is no spending budget allocated to this customer. |
| Attributes | ResourceAttributes | The metadata attributes corresponding to the budget.                                                |
