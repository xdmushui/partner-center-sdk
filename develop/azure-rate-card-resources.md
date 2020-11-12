---
title: Azure rate card - current Azure pricing
description: Learn how to use the Azure Rate Card to get real-time, current prices for Azure offers in your region. Azure Rate Card is accessed via Partner Center REST API.
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice:  partnercenter-sdk
author: amitravat
ms.author: amrava
---

# Azure rate card resources to get real-time, current Azure prices on Azure offers in your region

**Applies to:**

- Partner Center
- Partner Center for Microsoft Cloud Germany
- Partner Center for Microsoft Cloud for US Government

The Azure Rate Card provides real-time prices for Azure offers. Azure pricing is quite dynamic and changes frequently. Microsoft publishes updates on Partner Center, but the REST API provides the fastest way for Cloud Solution Provider partners to get current prices.

To track usage and help predict your monthly bill and the bills for individual customers, you can combine a Rate Card query to [Get prices for Microsoft Azure](get-prices-for-microsoft-azure.md) with a request to [Get a customer's utilization records for Azure](get-a-customer-s-utilization-record-for-azure.md).

Prices differ by market and currency, and this API takes location into consideration. By default, the API uses your partner profile settings in Partner Center and your browser language, and those settings are customizable. The location awareness is especially relevant if you manage sales in multiple markets from a single, centralized office.

## AzureRateCard

Describes the properties of an Azure Rate Card resource.

| Property      | Type                                      | Description                                                       |
|---------------|-------------------------------------------|-------------------------------------------------------------------|
| currency      | string                                    | The currency in which the rates are provided.                     |
| isTaxIncluded | boolean                                   | All rates are pretax, so this property returns as `false`. |
| locale        | string                                    | The culture in which the resource information is localized.       |
| meters        | array of objects                          | Array of [AzureMeter](#azuremeter) objects.                       |
| offerTerms    | array of objects                          | Array of [AzureOfferTerm](#azureofferterm) objects.               |
| attributes    | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes. Contains `"objectType": "AzureRateCard"`   |

### Operations on the AzureRateCard resource

- [Get prices for Microsoft Azure](get-prices-for-microsoft-azure.md)

## AzureMeter

| Property         | Type             | Description                                                                                   |
|------------------|------------------|-----------------------------------------------------------------------------------------------|
| id               | string           | Meter's unique identifier.                                                                    |
| name             | string           | Friendly name of the meter.                                                                   |
| rates            | object           | Meter rates. The key is the meter quantity (string) and the value is the meter rate (number). |
| tags             | array of strings | Optional meter tags. This array can be empty.                                                 |
| category         | string           | Category of the resource.                                                                     |
| subcategory      | string           | Subcategory of the resource.                                                                 |
| region           | string           | Region of the id.                                                                             |
| unit             | string           | The type of quantity (hours, bytes, etc.)                                                     |
| includedQuantity | number           | Meter quantity that is included free of charge.                                               |
| effectiveDate    | string           | The date this meter is in effect.                                                             |

## AzureOfferTerm

| Property         | Type             | Description                             |
|------------------|------------------|-----------------------------------------|
| name             | string           | Friendly name of the offer term.        |
| discount         | number           | The discount applied, if any.           |
| excludedMeterIds | array of strings | Meters excluded from the offer, if any. |
| effectiveDate    | string           | The date the offer is in effect.        |
