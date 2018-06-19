---
title: Partner Center Analytics
description: Partner Center Analytics public API documentation.
author: Xansky
ms.author: mhopkins 
ms.assetid: B605C1CD-FC40-4393-8588-55C8F0CAA51A
robots: noindex,nofollow 
ms.date: 06/11/2018
ms.topic: article
ms.prod: partner-center
ms.technology: partner-center-sdk
---

# Partner Center Analytics - Public API documentation

>[!IMPORTANT] 
>This information relates to pre-released product which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here. 

**Applies To**

- Partner Center
- Partner Center operated by 21Vianet
- Partner Center for Microsoft Cloud Germany
- Partner Center for Microsoft Cloud for US Government


The Analytics API allows you to programmatically access data that is being presented in the User Experience. 

## <span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>Prerequisites


- Credentials as described in [Partner Center authentication](partner-center-authentication.md). These scenarios support authentication with User credentials only.

## <span id="Subscription_Analytics"></span><span id="subscription_analytics"></span><span id="SUBSCRIPTION_ANALYTICS"></span>CSP program: subscription analytics



The following scenarios show you how to use the Analytics API to retrieve all your Partner Center subscription analytics information, filter it with a search query, or group it by dates or terms.  

- [Get all subscription analytics information](get-all-subscription-analytics.md)  
- [Get subscription analytics information filtered by a search query](get-subscription-analytics-by-search-query.md)  
- [Get subscription analytics information grouped by dates or terms](get-subscription-analytics-grouped-by-dates-or-terms.md)  

All of these scenarios return your analytics information in a collection of [Subscription](#subscription) resources. 


## <span id="Subscription"></span><span id="subscription"></span><span id="SUBSCRIPTION"></span>Subscription resource


Represents all of the analytical data for a subscription.
 
| Property                  | Type                              | Description |
|---------------------------|-----------------------------------|-------------|
| customerTenantId          | string                         | A GUID-formatted string that identifies the customer tenant.                            |
| customerName              | string                         | The name of the customer.                                                               |
| customerMarket            | string                         | The country/region that the customer does business in.                                  |
| id                        | string                         | The subscription identifier.                                                            |
| status                    | string                         | The subscription status: "ACTIVE", "SUSPENDED", or "DEPROVISIONED".                    |
| productName               | string                         | The name of the product.                                                                |
| subscriptionType          | string                         | The subscription type. **Note**: This field is case sensitive. Supported values are: "Office", "Azure", "Microsoft365", "Dynamics", "EMS".  |
| autoRenewEnabled          | boolean                        | A value indicating whether the subscription is renewed automatically.                   |
| partnerId                 | string                         | The MPN ID. For a direct reseller, this will be the MPN ID of the partner. For an indirect reseller, this will be the MPN ID of the indirect reseller.  |
| friendlyName              | string                         | The name of the subscription.                                                           |
| creationDate              | string in UTC date time format | The date the subscription was created.                                                  |
| effectiveStartDate        | string in UTC date time format | The date the subscription starts.                                                       |
| commitmentEndDate         | string in UTC date time format | The date the subscription ends.                                                         |
| currentStateEndDate       | string in UTC date time format | The date that the current status of the subscription will change.                       |
| trialToPaidConversionDate | string in UTC date time format | The date that the subscription converts from trial to paid. The default value is null.  |
| trialStartDate            | string in UTC date time format | The date that the trial period for the subscription started. The default value is null. |
| trialEndDate              | string in UTC date time format | The date that the trial period for the subscription ends. The default value is null.    |
| lastUsageDate             | string in UTC date time format | The date that the subscription was last used. The default value is null.                |
| deprovisionedDate         | string in UTC date time format | The date that the subscription was deprovisioned. The default value is null.            |
| lastRenewalDate           | string in UTC date time format | The date that the subscription was last renewed The default value is null.              |
| licenseCount              | number                         | The total number of licenses.                                                           |
| subscriptionCount         | number                         | The number of subscriptions. Note: This value will only appear in the response of an aggregation query.  |


## <span id="Azure_Usage_Analytics"></span><span id="azure_usage_analytics"></span><span id="AZURE_USAGE_ANALYTICS"></span>CSP program: search analytics

The following scenario shows you how to use the Analytics API to retrieve all your Partner Center Azure usage analytics information.  

- [Get all Azure usage analytics information](get-all-azure-usage-analytics.md)  

This scenario returns your analytics information in a collection of [Azure usage](#azure_usage) resources. 

## <span id="Azure-Usage"></span><span id="azure-usage"></span><span id="AZURE-USAGE"></span>Azure usage resource

Accessing Azure usage data is similar to the [subscription analytics](#subscription_analytics) scenario but using the Azure usage resource described here.

Represents all of the analytical data for Azure usage.
 
| Property              | Type   | Description                    |
|-----------------------|--------|--------------------------------|
| CustomerTenantId      | string | The customer tenant identifier |
| customerName          | string | The customer name              |
| subscriptionId        | string | The subscription identifier    |
| subscriptionName      | string | The subscription name          |
| usageDate             | string | The usage date                 |
| resourceLocation      | string | The location of the data center, Western Europe, for example. |
| meterCategory         | string | The meter category, data management, for example. |
| meterSubcategory      | string | The meter subcategory, ror example, geo redundant. | 
| meterUnit             | string | The meter unit, such as gigabytes or hours. | 
| reservationOrderId    | string | The reservation order for an Azure VM Reserved Instance. |
| reservationId | string | Reserved instances under a specific RI order. |
| serviceType           | string | Indicates the virtual machine type. For example, Standard_E4s_v3. |
| quantity              | long   | Indicates the numbers used in the meter unit. | 


## <span id="Indirect_Resellers_Analytics"></span><span id="indirect_resellers_analytics"></span><span id="INDIRECT_RESELLERS_ANALYTICS"></span>CSP program: indirect resellers analytics

The following scenario shows you how to use the Analytics API to retrieve all your Partner Center indirect resellers analytics information.  

- [Get all indirect resellers analytics information](get-all-indirect-resellers-analytics.md)  

This scenario returns your analytics information in a collection of [indirect resellers](#indirect_resellers) resources. 


## <span id="Indirect_Resellers"></span><span id="indirect_resellers"></span><span id="IDIRECT_RESELLERS"></span>Indirect resellers resource

Accessing indirect resellers data is similar to the [subscription analytics](#subscription_analytics) scenario but using the indirect reseller resource described here.

Represents all of the analytical data for indirect resellers.
 
| Property | Type | Description |
|----------|------|-------------|
| partnerTenantId | string | The Tenant ID of the partner for which you want to retrieve indirect resellers data. |
| id | string | Indirect reseller ID |
| name | string | The Name of the partner for which you want to retrieve indirect resellers data. |
| market | string | The Market of the partner for which you want to retrieve indirect resellers data. |
| firstSubscriptionCreationDate | date | The creation date of the first subscription based on which you want to retrieve indirect resellers data. |
| latestSubscriptionCreationDate | Date | The creation date of the latest subscription. |
| firstSubscriptionEndDate | Date | First time any subscription was ended. |
| latestSubscriptionEndDate | Date | Latest date when any subscription was ended. |
| firstSubscriptionSuspendedDate | Date | First time any subscription was suspended. |
| latestSubscriptionSuspendedDate | Date | Latest date when any subscription was suspended. |
| firstSubscriptionDeprovisionedDate | Date | First time any subscription was deprovisioned. |
| latestSubscriptionDeprovisionedDate | Date | Latest date when any subscription was deprovisioned. |
| subscriptionCount | Double | Subscription count for all value added resellers |
| licenseCount | Double | License count for all value added resellers |
| indirectResellerCount | Double | Indirect resellers count |


## <span id="Search_Analytics"></span><span id="search_analytics"></span><span id="SEARCH_ANALYTICS"></span>Search analytics

CSP program membership is not required for search analytics.

The following scenario shows you how to use the Analytics API to retrieve all your Partner Center search analytics information.  

- [Get all search analytics information](get-all-search-analytics.md)  

This scenario returns your analytics information in a collection of [Search](#search) resources. 


## <span id="Search"></span><span id="search"></span><span id="SEARCH"></span>Search resource

Represents all of the analytical data for a search.

| Property | Type | Description |  
|----------|------|-------------|  
| companyName | string | The billing company name. |
| industryFocus	| string | The industry to search within, for example, healthcare. |
| mpnId | string | The MPN ID. For a direct reseller, this will be the MPN ID of the partner. For an indirect reseller, this will be the MPN ID of the indirect reseller. |
| partnerMarket | string |   |
| searchDate | date | Date key for showing |
| searchResultPageViews | long | Number of times the partner came up in the search result |
| contactClicks | long | Number of times the contact button was clicked. |
| referralCount | long | Number of referral generated from the search |
| profileViews | long |  |


## <span id="Referral_Analytics"></span><span id="referral_analytics"></span><span id="REFERRAL_ANALYTICS"></span>Referral analytics

CSP program membership is not required for referral analytics.

The following scenario shows you how to use the Analytics API to retrieve all your Partner Center referral analytics information.  

- [Get all referral analytics information](get-all-referral-analytics.md)  

This scenario returns your analytics information in a collection of [Referral](#referral) resources. 

> [!NOTE] Referral analytics are not available to the Partner Center operated by 21Vianet. 


## <span id="Referral"></span><span id="referral"></span><span id="REFERRAL"></span>Referral resource

Represents all of the analytical data for a referral.
 
| Property | Type | Description |
|----------|------|-------------|
| id | string |   |
| status | string |  |
| customerMarket | string |  |
| customerName | string |
| customerOrgSize | string |
| acceptedDate | date |  |
| acknowledgedDate | date |  |
| archivedDate | date |  |
| declinedDate | date |  |
| expiredDate | date |  |
| lostDate | date |  |
| missedDate | date |  |
| createdDate | date |  |
| skippedDate | date |  |
| wonDate | date |  |
| partnerMarket | string |  |
| partnerTenantId | string |
| referralCount | long |  |
