---
title: Order
description: 
    A partner places an order when a customer wants to buy a subscription
    from a list of offers.
ms.assetid: 5CFA35FF-1C0D-461D-A942-309AFCD98395
ms.author: v-thpr
ms.date: 12/15/2017
ms.topic: article
ms.prod: partner-center
ms.technology: partner-center-sdk
---

# Order


<span class="sidebar_heading" style="font-weight: bold;">Applies
To</span>

-   Partner Center
-   Partner Center operated by 21Vianet
-   Partner Center for Microsoft Cloud Germany
-   Partner Center for Microsoft Cloud for US Government

A partner places an order when a customer wants to buy a subscription
from a list of offers.

**Note** The Order resource has a rate limit of 500 requests per minute per tenant identifier.


## <span id="order"></span><span id="ORDER"></span>Order


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
<td>The order identifier.</td>
</tr>
<tr class="even">
<td>referenceCustomerId</td>
<td>string</td>
<td>The customer identifier.</td>
</tr>
<tr class="odd">
<td>lineItems</td>
<td>array of [OrderLineItem](#orderlineitem) resources</td>
<td>An itemized list of the offers the customer is purchasing and the quantity.</td>
</tr>
<tr class="even">
<td>billingCycle</td>
<td>string</td>
<td>Indicates the frequency with which the partner is billed for this order. Supported values are the member names found in [<strong>BillingCycleType</strong>](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.offers.billingcycletype). The default is &quot;Monthly&quot; at order creation. This field is applied upon successful creation of the order.
<div class="alert">
<strong>Note</strong>  The annual billing feature is not yet generally available. Support for annual billing is coming soon.
</div>
<div>
 
</div></td>
</tr>
<tr class="odd">
<td>creationDate</td>
<td>string</td>
<td>The date the order was created, in date-time format.</td>
</tr>
<tr class="even">
<td>links</td>
<td>[ResourceLinks](utility-resources.md#resourcelinks)</td>
<td>The resource links corresponding to the Order.</td>
</tr>
<tr class="odd">
<td>attributes</td>
<td>[ResourceAttributes](utility-resources.md#resourceattributes)</td>
<td>The metadata attributes corresponding to the Order.</td>
</tr>
</tbody>
</table>

 

## <span id="orderLineItem"></span><span id="orderlineitem"></span><span id="ORDERLINEITEM"></span>OrderLineItem


An order contains an itemized list of offers, and each item is
represented as an OrderLineItem.

| Property             | Type                                      | Description                                                                                                                                                                                                                                |
|----------------------|-------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| lineItemNumber       | int                                       | Each line item in the collection gets a unique line number, counting up from 0 to count-1.                                                                                                                                                 |
| offerId              | string                                    | The ID of the offer.                                                                                                                                                                                                                       |
| subscriptionId       | string                                    | The ID of the subscription.                                                                                                                                                                                                                |
| parentSubscriptionId | string                                    | Optional. The ID of the parent subscription in an add-on offer. Applies to PATCH only.                                                                                                                                                     |
| friendlyName         | string                                    | Optional. The friendly name for the subscription defined by the partner to help disambiguate.                                                                                                                                              |
| quantity             | int                                       | The number of licenses for a licence-based subscription.                                                                                                                                                                                   |
| partnerIdOnRecord    | string                                    | When an indirect provider places an order on behalf of an indirect reseller, populate this field with the MPN ID of the **indirect reseller only** (never the ID of the indirect provider). This ensures proper accounting for incentives. |
| links                | [OrderLineItemLinks](#orderlineitemlinks) | Read-only. Gets the order's resulting contract information.                                                                                                                                                                                |

 

## <span id="orderLineItemLinks"></span><span id="orderlineitemlinks"></span><span id="ORDERLINEITEMLINKS"></span>OrderLineItemLinks


Represents the full subscription associated with the order.

| Property     | Type                                         | Description                                    |
|--------------|----------------------------------------------|------------------------------------------------|
| subscription | [Link](utility-resources.md#Link) | The link to the full subscription information. |

 

 

 




