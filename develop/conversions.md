---
title: Conversions
description: 
    Conversion resources support the conversion of a trial subscription to a
    paid subscription.
ms.assetid: 4AE796E3-47D9-428B-8267-A5247B573E0C
ms.author: v-thpr
ms.date: 12/15/2017
ms.topic: article
ms.prod: partner-center
ms.technology: partner-center-sdk
---

# Conversions


<span class="sidebar_heading" style="font-weight: bold;">Applies
To</span>

-   Partner Center
-   Partner Center operated by 21Vianet
-   Partner Center for Microsoft Cloud Germany
-   Partner Center for Microsoft Cloud for US Government

Conversion resources support the conversion of a trial subscription to a
paid subscription.

## <span id="Conversion"></span><span id="conversion"></span><span id="CONVERSION"></span>Conversion


Contains information used to convert a trial subscription to a paid
subscription.

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
<td>offerId</td>
<td>string</td>
<td>The offer identifier of the original, trial offer.</td>
</tr>
<tr class="even">
<td>targetOfferId</td>
<td>string</td>
<td>The offer identifier for the target offer.</td>
</tr>
<tr class="odd">
<td>orderId</td>
<td>string</td>
<td>The order identifier.</td>
</tr>
<tr class="even">
<td>quantity</td>
<td>int</td>
<td>The number of licenses. The default is the number of licenses in the trial subscription.</td>
</tr>
<tr class="odd">
<td>billingCycle</td>
<td>string</td>
<td>Indicates how often the partner is charged for the subscription. Possible values:
<p>Monthly - Partner is billed monthly.</p>
<p>Annual - Partner is billed annually.</p>
<p>None - Partner is not billed. Used for trial subscriptions.</p></td>
</tr>
</tbody>
</table>

 

## <span id="ConversionError"></span><span id="conversionerror"></span><span id="CONVERSIONERROR"></span>ConversionError


Represents an error that occurred during conversion.

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
<td>code</td>
<td>string</td>
<td>The error code associated with the issue. Possible values:
<p>Other - General error.</p>
<p>ConversionsNotFound - Cannot find any conversions for the trial subscription to convert to.</p></td>
</tr>
<tr class="even">
<td>description</td>
<td>string</td>
<td>The friendly text describing the issue.</td>
</tr>
</tbody>
</table>

 

## <span id="ConversionResult"></span><span id="conversionresult"></span><span id="CONVERSIONRESULT"></span>ConversionResult


Represents the result of performing a subscription conversion.

| Property       | Type                                | Description                                                            |
|----------------|-------------------------------------|------------------------------------------------------------------------|
| subscriptionId | string                              | The subscription identifier.                                           |
| offerId        | string                              | The original offer identifier.                                         |
| targetOfferId  | string                              | The offer identifier for the target offer.                             |
| error          | [ConversionError](#conversionerror) | The error encountered while attempting the conversion, if applicable.. |

 

 

 




