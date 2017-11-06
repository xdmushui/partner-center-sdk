---
title: ServiceCosts
description: Describes resources related to services purchased by a customer.
MSHAttr:
- 'PreferredSiteName:MSDN'
- 'PreferredLib:/library/PartnerCenter'
ms.assetid: 2916B7F3-06D5-4DC1-A137-CD8270258CDB
---

# ServiceCosts


**Applies To**

-   Partner Center

Describes resources related to services purchased by a customer.

## <span id="ServiceCostsSummary"></span><span id="servicecostssummary"></span><span id="SERVICECOSTSSUMMARY"></span>ServiceCostsSummary


Contains a summary that aggregates all services purchased by the specified customer during the billing period.

| Property         | Type                                                           | Description                                                      |
|------------------|----------------------------------------------------------------|------------------------------------------------------------------|
| billingStartDate | date                                                           | The start of the billing period.                                 |
| billingEndDate   | date                                                           | The end of the billing period.                                   |
| pretaxTotal      | double                                                         | The pre-tax total of all costs for the customer.                 |
| tax              | double                                                         | The total tax incurred over all items purchased by the customer. |
| afterTaxTotal    | double                                                         | The net total cost for all items purchased by the customer.      |
| currencyCode     | string                                                         | Represents the currency used for the costs.                      |
| currencySymbol   | string                                                         | The currency symbol used for the costs.                          |
| customerId       | string                                                         | The id of the customer making the purchase.                      |
| links            | [ResourceLinks](utility-resources.md#resourcelinks)           | The resource links.                                              |
| attributes       | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes.                                         |

 

## <span id="ServiceCostLineItem"></span><span id="servicecostlineitem"></span><span id="SERVICECOSTLINEITEM"></span>ServiceCostLineItem


Describes a single item purchased by the customer.

| Property                 | Type                           | Description                                                          |
|--------------------------|--------------------------------|----------------------------------------------------------------------|
| startDate                | string in UTC date-time format | The start date for the charge.                                       |
| endDate                  | string in UTC date-time format | The end date for the charge.                                         |
| subscriptionFriendlyName | string                         | The friendly name for the subscription.                              |
| subscriptionId           | string                         | The subscription identifier.                                         |
| orderId                  | string                         | The order identifier.                                                |
| offerId                  | string                         | The offer identifier.                                                |
| offerName                | string                         | The offer name.                                                      |
| resellerMPNId            | string                         | Only used in 2-tier partner scenarios. Refers to the MPN identifier. |
| chargeType               | string                         | The associated charge type.                                          |
| quantity                 | number                         | The quantity of units used or purchased.                             |
| unitPrice                | number                         | The price per unit.                                                  |
| pretaxTotal              | number                         | The total charge for this item before taxes.                         |
| tax                      | number                         | The total tax charge incurred for this item.                         |
| afterTaxTotal            | number                         | The net total cost for this item.                                    |
| currencyCode             | string                         | Represents the currency used for the costs.                          |
| currencySymbol           | string                         | The currency symbol used for the costs.                              |
| customerId               | string                         | The id of the customer making the purchase.                          |
| customerName             | string                         | The name of the customer making the purchase.                        |

 

## <span id="ServiceCostsSummaryLinks"></span><span id="servicecostssummarylinks"></span><span id="SERVICECOSTSSUMMARYLINKS"></span>ServiceCostsSummaryLinks


| Property             | Type                               | Description                         |
|----------------------|------------------------------------|-------------------------------------|
| serviceCostLineItems | [Link](utility-resources.md#link) | The URI to retrieve the line items. |
| self                 | [Link](utility-resources.md#link) | The self URI.                       |

 

 

 




