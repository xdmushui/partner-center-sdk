---
title: Product upgrade resources
description: You can use multiple resources related to Partner Center product upgrades to an Azure plan. These include ProductUpgradeRequest, ProductUpgradesEligibility, ProductUpgradesStatus, UpgradesLineItem, UpgradeProduct, and ErrorDetails.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice:  partnercenter-sdk
---

# Product upgrade resources

You can use the following resources for information about Partner Center product upgrades from a Microsoft Azure (MS-AZR-0145P) subscription to an Azure plan.

## ProductUpgradeRequest

The **ProductUpgradesRequest** resource provides information about the product upgrades request object.

| Property      | Type                                                          | Description                                                |
|---------------|---------------------------------------------------------------|------------------------------------------------------------|
| customerId    | string                                                        | A GUID-formatted string that identifies the customer.      |
| productFamily | string                                                        | The product family for which the upgrade is requested for. |
| attributes    | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes.                                   |

## ProductUpgradesEligibility

The **ProductUpgradesEligibility** resource provides information about the customer's eligibility for upgrading a product.

| Property      | Type                                                          | Description                                                                      |
|---------------|---------------------------------------------------------------|----------------------------------------------------------------------------------|
| customerId    | string                                                        | A GUID-formatted string that identifies the customer.                            |
| productFamily | string                                                        | The product family for which the upgrade is requested for.                       |
| isEligible    | bool                                                          | The bool value indicates whether the customer is eligible for requested upgrade. |
| upgradeId     | string                                                        | The upgrade ID if a product upgrade for given family is already in place.        |
| reason        | string                                                        | The reason for which customer isn't eligible for product upgrade.                |
| productFamily | string                                                        | The product family for which the upgrade is requested for.                       |
| attributes    | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes.                                                         |

## ProductUpgradesStatus

The **ProductUpgradesStatus** resource provides information about the status of a product upgrade.

| Property | Type   | Description                                          |
|----------|--------|------------------------------------------------------|
| Id       | string | A GUID-formatted string that identifies the upgrade. |
| productFamily       | string                                                         | The product family for which the upgrade is requested for.
| status              | string                                                         | The status of the product upgrade.
| lineItems           | array of [UpgradesLineItem](#upgradeslineitem) resources       | An array of objects that provides information of the upgrade details for each line item that was part of the request body.
| errorDetails        | [ErrorDetails](#errordetails) resource                         | The error details for upgrade requested.
| attributes          | [ResourceAttributes](utility-resources.md#resourceattributes)  | The metadata attributes. |

## UpgradesLineItem

The **UpgradesLineItem** resource describes the status of product upgrade details for each line item of the request.

| Property      | Type                                                          | Description                                       |
|---------------|---------------------------------------------------------------|---------------------------------------------------|
| sourceProduct | [UpgradeProduct](#upgradeproduct) object                      | Information of the source product being upgraded. |
| targetProduct | [UpgradeProduct](#upgradeproduct) object                      | Information of the target product post upgrade.   |
| upgradedDate  | string in UTC date-time format                                | The date the subscription was upgraded.           |
| status        | string                                                        | The status of the product upgrade.                |
| errorDetails  | [ErrorDetails](#errordetails) resource                        | The error details for upgrade requested.          |
| attributes    | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes.                          |

## UpgradeProduct

The **UpgradeProduct** resource provides information about the product being upgraded.

| Property   | Type                                                          | Description                                          |
|------------|---------------------------------------------------------------|------------------------------------------------------|
| id         | string                                                        | A GUID-formatted string that identifies the product. |
| name       | string                                                        | The friendly name of product being upgraded.         |
| attributes | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes.                             |

## ErrorDetails

The **ErrorDetails** resource provides details about errors during the upgrade process.

| Property   | Type                                                          | Description                                       |
|------------|---------------------------------------------------------------|---------------------------------------------------|
| code       | string                                                        | An error code when the product upgrade fails.      |
| message    | string                                                        | The error message when the product upgrade fails. |
| attributes | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes.                          |
