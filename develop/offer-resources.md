---
title: Offer resources
description: Describes a product listed in the reseller catalog that they can offer to their customers.
ms.assetid: 702B18DB-D78A-4E3B-BC8F-EFD4092131DE
ms.date: 03/15/2019
ms.service: partner-dashboard
ms.subservice:  partnercenter-sdk
ms.localizationpriority: medium
---

# Offer resources

**Applies To**

- Partner Center
- Partner Center operated by 21Vianet
- Partner Center for Microsoft Cloud Germany
- Partner Center for Microsoft Cloud for US Government

Describes a product listed in the reseller catalog that they can offer
to their customers.

## <span id="Offer"/><span id="offer"/><span id="OFFER"/>Offer

| Property                    | Type                      | Description                                                                                                                                                                |
|-----------------------------|---------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id                          | string                    | The offer identifier.                                                                                           |
| name                        | string                    | The offer name.                                                                                                 |
| description                 | string                    | A description of the offer.                                                                                     |
| minimumQuantity             | int                       | The minimum quantity available.                                                                                 |
| maximumQuantity             | int                       | The maximum quantity available.                                                                                 |
| rank                        | int                       | The offer rank or priority compared to other categories in the same product line. This property should be set only if there is more than one offer for a given product line.  |
| uri                         | string                    | The offer URI.                                                                                                  |
| locale                      | string                    | The locale in which the offer applies.                                                                          |
| country                     | string                    | The country/region  where the offer applies.                                                                    |
| category                    | [OfferCategory](#offercategory)           | The category of the offer.                                                                   |
| limitUnitOfMeasure          | string                    | A value that indicates the type of purchase limitation. Possible values include:<br/> "None" - There are no restrictions on the number of subscriptions based on the offer purchased.<br/> "Concurrent" - The number of subscriptions that can exist on the customer tenant at a given time, this includes subscriptions that are active or canceled. This value applies mostly to small business offers where license counts are less than 300. De-provisionioned subscriptions don't count.<br/> "LifeTime" - The number of subscriptions that can exist for the lifetime of the customer tenant. This value is most applicable to Trials. De-provisionioned subscriptions don't count.      |
| limit                       | int                       | The amount of subscriptions that can be purchased of this offer based on the limitUnitOfMeasure.                |
| prerequisiteOffers          | string                    | The prerequisite offers.                                                                                        |
| isAddOn                     | boolean                   | A value indicating whether this instance is an addon.                                                           |
| hasAddOns                   | boolean                   | A value indicating whether this offer has any addons.                                                           |
| isAvailableForPurchase      | boolean                   | A value indicating whether this instance is available for purchase.                                             |
| billing                     | string                    | Specifies the billing type for the line item purchase: "none", "usage", or "license".                           |
| supportedBillingCycles      | array of strings          | Indicates the billing cycles supported for this offer. Supported values are the member names found in [BillingCycleType](product-resources.md#billingcycletype)   |
| isAutoRenewable             | boolean                   | A value indicating whether the offer renews automatically.                                                      |
| upgradeTargetOffers         | array of strings          | The list of offers that this offer can be upgraded to.                                                          |
| conversionTargetOffers      | array of strings          | The list of offers that this offer can be converted to.                                                         |
| reselleeQualifications      | array of strings          | The qualifications required by the customer in order for a partner to purchase the offer for that customer.     |
| resellerQualifications      | array of strings          | The qualifications required by the partner in order to purchase the offer for a customer.                       |
| salesGroupId                | string                    | A string used to group offers into separate orders.                                                             |
| isTrial                     | boolean                   | A value indicating whether this is a trial offer.                                                               |
| product                     | [OfferProduct](#offerproduct)           | Gets the offer product.                                                                           |
| unitType                    | string                    | The type of the unit.                                                                                      |
| links                       | [OfferLinks](#offerlinks)               | The offer's "learn more" link.                                                                    |
| attributes                  | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes corresponding to the offer.                         |

## <span id="OfferCategory"/><span id="offercategory"/><span id="OFFERCATEGORY"/>OfferCategory

Describes the categorization of an offer. This includes the rank or
priority of this offer category compared to others in the same product
line.

| Property   | Type                                                           | Description                                                                                                                                                                |
|------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id         | string                                                         | The category identifier.                                                                                                                                                   |
| name       | string                                                         | The category name.                                                                                                                                                         |
| rank       | int                                                            | The category rank or priority compared to other categories in the same offer. This property should be set only if there is more than one offer category for a given offer. |
| locale     | string                                                         | The locale in which the offer applies.                                                                                                                        |
| country    | string                                                         | The country/region where the offer applies.                                                                                                                   |
| links      | [ResourceLinks](utility-resources.md#resourcelinks)           | The resource links corresponding to the OfferCategory.                                                                                                                     |
| attributes | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes corresponding to the OfferCategory.                                                                                                                |

## <span id="OfferLinks"/><span id="offerlinks"/><span id="OFFERLINKS"/>OfferLinks

Contains links for learning more information about the offer.

| Property  | Type | Description                 |
|-----------|------|-----------------------------|
| learnMore | Link | The "learn more" link.      |
| self      | Link | The self URI                |
| next      | Link | The next page of items.     |
| previous  | Link | The previous page of items. |

## <span id="OfferProduct"/><span id="offerproduct"/><span id="OFFERPRODUCT"/>OfferProduct

A product or service which may have more than one offer associated with it, each with different sets of features and targeted at different customer needs.

| Property | Type   | Description              |
|----------|--------|--------------------------|
| Id       | string | The category identifier. |
| Name     | string | The category name.       |
| Unit     | string | The product unit.        |
