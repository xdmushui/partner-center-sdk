---
title: Subscription
description: 
    A subscription lets a customer use a service for a certain period of
    time.
ms.assetid: E99B5EC3-2247-4CAD-B651-3000E36AF6B6
ms.author: v-thpr
ms.date: 12/15/2017
ms.topic: article
ms.prod: partner-center
ms.technology: partner-center-sdk
---

# Subscription


<span class="sidebar_heading" style="font-weight: bold;">Applies
To</span>

-   Partner Center
-   Partner Center operated by 21Vianet
-   Partner Center for Microsoft Cloud Germany
-   Partner Center for Microsoft Cloud for US Government

A subscription lets a customer use a service for a certain period of
time. Not all fields will apply to all subscriptions, and many only
apply at certain points in the life cycle, such as if a subscription is
suspended or cancelled.

## <span id="Subscription"></span><span id="subscription"></span><span id="SUBSCRIPTION"></span>Subscription


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
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
<td>The subscription identifier.</td>
</tr>
<tr class="even">
<td>offerId</td>
<td>string</td>
<td>The offer identifier.</td>
</tr>
<tr class="odd">
<td>offerName</td>
<td>string</td>
<td>The offer name.</td>
</tr>
<tr class="even">
<td>friendlyName</td>
<td>string</td>
<td>The friendly name for the subscription defined by the partner to help disambiguate.</td>
</tr>
<tr class="odd">
<td>quantity</td>
<td>number</td>
<td>Read-only. The quantity. For example, in case of license-based billing, this property is set to the license count.</td>
</tr>
<tr class="even">
<td>unitType</td>
<td>string</td>
<td>The units defining Quantity for the subscription.</td>
</tr>
<tr class="odd">
<td>parentSubscriptionId</td>
<td>string</td>
<td>Gets or sets the parent subscription identifier.</td>
</tr>
<tr class="even">
<td>creationDate</td>
<td>string</td>
<td>Gets or sets the creation date, in date-time format.</td>
</tr>
<tr class="odd">
<td>effectiveStartDate</td>
<td>string in UTC date time format</td>
<td>Gets or sets the effective start date for this subscription, in date-time format. It is used to back date a migrated subscription or to align it with another.</td>
</tr>
<tr class="even">
<td>commitmentEndDate</td>
<td>string in UTC date time format</td>
<td>The commitment end date for this subscription, in date-time format. For subscriptions which are not autorenewable, this represents a date far, far away in the future.</td>
</tr>
<tr class="odd">
<td>status</td>
<td>string</td>
<td>The subscription status: &quot;none&quot;, &quot;active&quot;, &quot;suspended&quot;, or &quot;deleted&quot;.</td>
</tr>
<tr class="even">
<td>autoRenewEnabled</td>
<td>boolean</td>
<td>Gets or sets a value indicating whether the subscription is renewed automatically.</td>
</tr>
<tr class="odd">
<td>billingType</td>
<td>string</td>
<td>Specifies how the subscription is billed: &quot;none&quot;, &quot;usage&quot;, or &quot;license&quot;.</td>
</tr>
<tr class="even">
<td>billingCycle</td>
<td>string</td>
<td>Indicates the frequency with which the partner is billed for this order. Supported values are the member names found in [<strong>BillingCycleType</strong>](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.offers.billingcycletype).
<div class="alert">
<strong>Note</strong>  The annual billing feature is not yet generally available. Support for annual billing is coming soon.
</div>
<div>
 
</div></td>
</tr>
<tr class="odd">
<td>partnerId</td>
<td>string</td>
<td>MPN ID of the reseller of record, used in the indirect partner model.</td>
</tr>
<tr class="even">
<td>suspensionReasons</td>
<td>array of strings</td>
<td>Read-only. If the subscription was suspended, indicates why.</td>
</tr>
<tr class="odd">
<td>contractType</td>
<td>string</td>
<td>Read-only. The type of contract: &quot;subscription&quot;, &quot;productKey&quot;, or &quot;redemptionCode&quot;.</td>
</tr>
<tr class="even">
<td>links</td>
<td>[SubscriptionLinks](#subscriptionlinks)</td>
<td>Gets or sets the subscription links.</td>
</tr>
<tr class="odd">
<td>orderId</td>
<td>string</td>
<td>The id of the order that was placed to begin the subscription.</td>
</tr>
<tr class="even">
<td>attributes</td>
<td>[ResourceAttributes](utility-resources.md#resourceattributes)</td>
<td>The metadata attributes corresponding to the subscription.</td>
</tr>
</tbody>
</table>

 

## <span id="SubscriptionLinks"></span><span id="subscriptionlinks"></span><span id="SUBSCRIPTIONLINKS"></span>SubscriptionLinks


Describes the collection of links attached to a subscription resource.

| Property           | Type                               | Description                           |
|--------------------|------------------------------------|---------------------------------------|
| offer              | [Link](utility-resources.md#link) | Gets or sets the offer.               |
| parentSubscription | [Link](utility-resources.md#link) | Gets or sets the parent subscription. |
| self               | [Link](utility-resources.md#link) | The self URI.                         |
| next               | [Link](utility-resources.md#link) | The next page of items.               |
| previous           | [Link](utility-resources.md#link) | The previous page of items.           |

 

## <span id="SubscriptionProvisioningStatus"></span><span id="subscriptionprovisioningstatus"></span><span id="SUBSCRIPTIONPROVISIONINGSTATUS"></span>SubscriptionProvisioningStatus


Provides information about the provisioning status of a subscription.

| Property   | Type                                                           | Description                                                          |
|------------|----------------------------------------------------------------|----------------------------------------------------------------------|
| skuId      | string                                                         | A GUID formatted string that identifies the product SKU.             |
| status     | string                                                         | Indicates the provisioning status: "success", "pending" or "failed". |
| quantity   | number                                                         | Provides the subscription quantity after provisioning.               |
| endDate    | string in UTC date time format                                 | The end date of the subscription.                                    |
| attributes | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes.                                             |

 

## <span id="SupportContact"></span><span id="supportcontact"></span><span id="SUPPORTCONTACT"></span>SupportContact


Represents a support contact for a customer's subscription.

| Property        | Type                                                           | Description                                                                     |
|-----------------|----------------------------------------------------------------|---------------------------------------------------------------------------------|
| supportTenantId | string                                                         | A GUID formatted string that indicates the support contact's tenant identifier. |
| supportMpnId    | string                                                         | The contact's Microsoft Partner Network (MPN) identifier.                       |
| name            | string                                                         | The name of the support contact.                                                |
| links           | [ResourceLinks](utility-resources.md#resourcelinks)           | The support contact related links.                                              |
| attributes      | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes. Contains "objectType": " SupportContact".              |

 

 

 




