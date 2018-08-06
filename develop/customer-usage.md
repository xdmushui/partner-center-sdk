---
title: Customer Usage Budgeting
description: 
    Customers with usage-based subscriptions may have a monthly use budget,
    which sets a limit on their maximum usage and allows the partner to
    track their usage over time.
ms.assetid: 268C7AF5-3A95-451F-8092-033A3E8126F2
ms.author: mhopkins
ms.date: 12/15/2017
ms.topic: article
ms.prod: partner-center
ms.technology: partner-center-sdk
---

# Customer Usage Budgeting


**Applies To**

-   Partner Center
-   Partner Center for Microsoft Cloud Germany
-   Partner Center for Microsoft Cloud for US Government

Customers with usage-based subscriptions may have a monthly use budget,
which sets a limit on their maximum usage and allows the partner to
track their usage over time. Customer usage numbers are estimates, not
final values, and they should not be used for billing purposes.

## <span id="CustomerMonthlyUsageRecord"></span><span id="customermonthlyusagerecord"></span><span id="CUSTOMERMONTHLYUSAGERECORD"></span>CustomerMonthlyUsageRecord


Represents the estimated monetary cost of a customer's usage in the
current month.

| Property         | Type               | Description                                                              |
|------------------|--------------------|--------------------------------------------------------------------------|
| Budget           | SpendingBudget     | The spending budget allocated for the customer.                          |
| PercentUsed      | double             | The percentage used out of the allocated budget.                         |
| ResourceId       | string             | The unique identifier of the resource.                                   |
| ResourceName     | string             | The name of the resource.                                                |
| TotalCost        | dobule             | The estimated total cost of usage for the resources in the subscription. |
| CurrencyLocale   | string             | The customer's currency locale.                                          |
| LastModifiedDate | date               | The date the usage data was last modified.                               |
| Attributes       | ResourceAttributes | The metadata attributes corresponding to the usage record.               |

 

## <span id="CustomerUsageSummary"></span><span id="customerusagesummary"></span><span id="CUSTOMERUSAGESUMMARY"></span>CustomerUsageSummary


Represents a summary of the customer's usage for an entire billing
period.

| Property         | Type               | Description                                                                                                      |
|------------------|--------------------|------------------------------------------------------------------------------------------------------------------|
| Budget           | SpendingBudget     | The spending budget allocated for the customer.                                                                  |
| ResourceId       | string             | The unique identifier of the resource. In the context of CustomerMonthlyUsageRecord, this id is the customer id. |
| ResourceName     | string             | The name of the resource. In the context of CustomerMonthlyUsageRecord, this is the customer name.               |
| BillingStartDate | date               | The start date of the current billing period.                                                                    |
| BillingEndDate   | date               | The end date of the current billing period.                                                                      |
| TotalCost        | dobule             | The estimated total cost of usage for the resources in the subscription.                                         |
| CurrencyLocale   | string             | The customer's currency locale.                                                                                  |
| LastModifiedDate | date               | The date the usage data was last modified.                                                                       |
| Links            | ResourceLinks      | The resource links corresponding to the usage summary.                                                           |
| Attributes       | ResourceAttributes | The metadata attributes corresponding to the usage summary.                                                      |

 

## <span id="PartnerUsageSummary"></span><span id="partnerusagesummary"></span><span id="PARTNERUSAGESUMMARY"></span>PartnerUsageSummary


Represents a partner-level summary of usage budgeting for all customers.

| Property                             | Type               | Description                                                                                                      |
|--------------------------------------|--------------------|------------------------------------------------------------------------------------------------------------------|
| EmailsToNotify                       | array of strings   | The list of email addresses for notifications.                                                                   |
| CustomerOverBudget                   | integer            | The number of customers that are over budget.                                                                    |
| CustomersTrendingOver                | integer            | The number of customers that are close to going over budget.                                                     |
| CustomersWithUsageBasedSubscriptions | integer            | The number of customers with a usage-based subscription.                                                         |
| ResourceId                           | string             | The unique identifier of the resource. In the context of CustomerMonthlyUsageRecord, this id is the customer id. |
| ResourceName                         | string             | The name of the resource. In the context of CustomerMonthlyUsageRecord, this is the customer name.               |
| BillingStartDate                     | date               | The start date of the current billing period.                                                                    |
| BillingEndDate                       | date               | The end date of the current billing period.                                                                      |
| TotalCost                            | dobule             | The estimated total cost of all customer usage based on current usage from the start of the billing period.      |
| CurrencyLocale                       | string             | The currency locale.                                                                                             |
| LastModifiedDate                     | date               | The date the usage data was last modified.                                                                       |
| Links                                | ResourceLinks      | The resource links corresponding to the usage summary.                                                           |
| Attributes                           | ResourceAttributes | The metadata attributes corresponding to the usage summary.                                                      |

 

## <span id="SpendingBudget"></span><span id="spendingbudget"></span><span id="SPENDINGBUDGET"></span>SpendingBudget


Represents the budget allocated to this customer for usage-based
subscriptions.

| Property   | Type               | Description                                                                                         |
|------------|--------------------|-----------------------------------------------------------------------------------------------------|
| Amount     | Double             | The allocated budget. If the value is null, there is no spending budget allocated to this customer. |
| Attributes | ResourceAttributes | The metadata attributes corresponding to the budget.                                                |

 

 

 




