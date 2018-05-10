---
title: Partner Center Analytics
description: Partner Center Analytics public API documentation.
ms.assetid: 
ms.author: v-thpr   
robots: noindex,nofollow   
ms.date: 05/10/2018
ms.topic: article
ms.prod: partner-center
ms.technology: partner-center-sdk
---

# Partner Center Analytics - Public API documentation

>[!IMPORTANT]   
>This information relates to pre-released product which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here. 

**Applies To**

-   Partner Center
-   Partner Center operated by 21Vianet
-   Partner Center for Microsoft Cloud Germany
-   Partner Center for Microsoft Cloud for US Government


The Analytics API allows you to programmatically access all the data that is being presented in the User Experience. This data is currently limited to Subscriptions in the CSP Program. In future, this API will be extended to include data from all other APIs in the CSP program, the Referral and Search Analytics API for the Referral program, and more. 

## <span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>Prerequisites


-   Credentials as described in [Partner Center authentication](partner-center-authentication.md). These scenarios support authentication with User credentials only.

## <span id="Subscription_Analytics"></span><span id="subscription_analytics"></span><span id="SUBSCRIPTION_ANALYTICS"></span>CSP Program: Subscription Analytics



The following scenarios show you how to use the Analytics API to retrieve all your Partner Center subscription analytics information, filter it with a search query, or group it by dates or terms.    

-   [Get all Subscription Analytics information](get-all-subscription-analytics.md)    
-   [Get Subscription Analytics information filtered by a search query](get-subscription-analytics-by-search-query.md)    
-   [Get Subscription Analytics information grouped by dates or terms](get-subscription-analytics-grouped-by-dates-or-terms.md)    

All of these scenarios return your analytics information in a collection of [Subscription](#subscription) resources. 


## <span id="Subscription"></span><span id="subscription"></span><span id="SUBSCRIPTION"></span>Subscription Resource


Represents all of the analytical data for a subscription.
 
| Property                  | Type                              | Description                                                                             |
|---------------------------|-----------------------------------|-----------------------------------------------------------------------------------------|
| customerTenantId          | string                            | A GUID-formatted string that identifies the customer tenant.                            |
| customerName              | string                            | The name of the customer.                                                               |
| customerMarket            | string                            | The country/region that the customer does business in.                                  |
| id                        | string                            | The subscription identifier.                                                            |
| status                    | string                            | The subscription status:  "ACTIVE", "SUSPENDED", or "DEPROVISIONED".                    |
| productName               | string                            | The name of the product.                                                                |
| subscriptionType          | string                            | The subscription type. **Note**: This field is case sensitive. Supported values are: "Office", "Azure", "Microsoft365", "Dynamics", "EMS".  |
| autoRenewEnabled          | boolean                           | A value indicating whether the subscription is renewed automatically.                   |
| partnerId                 | string                            | The MPN ID. For a direct reseller, this will be the MPN ID of the partner. For an indirect reseller, this will be the MPN ID of the indirect reseller.  |
| friendlyName              | string                            | The name of the subscription.                                                           |
| creationDate              | string in UTC date time format    | The date the subscription was created.                                                  |
| effectiveStartDate        | string in UTC date time format    | The date the subscription starts.                                                       |
| commitmentEndDate         | string in UTC date time format    | The date the subscription ends.                                                         |
| currentStateEndDate       | string in UTC date time format    | The date that the current status of the subscription will change.                       |
| trialToPaidConversionDate | string in UTC date time format    | The date that the subscription converts from trial to paid. The default value is null.  |
| trialStartDate            | string in UTC date time format    | The date that the trial period for the subscription started. The default value is null. |
| trialEndDate              | string in UTC date time format    | The date that the trial period for the subscription ends. The default value is null.    |
| lastUsageDate             | string in UTC date time format    | The date that the subscription was last used. The default value is null.                |
| deprovisionedDate         | string in UTC date time format    | The date that the subscription was deprovisioned. The default value is null.            |
| lastRenewalDate           | string in UTC date time format    | The date that the subscription was last renewed The default value is null.              |
| licenseCount              | number                            | The total number of licenses.                                                           |
| subscriptionCount         | number                            | The number of subscriptions. Note: This value will only appear in the response of an aggregation query.  |
