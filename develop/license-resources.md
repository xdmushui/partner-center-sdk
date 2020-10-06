---
title: License resources
description: Describes resources related to licenses.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice:  partnercenter-sdk
---

# License resources

**Applies To**

- Partner Center
- Partner Center for Microsoft Cloud Germany
- Partner Center for Microsoft Cloud for US Government

Describes resources related to licenses.

## License

Describes a user license.

>[!NOTE]
>Unsupported on Partner Center operated by 21Vianet.

| Property     | Type                                                           | Description                                                    |
|--------------|----------------------------------------------------------------|----------------------------------------------------------------|
| servicePlans | array of ServicePlan resources                                 | The collection of service plans that correspond to the license |
| productSKU   | ProductSku                                                     | The sku of the product that corresponds to the license.        |
| attributes   | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes corresponding to the license.          |

## LicenseUpdate

Provides information used to assign or remove licenses from a user.

| Property         | Type                                                           | Description                                               |
|------------------|----------------------------------------------------------------|-----------------------------------------------------------|
| licensestoAssign | array of objects                                               | Array of [LicenseAssignment](#licenseassignment) objects. |
| licensesToRemove | array of strings                                               | The product SKU identifiers of the licenses to remove.    |
| licenseWarnings  | array of objects                                               | Array of [LicenseWarning](#licensewarning) objects.       |
| attributes       | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes.                                  |

## LicenseAssignment

Provides information needed for a license update operation.

| Property      | Type             | Description                                                                |
|---------------|------------------|----------------------------------------------------------------------------|
| excludedPlans | array of strings | The service plan identifiers to be excluded from availability to the user. |
| skuId         | string           | The product SKU identifier for the license.                                |

## LicenseWarning

Contains warning information that occurred during a license update
operation.

| Property     | Type             | Description                                         |
|--------------|------------------|-----------------------------------------------------|
| code         | string           | The warning code.                                   |
| message      | string           | The warning message.                                |
| servicePlans | array of strings | The service plan names associated with the warning. |

## ProductSku

Describes product details.

| Property       | Type             | Description                                         |
|----------------|------------------|-----------------------------------------------------|
| id             | string           | The product identifier.                             |
| name           | string           | The user principal identifier.                      |
| skuPartNumber  | string           | The SKU part number name for the product. For example, for Office 365 Plan E3, this value is <code>EnterprisePack</code>. This property can be used in place of id if the id isn't available.                |
| targetType     | string           | The target type of the product. This property identifies whether the product is applicable to a <code>User</code> or a <code>Tenant</code>.                                                                    |
| licenseGroupId | string           | Identifies via a group identifier the authority or service that manages the productSku license. Products are segregated under license groups for better manageability.<br/><br/>                                                                                     <code>group1</code> - All products whose licenses can be managed by Azure Active Directory (AAD).<br/><br/>                                            <code>group2</code> - Minecraft product licenses.                                         |

## ServicePlan

Identifies a deployable service within a product SKU. A product can have
many service plans.

| Property         | Type   | Description                                                                                                       |
|------------------|--------|-------------------------------------------------------------------------------------------------------------------|
| id               | string | The service plan identifier.                                                                                      |
| displayName      | string | The localized display name for the service plan.                                                                  |
| serviceName      | string | The service name.                                                                                                 |
| capabilityStatus | string | The service plan status of the service plan.                                                                      |
| targetType       | string | The target type of the service plan. This property identifies whether the product is applicable to a "User" or a "Tenant". |

## SubscribedSku

Describes a subscribed product owned by a tenant.

| Property         | Type                                                           | Description                                                                                       |
|------------------|----------------------------------------------------------------|---------------------------------------------------------------------------------------------------|
| availableUnits   | integer                                                        | The number of units available for assignment. This value is calculated as total units - consumed units. |
| activeUnits      | integer                                                        | The number of units active for assignment.                                                        |
| consumedUnits    | integer                                                        | The number of units consumed.                                                                     |
| suspendedUnits   | integer                                                        | The number of units suspended.                                                                    |
| totalUnits       | integer                                                        | The total number of units. This value is calculated as the sum of the active and warning units.         |
| warningUnits     | integer                                                        | The number of warning units.                                                                      |
| productSku       | ProductSku                                                     | The product sku.                                                                                  |
| servicePlans     | array of ServicePlan resources                                 | The collection of service plans of a product.                                                     |
| capabilityStatus | string                                                         | The sku status of a product.                                                                      |
| attributes       | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes corresponding to the resource.                                            |
