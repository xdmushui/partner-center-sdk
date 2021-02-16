---
title: Conversion resources
description: Learn about using Partner Center API Conversion resources to help you convert a trial subscription to a paid subscription.
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice:  partnercenter-sdk
---

# Conversion resources to convert trial subscriptions to paid

**Applies to:**

- Partner Center
- Partner Center operated by 21Vianet
- Partner Center for Microsoft Cloud Germany
- Partner Center for Microsoft Cloud for US Government

Conversion resources support the conversion of a trial subscription to a paid subscription.

## Conversion

Contains information used to convert a trial subscription to a paid subscription.

| Property | Type | Description |
| -------- | ---- | ----------- |
| offerId | string | The offer identifier of the original, trial offer. |
| targetOfferId | string | The offer identifier for the target offer. |
| orderId | string | The order identifier. |
| quantity | int | The number of licenses. The default is the number of licenses in the trial subscription. |
| billingCycle | string | Indicates how often the partner is charged for the subscription. Possible values: **Monthly** (partner is billed monthly), **Annual** (partner is billed annually), or **None** (Partner isn't billed. Used for trial subscriptions). |

## ConversionError

Represents an error that occurred during conversion.

| Property | Type | Description |
| -------- | ---- | ----------- |
| code | string | The error code associated with the issue. Possible values: **Other** (general error), **ConversionsNotFound** (can't find any conversions for the trial subscription to convert to).
| description | string | The friendly text describing the issue. |

## ConversionResult

Represents the result of performing a subscription conversion.

| Property       | Type                                | Description                                                            |
|----------------|-------------------------------------|------------------------------------------------------------------------|
| subscriptionId | string                              | The subscription identifier.                                           |
| offerId        | string                              | The original offer identifier.                                         |
| targetOfferId  | string                              | The offer identifier for the target offer.                             |
| error          | [ConversionError](#conversionerror) | The error encountered while attempting the conversion, if applicable.. |