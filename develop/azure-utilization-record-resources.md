---
title: Azure utilization record resources
description: The Azure utilization record contains details about the utilization of an Azure subscription resource.
ms.assetid: 4C1EEEB3-DB25-4D61-BFED-C4AB5D3BB5CF
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice:  partnercenter-sdk
ms.localizationpriority: medium
---

# Azure utilization record resources

**Applies to:**

- Partner Center
- Partner Center for Microsoft Cloud Germany
- Partner Center for Microsoft Cloud for US Government

The Azure utilization record contains details about the utilization of an Azure subscription resource. If you are a cloud service provider partner who owns the billing relationship for your customers' Azure subscriptions, you can use this REST API to provide a scalable way to track usage incurred on the subscriptions in order to send an invoice to your customers at the end of every billing cycle.

To track usage and help predict your monthly bill and the bills for individual customers, you can combine a Rate Card query to [Get prices for Microsoft Azure](get-prices-for-microsoft-azure.md) with a request to [Get a customer's utilization records for Azure](get-a-customer-s-utilization-record-for-azure.md).

Prices differ by market and currency, and this API takes location into consideration. By default, the API uses your partner profile settings in Partner Center and your browser language, and those settings are customizable. The location awareness is especially relevant if you manage sales in multiple markets from a single, centralized office.

## AzureUtilizationRecord

Describes the properties of an Azure utilization record resource.

| Property       | Type                                      | Required | Description                                                                                                                                                                             |
|----------------|-------------------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| usageStartTime | string                                    | Yes      | The start of the usage aggregation time range. The response is grouped by the time of consumption (when the resource was actually used vs. when was it reported to the billing system). |
| usageEndTime   | string                                    | Yes      | The end of the usage aggregation time range. The response is grouped by the time of consumption. That is, when the resource was actually used vs. when was it reported to the billing system.   |
| resource       | object                                    | Yes      | Contains an [AzureResource](#azureresource) object.                                                                                                                                     |
| quantity       | number                                    | Yes      | The quantity consumed of the [AzureResource.](#azureresource)                                                                                                                           |
| unit           | string                                    | No       | The type of quantity (hours, bytes, etc.) This property is optional                                                                                                                     |
| infoFields     | object                                    | Yes      | Key-value pairs of instance level details. This object may be empty.                                                                                                                    |
| instanceData   | object                                    | No       | Contains an [AzureInstanceData](#azureinstancedata) object that contains key-value pairs of instance level details. This property is optional and may not be included.                  |
| attributes     | [ResourceAttributes](utility-resources.md#resourceattributes) | Yes      | The metadata attributes. Contains "objectType": "AzureUtilizationRecord"                                                                                                                |

### Operations on the AzureUtilizationRecord resource

- [Get a customer's utilization records for Azure](get-a-customer-s-utilization-record-for-azure.md)

## AzureResource

Describes the properties of an Azure Resource.

| Property    | Type   | Required | Description                                                                         |
|-------------|--------|----------|-------------------------------------------------------------------------------------|
| id          | string | Yes      | Unique identifier of the Azure resource. Also known as resourceID or resource GUID. |
| name        | string | No       | Friendly name of the resource being consumed. This property is optional.            |
| category    | string | No       | The category of the consumed resource. This property is optional.                   |
| subcategory | string | No       | The subcategory of the consumed resource. This property is optional.               |
| region      | string | No       | The region of the consumed resource. This property is optional.                     |

## AzureInstanceData

Describes the properties of an Azure Instance Data resource.

| Property       | Type             | Required | Description                                                                                                        |
|----------------|------------------|----------|--------------------------------------------------------------------------------------------------------------------|
| resourceUri    | string           | Yes      | The fully qualified Azure resource ID, which includes the resource groups and the instance name.                   |
| location       | string           | Yes      | Region in which the service was run.                                                                               |
| partNumber     | object           | Yes      | Unique namespace used to identify the resource for commercial marketplace third-party usage. This property may be an empty string. |
| orderNumber    | number           | Yes      | Unique namespace used to identify the third-party order for commercial marketplace. This property may be an empty string.          |
| tags           | array of strings | No       | Resource tags specified by the user. This property is optional and may not be included.                            |
| additionalInfo | array of strings | No       | Additional data for an Azure resource. This property is optional and may not be included.                          |