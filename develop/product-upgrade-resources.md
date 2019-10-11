---
title: Product upgrade resources
description: Resources related to Partner Center product upgrade.
ms.assetid: DF237297-7956-42EE-8F09-4304F6EFBF26
ms.date: 10/11/2019
ms.localizationpriority: medium
---

# Product upgrade resources

Applies to:

- Partner Center

The following resources are related to product upgrade.

## ProductUpgradeRequest

**ProductUpgradesRequest** provides information about the product upgrades request object.

| Property | Type | Description |
|----------------------|----------------------------------------------|----------------------------------------------------------------|
| customerId           | string                                       | A GUID-formatted string that identifies the customer. |
| productFamily        | string                                       | The product family for which the upgrade is requested for. |
| attributes           | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes. |


## ProductUpgradesEligibility

**ProductUpgradesEligibility** provides information about the customer's eligibility for upgrading a product.

| Property | Type | Description |
|----------------------|--------------------------------------------- |----------------------------------------------------------------|
| customerId           | string                                       | A GUID-formatted string that identifies the customer. |          | productFamily        | string                                       | The product family for which the upgrade is requested for. |
| isEligible           | bool                                         | The bool value indicates whether the customer is eligible for requested upgrade. |
| upgradeId            | string                                       | The upgrade ID if a product upgrade for given family is already in place. |
| reason               | string                                       | The reason for which customer isn't eligible for product upgrade. |
| productFamily        | string                                       | The product family for which the upgrade is requested for. |
| attributes           | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes.  

## ProductUpgradesStatus

**ProductUpgradesStatus** provides information about the status of a product upgrade.

| Property | Type | Description |
|---------------------|----------------------------------------------------------------|-----------------------------------------------|
| Id                  | string                                                         | A GUID-formatted string that identifies the upgrade.             
| productFamily       | string                                                         | The product family for which the upgrade is requested for.
| status              | string                                                         | The status of the product upgrade.
| lineItems           | array of [UpgradesLineItem](#upgradeslineitem) resources       | An array of objects that provides information of the upgrade details for each line item that was part of the request body.
| errorDetails        | [ErrorDetails](#errordetails) resource                         | The error details for upgrade requested.
| attributes          | [ResourceAttributes](utility-resources.md#resourceattributes)  | The metadata attributes.      

## UpgradesLineItem

**UpgradesLineItem** describes the status of product upgrade details for each line item of the request.

| Property | Type | Description |
|-----------------|-----------------------------------------------------|--------------------------------------------------------------|
| sourceProduct   | [UpgradeProduct](#upgradeproduct) object            | Information of the source product being upgraded. |          
| targetProduct   | [UpgradeProduct](#upgradeproduct) object            | Information of the target product post upgrade. |             
| upgradedDate    | string in UTC date-time format                      | The date the subscription was upgraded. |
| status          | string                                              | The status of the product upgrade. | 
| errorDetails    | [ErrorDetails](#errordetails) resource              | The error details for upgrade requested. | 
| attributes      | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes.  |

## UpgradeProduct

**UpgradeProduct** provides information on the product being upgraded. 

| Property | Type |Description |
|----------------------|----------------------------------------------|----------------------------------------------------------------|
| id                   | string                                       | A GUID-formatted string that identifies the product. |
| name                 | string                                       | The friendly name of product being upgraded. |  
| attributes           | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes.    

## ErrorDetails

**ErrorDetails** provides details on errors during the upgrade process.

| Property | Type | Description |
|-------------------------|----------------------------------------------|-------------------------------------------------------------|
| code                    | string                                       | A error code when the product upgrade fails.           
| message                 | string                                       | The error message when the product upgrade fails.       
| attributes              | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes.    
