---
title: License resources
description: Describes resources related to licenses.
ms.assetid: 20592E06-8A87-41F4-B8B0-6F9200556FDA
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: PartnerCenterCSP
ms.localizationpriority: medium
---

# License resources


**Applies To**

- Partner Center
- Partner Center for Microsoft Cloud Germany
- Partner Center for Microsoft Cloud for US Government

Describes resources related to licenses.

## <span id="License"/><span id="license"/><span id="LICENSE"/>License


Describes a user license.

>[!NOTE]
>Unsupported on Partner Center operated by 21Vianet.

 

| Property     | Type                                                           | Description                                                    |
|--------------|----------------------------------------------------------------|----------------------------------------------------------------|
| servicePlans | array of ServicePlan resources                                 | The collection of service plans that correspond to the license |
| productSKU   | ProductSku                                                     | The sku of the product that corresponds to the license.        |
| attributes   | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes corresponding to the license.          |

 

## <span id="LicenseUpdate"/><span id="licenseupdate"/><span id="LICENSEUPDATE"/>LicenseUpdate


Provides information used to assign or remove licenses from a user.

| Property         | Type                                                           | Description                                               |
|------------------|----------------------------------------------------------------|-----------------------------------------------------------|
| licensestoAssign | array of objects                                               | Array of [LicenseAssignment](#licenseassignment) objects. |
| licensesToRemove | array of strings                                               | The product SKU identifiers of the licenses to remove.    |
| licenseWarnings  | array of objects                                               | Array of [LicenseWarning](#licensewarning) objects.       |
| attributes       | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes.                                  |

 

## <span id="LicenseAssignment"/><span id="licenseassignment"/><span id="LICENSEASSIGNMENT"/>LicenseAssignment


Provides information needed for a license update operation.

| Property      | Type             | Description                                                                |
|---------------|------------------|----------------------------------------------------------------------------|
| excludedPlans | array of strings | The service plan identifiers to be excluded from availability to the user. |
| skuId         | string           | The product SKU identifier for the license.                                |

 

## <span id="LicenseWarning"/><span id="licensewarning"/><span id="LICENSEWARNING"/>LicenseWarning


Contains warning information that occurred during a license update
operation.

| Property     | Type             | Description                                         |
|--------------|------------------|-----------------------------------------------------|
| code         | string           | The warning code.                                   |
| message      | string           | The warning message.                                |
| servicePlans | array of strings | The service plan names associated with the warning. |

 

## <span id="ProductSku"/><span id="productsku"/><span id="PRODUCTSKU"/>ProductSku


Describes product details.

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
<td>The product identifier.</td>
</tr>
<tr class="even">
<td>name</td>
<td>string</td>
<td>The user principal identifier.</td>
</tr>
<tr class="odd">
<td>skuPartNumber</td>
<td>string</td>
<td>The SKU part number name for the product. For example, for Office 365 Plan E3 , this value is &quot;EnterprisePack&quot;. This can be used in place of id if the id is not available.</td>
</tr>
<tr class="even">
<td>targetType</td>
<td>string</td>
<td>The target type of the product. This identifies whether the product is applicable to a &quot;User&quot; or a &quot;Tenant&quot;.</td>
</tr>
<tr class="odd">
<td>licenseGroupId</td>
<td>string</td>
<td>Identifies via a group identifier the authority or service that manages the productSku license. Products are segregated under license groups for better manageability.
<p>&quot;group1&quot; - All products whose licenses can be managed by Azure Active Directory (AAD).</p>
<p>&quot;group2&quot; - Minecraft product licenses.</p></td>
</tr>
</tbody>
</table>

 

## <span id="ServicePlan"/><span id="serviceplan"/><span id="SERVICEPLAN"/>ServicePlan


Identifies a deployable service within a product SKU. A product can have
many service plans.

| Property         | Type   | Description                                                                                                       |
|------------------|--------|-------------------------------------------------------------------------------------------------------------------|
| id               | string | The service plan identifier.                                                                                      |
| displayName      | string | The localized display name for the service plan.                                                                  |
| serviceName      | string | The service name.                                                                                                 |
| capabilityStatus | string | The service plan status of the service plan.                                                                      |
| targetType       | string | The target type of the service plan. This identifies whether the product is applicable to a "User" or a "Tenant". |

 

## <span id="SubscribedSku"/><span id="subscribedsku"/><span id="SUBSCRIBEDSKU"/>SubscribedSku


Describes a subscribed product owned by a tenant.

| Property         | Type                                                           | Description                                                                                       |
|------------------|----------------------------------------------------------------|---------------------------------------------------------------------------------------------------|
| availableUnits   | integer                                                        | The number of units available for assignment. This is calculated as total units - consumed units. |
| activeUnits      | integer                                                        | The number of units active for assignment.                                                        |
| consumedUnits    | integer                                                        | The number of units consumed.                                                                     |
| suspendedUnits   | integer                                                        | The number of units suspended.                                                                    |
| totalUnits       | integer                                                        | The total number of units. This is calculated as the sum of the active and warning units.         |
| warningUnits     | integer                                                        | The number of warning units.                                                                      |
| productSku       | ProductSku                                                     | The product sku.                                                                                  |
| servicePlans     | array of ServicePlan resources                                 | The collection of service plans of a product.                                                     |
| capabilityStatus | string                                                         | The sku status of a product.                                                                      |
| attributes       | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes corresponding to the resource.                                            |

 

 

 




