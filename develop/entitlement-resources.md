---
title: Entitlement resources
description: Describes resources related to entitlement.
ms.assetid: FDD151CC-3473-46DF-A422-265DCBC8A498
ms.date: 07/27/2018
ms.localizationpriority: medium
---

# Entitlement resources


**Applies To**

- Partner Center
- Partner Center operated by 21Vianet
- Partner Center for Microsoft Cloud Germany
- Partner Center for Microsoft Cloud for US Government


## <span id="Entitlement"/><span id="entitlement"/><span id="ENTITLEMENT"/>Entitlement


This resource represents the products to which the customer has right to use because of partner purchase on items from the catalog. 

| Property | Type | Description |
|----------|------|-------------|
| referenceOrder | [ReferenceOrder](#referenceorder) | The order reference which resulted in the entitlement. |
| productId | string | The ID of the product. |
| skuID | string | The ID of the SKU. |
| quantity | int | The quantity of entitlements (excludes Unfulfilled/Transfered entitlements). |
| quantityDetails | IEnumerable<[QuantityDetail](#quantitydetail)> | The list of entitlement quantity details (the number of items and status of each quantity). |
| entitlementType | string | The type of entitlement. (Updated to string from [EntitlementType](#entitlementtype) in SDK 1.8.) |
| entitledArtifacts | IEnumerable<[Artifact](#artifact)> | The list of artifacts associated with the entitlement. |
| IncludedEntitlements | IEnumerable<[Entitlement](#artifact)> | The list of entitlements which are implicitly included as a result of the ProductId / SkuId purchase from catalog. |


## <span id="ReferenceOrder"/><span id="referenceorder"/><span id="REFERENCEORDER"/>ReferenceOrder

The order reference of an entitlement. 

| Property | Type | Description |
|----------|------|-------------|
| id | string | The ID of the referenced order. |
| lineItemId | string | The ID of the referenced order line item. |


## <span id="QuantityDetail"/><span id="quantitydetail"/><span id="QUANTITYDETAIL"/>QuantityDetail

Represents the details of an entitlement quantity.

| Property | Type | Description |
|----------|------|-------------|
| quantity | int | The number of items. |
| status | string | The status of quantity. |


## <span id="EntitlementType"/><span id="entitlementtype"/><span id="ENTITLEMENTTYPE"/>EntitlementType

> [!IMPORTANT]  
> Deprecated in SDK v1.9

An [Enum](https://docs.microsoft.com/dotnet/api/system.enum) with values that indicate the type of entitlement.

| Value | Description |
|-------|-------------|
| Software | Indicates entitlement type related to software. |
| VirtualMachineReservedInstance | Indicates entitlement type related to Azure Reserved Virtual Machine Instances. |


## <span id="Artifact"/><span id="artifact"/><span id="ARTIFACT"/>Artifact

The artifact associated with the entitlement.  

| Property | Type | Description |
|----------|------|-------------|
| artifactType | string | The type of artifact. (Updated to string from [ArtifactType](#artifacttype) in SDK V1.8) |
| dynamicAttributes | Dictionary&lt;string, object&gt; | Dynamic attributes containing artifacttype specific values. For example when artifactType = "reservedinstance", this will contain "reservationType" = "virtualmachines" or "reservationType" = "sqldatabases" denoting virtual machine reserved instance or Azure SQL reserved instance. (Available starting in SDK v1.9) |


## <span id="ArtifactType"/><span id="artifacttype"/><span id="ARTIFACTTYPE"/>ArtifactType

> [!IMPORTANT]  
> Deprecated in SDK v1.9

An [Enum](https://docs.microsoft.com/dotnet/api/system.enum) with values that indicate the type of entitlement artifact.

| Value                          | Description                                                                             |
|--------------------------------| ----------------------------------------------------------------------------------------|
| VirtualMachineReservedInstance | Indicates the artifact aids with retrieval of Azure Reserved Virtual Machine Instances. |


## <span id="ReservedInstanceArtifact"/><span id="reservedinstanceartifact"/><span id="RESERVEDINSTANCEARTIFACT"/>ReservedInstanceArtifact

The artifact associated with an Azure Reserved Instance entitlement. It inherits from the [Artifact](#artifact) class. 

| Property   | Type                           | Description                                        |
|------------|--------------------------------|----------------------------------------------------|
| link       | [Link](./utility-resources.md#link) | The link to get all associated artifact details.   |
| resourceID | string                         | The ID of the Azure reservation order or resource. |


## <span id="ReservedInstanceArtifactDetails"/><span id="reservedinstanceartifactdetails"/><span id="RESERVEDINSTANCEARTIFACTDETAILS"/>ReservedInstanceArtifactDetails

Represents the entity returned upon invocation of the Azure Reserved Instance artifact link. 


|   Property   |           Type           |                          Description                          |
|--------------|--------------------------|---------------------------------------------------------------|
|     type     |          string          |                     The type of artifact.                     |
| reservations | IEnumerable<Reservation> | Indicates the Azure resource or reservation order identifier. |

## <span id="Reservation"/><span id="reservation"/><span id="RESERVATION"/>Reservation

Represents an individual reservation.

| Property          | Type                           | Description                                                        |
|-------------------|--------------------------------|--------------------------------------------------------------------|
| reservationId     | string                         | The ID of the reservation.                                         |
| scopeType         | string                         | The type of scope associated with the virtual machine reservation. |
| displayName       | string                         | The display name of the reservation.                               |
| appliedScopes     | IEnumerable                    | The list of applied scopes associated with the reservation. (Only available when scopeType is not shared.) |
| quantity          | int                            | The number of virtual machines in the reservation.                 |
| expiryDateTime    | string in UTC date-time format | The expiry date of the reservation.                                |
| effectiveDateTime | string in UTC date-time format | The effective date of the reservation.                             |
| provisioningState | string                         | The provisioning state of the reservation.                         |


## <span id="VirtualMachineReservedInstanceArtifact"/><span id="virtualmachinereservedinstanceartifact"/><span id="VIRTUALMACHINERESERVEDARTIFACT"/>VirtualMachineReservedInstanceArtifact

> [!IMPORTANT]  
> Deprecated in SDK v1.9

The artifact associated with an Azure Reserved Virtual Machine Instance entitlement. It inherits from the [Artifact](#artifact) class.  

| Property   | Type                              | Description                                        |
|------------|-----------------------------------|----------------------------------------------------|
| link       | [Link](utility-resources.md#link) | The link to get all associated artifact details.   |
| resourceID | string                            | The ID of the Azure reservation order or resource. |


## <span id="VirtualMachineReservedInstanceArtifactDetails"/><span id="virtualmachinereservedinstanceartifactdetails"/><span id="VIRTUALMACHINERESERVEDARTIFACTDETAILS"/>VirtualMachineReservedInstanceArtifactDetails

> [!IMPORTANT]  
> Deprecated in SDK v1.9

Represents the entity returned upon invocation of the Azure Reserved Virtual Machine Instance artifact link.  

| Property                    | Type                                                                 | Description           |
|-----------------------------|----------------------------------------------------------------------|-----------------------|
| type                        | [ArtifactType](#artifacttype)                                        | The type of artifact. |
| virtualMachineReservations  | IEnumerable<[VirtualMachineReservation](#virtualmachinereservation)> | Indicates the Azure resource or reservation order identifier. |


## <span id="VirtualMachineReservation"/><span id="virtualmachinereservation"/><span id="VIRTUALMACHINERESERVATION"/>VirtualMachineReservation

> [!IMPORTANT]  
> Deprecated in SDK v1.9

Represents an individual virtual machine reservation.


|     Property      |              Type              |                                                Description                                                 |
|-------------------|--------------------------------|------------------------------------------------------------------------------------------------------------|
|   reservationId   |             string             |                                         The ID of the reservation.                                         |
|     scopeType     |             string             |                     The type of scope associated with the virtual machine reservation.                     |
|    displayName    |             string             |                                    The display name of the reservation.                                    |
|   appliedScopes   |      IEnumerable<string>       | The list of applied scopes associated with the reservation. (Only available when scopeType is not shared.) |
|     quantity      |              int               |                             The number of virtual machines in the reservation.                             |
|  expiryDateTime   | string in UTC date-time format |                                    The expiry date of the reservation.                                     |
| effectiveDateTime | string in UTC date-time format |                                   The effective date of the reservation.                                   |
| provisioningState |             string             |                                 The provisioning state of the reservation.                                 |

