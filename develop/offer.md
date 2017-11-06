---
title: Offer
description: Describes a product listed in the reseller catalog that they can offer to their customers.
MSHAttr:
- 'PreferredSiteName:MSDN'
- 'PreferredLib:/library/PartnerCenter'
ms.assetid: 702B18DB-D78A-4E3B-BC8F-EFD4092131DE
---

# Offer


**Applies To**

-   Partner Center
-   Partner Center operated by 21Vianet
-   Partner Center for Microsoft Cloud Germany
-   Partner Center for Microsoft Cloud for US Government

Describes a product listed in the reseller catalog that they can offer to their customers.

## <span id="Offer"></span><span id="offer"></span><span id="OFFER"></span>Offer


<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>Property</th>
<th>Type</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>id</td>
<td>string</td>
<td>The offer identifier.</td>
</tr>
<tr class="even">
<td>name</td>
<td>string</td>
<td>The offer name.</td>
</tr>
<tr class="odd">
<td>description</td>
<td>string</td>
<td>A description of the offer.</td>
</tr>
<tr class="even">
<td>minimumQuantity</td>
<td>int</td>
<td>The minimum quantity available.</td>
</tr>
<tr class="odd">
<td>maximumQuantity</td>
<td>int</td>
<td>The maximum quantity available.</td>
</tr>
<tr class="even">
<td>rank</td>
<td>int</td>
<td>The offer rank or priority compared to other categories in the same product line. This property should be set only if there is more than one offer for a given product line.</td>
</tr>
<tr class="odd">
<td>uri</td>
<td>string</td>
<td>The offer URI.</td>
</tr>
<tr class="even">
<td>locale</td>
<td>string</td>
<td>Gets or sets the locale in which the offer applies.</td>
</tr>
<tr class="odd">
<td>country</td>
<td>string</td>
<td>Gets or sets the country/region where the offer applies.</td>
</tr>
<tr class="even">
<td>category</td>
<td>[OfferCategory](pc_apiv2.offercategory)</td>
<td>Gets or sets the category.</td>
</tr>
<tr class="odd">
<td>prerequisiteOffers</td>
<td>string</td>
<td>Gets or sets the prerequisite offers.</td>
</tr>
<tr class="even">
<td>isAddOn</td>
<td>boolean</td>
<td>Gets or sets a value indicating whether this instance is addon.</td>
</tr>
<tr class="odd">
<td>isAvailableForPurchase</td>
<td>boolean</td>
<td>Gets or sets a value indicating whether this instance is available for purchase.</td>
</tr>
<tr class="even">
<td>billing</td>
<td>string</td>
<td>Specifies the billing type for the line item purchase: &quot;none&quot;, &quot;usage&quot;, or &quot;license&quot;.</td>
</tr>
<tr class="odd">
<td>supportedBillingCycles</td>
<td>array of strings</td>
<td>Indicates the billing cycles supported for this offer. Supported values are the member names found in [<strong>BillingCycleType</strong>](pc_sdk_models_offers.billingcycletype).
<div class="alert">
<strong>Note</strong>  The annual billing feature is not yet generally available. Support for annual billing is coming soon.
</div>
<div>
 
</div></td>
</tr>
<tr class="even">
<td>isAutoRenewable</td>
<td>boolean</td>
<td>Gets or sets a value indicating whether the offer renews automatically.</td>
</tr>
<tr class="odd">
<td>upgradeTargetOffers</td>
<td>array of strings</td>
<td>Gets or sets the list of offers that this offer can be upgraded to.</td>
</tr>
<tr class="even">
<td>conversionTargetOffers</td>
<td>array of strings</td>
<td>Gets or sets the list of offers that this offer can be converted to.</td>
</tr>
<tr class="odd">
<td>partnerQualifications</td>
<td>array of strings</td>
<td>A partner must be qualified to sell at least one of the specified offer types to get the specific offer, such as &quot;none&quot;, &quot;syndication&quot;, &quot;education&quot;, &quot;nonprofit&quot;, or &quot;government&quot;. If no qualifications are specified, then the offer is available to all partners.</td>
</tr>
<tr class="even">
<td>product</td>
<td>[Product](product.md)</td>
<td>Gets or sets the product.</td>
</tr>
<tr class="odd">
<td>unitType</td>
<td>string</td>
<td>Gets or sets the type of the unit.</td>
</tr>
<tr class="even">
<td>links</td>
<td>[OfferLinks](#offerlinks)</td>
<td>The offer's &quot;lean more&quot; link.</td>
</tr>
<tr class="odd">
<td>attributes</td>
<td>[ResourceAttributes](utility-resources.md#resourceattributes)</td>
<td>The metadata attributes corresponding to the offer.</td>
</tr>
</tbody>
</table>

 

## <span id="OfferCategory"></span><span id="offercategory"></span><span id="OFFERCATEGORY"></span>OfferCategory


Describes the categorization of an offer. This includes the rank or priority of this offer category compared to others in the same product line.

| Property   | Type                                                           | Description                                                                                                                                                                |
|------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id         | string                                                         | The category identifier.                                                                                                                                                   |
| name       | string                                                         | The category name.                                                                                                                                                         |
| rank       | int                                                            | The category rank or priority compared to other categories in the same offer. This property should be set only if there is more than one offer category for a given offer. |
| locale     | string                                                         | Gets or sets the locale in which the offer applies.                                                                                                                        |
| country    | string                                                         | Gets or sets the country/region where the offer applies.                                                                                                                   |
| links      | [ResourceLinks](utility-resources.md#resourcelinks)           | The resource links corresponding to the OfferCategory.                                                                                                                     |
| attributes | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes corresponding to the OfferCategory.                                                                                                                |

 

## <span id="OfferLinks"></span><span id="offerlinks"></span><span id="OFFERLINKS"></span>OfferLinks


Contains links for learning more information about the offer.

| Property  | Type | Description                 |
|-----------|------|-----------------------------|
| learnMore | Link | The "learn more" link.      |
| self      | Link | The self URI                |
| next      | Link | The next page of items.     |
| previous  | Link | The previous page of items. |

 

 

 




