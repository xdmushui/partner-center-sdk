---
title: Subscription Usage
description: 
    Describes usage information for a specific subscription with usage-based
    billing. These subscriptions have daily and monthly usage records, along
    with a usage summary for each pay period.
ms.assetid: 61B98AB8-D802-4EC1-91FB-B7A2B95DE20C
ms.author: v-thpr
ms.date: 12/15/2017
ms.topic: article
ms.prod: partner-center
ms.technology: partner-center-sdk
---

# Subscription Usage


**Applies To**

-   Partner Center
-   Partner Center for Microsoft Cloud Germany
-   Partner Center for Microsoft Cloud for US Government

Describes usage information for a specific subscription with usage-based
billing. These subscriptions have daily and monthly usage records, along
with a usage summary for each pay period.

## <span id="SubscriptionDailyUsageRecord"></span><span id="subscriptiondailyusagerecord"></span><span id="SUBSCRIPTIONDAILYUSAGERECORD"></span>SubscriptionDailyUsageRecord


>[!NOTE]
>The SubscriptionDailyUsageRecord resource is obsolete and may produce inaccurate results. We recommend that you update your applications to use the APIs described in
>[Get a customer's utilization records for Azure](get-a-customer-s-utilization-record-for-azure.md) and [Get prices for Microsoft Azure](get-prices-for-microsoft-azure.md)
>instead.

 

Describes how much a subscription is used in a single day.

| Property         | Type               | Description                                                                                   |
|------------------|--------------------|-----------------------------------------------------------------------------------------------|
| DateUsed         | string             | The day, in date-time format, that the subscription was used.                                 |
| ResourceId       | string             | GUID. The unique ID of the resource.                                                          |
| ResourceName     | string             | The name of the resource.                                                                     |
| TotalCost        | double             | The estimated total cost of using the resources in the subscription on the specified day.     |
| CurrencyLocale   | string             | The locale in which the subscription was used, determines the currency to use on the invoice. |
| LastModifiedDate | string             | The day, in date-time format, that this record was last modified.                             |
| Attributes       | ResourceAttributes | The metadata attributes corresponding to the resource.                                        |

 

## <span id="SubscriptionMonthlyUsageRecord"></span><span id="subscriptionmonthlyusagerecord"></span><span id="SUBSCRIPTIONMONTHLYUSAGERECORD"></span>SubscriptionMonthlyUsageRecord


Describes how much a subscription is used in a single month.

| Property         | Type               | Description                                                                                   |
|------------------|--------------------|-----------------------------------------------------------------------------------------------|
| Status           | string             | The status of the subscription: "none", "active", "suspended", or "deleted".                  |
| PartnerOnRecord  | string             | "The MPN ID of the partner on record."                                                        |
| OfferId          | string             | GUID. The id of the offer related to this subscription.                                       |
| Id               | string             | GUID. The id of the subscription or resource.                                                 |
| Name             | string             | The name of the subscription or resource.                                                     |
| TotalCost        | double             | The estimated total cost of using the resources in the subscription in the specified month.   |
| CurrencyLocale   | string             | The locale in which the subscription was used, determines the currency to use on the invoice. |
| LastModifiedDate | string             | The day, in date-time format, that this record was last modified.                             |
| Attributes       | ResourceAttributes | The metadata attributes corresponding to the resource.                                        |

 

## <span id="SubscriptionUsageSummary"></span><span id="subscriptionusagesummary"></span><span id="SUBSCRIPTIONUSAGESUMMARY"></span>SubscriptionUsageSummary


Describes how much a specific subscription was used in the current
billing period.

| Property         | Type               | Description                                                                                                            |
|------------------|--------------------|------------------------------------------------------------------------------------------------------------------------|
| ResourceId       | string             | GUID. The id of the subscription or resource. In the context of CustomerMonthlyUsageRecord this id is the customer id. |
| ResourceName     | string             | The name of the subscription or resource. In the context of CustomerMonthlyUsageRecord this name is the customer name. |
| BillingStartDate | date               | The start date of the current billing period, in date-time format.                                                     |
| BillingEndDate   | date               | The end date of the current billing period, in date-time format.                                                       |
| TotalCost        | double             | The estimated total cost of using the resources in the subscription during the specified billing period.               |
| CurrencyLocale   | string             | The locale in which the subscription was used, determines the currency to use on the invoice.                          |
| LastModifiedDate | string             | The day, in date-time format, that this record was last modified.                                                      |
| Links            | ResourceLinks      | The resource links corresponding to the SubscriptionUsageSummary.                                                      |
| Attributes       | ResourceAttributes | The metadata attributes corresponding to the SubscriptionUsageSummary.                                                 |

 

 

 




