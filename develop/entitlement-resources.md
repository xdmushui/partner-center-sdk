---
title: Entitlement resources
description: Describes resources related to entitlement.
ms.date: 01/28/2019
ms.service: partner-dashboard
ms.subservice:  partnercenter-sdk
---

# Entitlement resources

**Applies To**

- Partner Center
- Partner Center operated by 21Vianet
- Partner Center for Microsoft Cloud Germany
- Partner Center for Microsoft Cloud for US Government

## Entitlement

This resource represents the products to which the customer has right to use because of partner purchase on items from the catalog.

| Property | Type | Description |
|----------|------|-------------|
| referenceOrder | [ReferenceOrder](#referenceorder) | The order reference that resulted in the entitlement. |
| productId | string | The ID of the product. |
| skuID | string | The ID of the SKU. |
| quantity | int | The quantity of entitlements (excludes Unfulfilled/Transfered entitlements). |
| quantityDetails | IEnumerable<[QuantityDetail](#quantitydetail)> | The list of entitlement quantity details (the number of items and status of each quantity). |
| entitlementType | string | The type of entitlement. (Updated to string from [EntitlementType](#entitlementtype) in SDK 1.8.) |
| entitledArtifacts | IEnumerable<[Artifact](#artifact)> | The list of artifacts associated with the entitlement. |
| IncludedEntitlements | IEnumerable<[Entitlement](#artifact)> | The list of entitlements, which are implicitly included as a result of the ProductId / SkuId purchase from catalog. |
| ExpiryDate | string in UTC date-time format  | The entitlement expiry date (if applicable). |

## ReferenceOrder

The order reference of an entitlement.

| Property | Type | Description |
|----------|------|-------------|
| id | string | The ID of the referenced order. |
| lineItemId | string | The ID of the referenced order line item. |
| alternateId | string | The alternate ID of the referenced order line item. |

## QuantityDetail

Represents the details of an entitlement quantity.

| Property | Type | Description |
|----------|------|-------------|
| quantity | int | The number of items. |
| status | string | The status of quantity. |

## EntitlementType

> [!IMPORTANT]
> Deprecated in SDK v1.9

An [Enum](/dotnet/api/system.enum) with values that indicate the type of entitlement.

| Value | Description |
|-------|-------------|
| Software | Indicates entitlement type related to software. |
| VirtualMachineReservedInstance | Indicates entitlement type related to Azure Reserved Virtual Machine Instances. |

## Artifact

The artifact associated with the entitlement.

| Property | Type | Description |
|----------|------|-------------|
| artifactType | string | The type of artifact. (Updated to string from [ArtifactType](#artifacttype) in SDK V1.8) |
| dynamicAttributes | Dictionary&lt;string, object&gt; | Dynamic attributes containing artifacttype specific values. For example when artifactType = "reservedinstance", this property will contain "reservationType" = "virtualmachines" or "reservationType" = "sqldatabases" denoting virtual machine reserved instance or Azure SQL reserved instance. (Available starting in SDK v1.9) |

## ArtifactType

> [!IMPORTANT]
> Deprecated in SDK v1.9

An [Enum](/dotnet/api/system.enum) with values that indicate the type of entitlement artifact.

| Value                          | Description                                                                             |
|--------------------------------| ----------------------------------------------------------------------------------------|
| VirtualMachineReservedInstance | Indicates the artifact aids with retrieval of Azure Reserved Virtual Machine Instances. |

## ReservedInstanceArtifact

The artifact associated with an Azure Reserved Instance entitlement. It inherits from the [Artifact](#artifact) class.

| Property   | Type                           | Description                                        |
|------------|--------------------------------|----------------------------------------------------|
| link       | [Link](./utility-resources.md#link) | The link to get all associated artifact details.   |
| resourceID | string                         | The ID of the Azure reservation order or resource. |

## ReservedInstanceArtifactDetails

Represents the entity returned upon invocation of the Azure Reserved Instance artifact link.

|   Property   |           Type           |                          Description                          |
|--------------|--------------------------|---------------------------------------------------------------|
|     type     |          string          |                     The type of artifact.                     |
| reservations | `IEnumerable<Reservation>` | Indicates the Azure resource or reservation order identifier. |

## Reservation

Represents an individual reservation.

| Property          | Type                           | Description                                                        |
|-------------------|--------------------------------|--------------------------------------------------------------------|
| reservationId     | string                         | The ID of the reservation.                                         |
| scopeType         | string                         | The type of scope associated with the virtual machine reservation. |
| displayName       | string                         | The display name of the reservation.                               |
| appliedScopes     | IEnumerable                    | The list of applied scopes associated with the reservation. (Only available when scopeType isn't shared.) |
| quantity          | int                            | The number of virtual machines in the reservation.                 |
| expiryDateTime    | string in UTC date-time format | The expiry date of the reservation.                                |
| effectiveDateTime | string in UTC date-time format | The effective date of the reservation.                             |
| provisioningState | string                         | The provisioning state of the reservation.                         |

## VirtualMachineReservedInstanceArtifact

> [!IMPORTANT]
> Deprecated in SDK v1.9

The artifact associated with an Azure Reserved Virtual Machine Instance entitlement. It inherits from the [Artifact](#artifact) class.

| Property   | Type                              | Description                                        |
|------------|-----------------------------------|----------------------------------------------------|
| link       | [Link](utility-resources.md#link) | The link to get all associated artifact details.   |
| resourceID | string                            | The ID of the Azure reservation order or resource. |

## VirtualMachineReservedInstanceArtifactDetails

> [!IMPORTANT]
> Deprecated in SDK v1.9

Represents the entity returned upon invocation of the Azure Reserved Virtual Machine Instance artifact link.

| Property                    | Type                                                                 | Description           |
|-----------------------------|----------------------------------------------------------------------|-----------------------|
| type                        | [ArtifactType](#artifacttype)                                        | The type of artifact. |
| virtualMachineReservations  | IEnumerable<[VirtualMachineReservation](#virtualmachinereservation)> | Indicates the Azure resource or reservation order identifier. |

## VirtualMachineReservation

> [!IMPORTANT]
> Deprecated in SDK v1.9

Represents an individual virtual machine reservation.

|     Property      |              Type              |                                                Description                                                 |
|-------------------|--------------------------------|------------------------------------------------------------------------------------------------------------|
|   reservationId   |             string             |                                         The ID of the reservation.                                         |
|     scopeType     |             string             |                     The type of scope associated with the virtual machine reservation.                     |
|    displayName    |             string             |                                    The display name of the reservation.                                    |
|   appliedScopes   |      `IEnumerable<string>`       | The list of applied scopes associated with the reservation. (Only available when scopeType isn't shared.) |
|     quantity      |              int               |                             The number of virtual machines in the reservation.                             |
|  expiryDateTime   | string in UTC date-time format |                                    The expiry date of the reservation.                                     |
| effectiveDateTime | string in UTC date-time format |                                   The effective date of the reservation.                                   |
| provisioningState |             string             |                                 The provisioning state of the reservation.                                 |
