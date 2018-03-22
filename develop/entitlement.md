---
title: Entitlement
description: Describes resources related to entitlement.
ms.assetid: FDD151CC-3473-46DF-A422-265DCBC8A498
ms.author: v-thpr
ms.date: 12/15/2017
ms.topic: article
ms.prod: partner-center
ms.technology: partner-center-sdk
---

# Invoice

[This information relates to pre-released product which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.] 

<span class="sidebar_heading" style="font-weight: bold;">Applies
To</span>

-   Partner Center
-   Partner Center operated by 21Vianet
-   Partner Center for Microsoft Cloud Germany
-   Partner Center for Microsoft Cloud for US Government


## <span id="Entitlement"></span><span id="entitlement"></span><span id="ENTITLEMENT"></span>Entitlement


This resource represents the products to which the customer has right to use because of partner purchase on items from the catalog. 

| Property             | Type                                                           | Description                                                             |
|----------------------|----------------------------------------------------------------|-------------------------------------------------------------------------|
| referenceOrder       | [ReferenceOrder](#referenceorder)                              | The order reference which resulted in the entitlement.                  |
| productId            | string                                                         | The ID of the product.                                                  |
| skuID                | string                                                         | The ID of the SKU.                                                      |
| skuTitle             | string                                                         | The title of the product SKU.                                           |
| quantity             | int                                                            | The quantity of entitlements.                                           |
| productType          | [ItemType](products.md#itemtype)                               | The type of product to filter the entitlements.                         |
| entitlementType      | [EntitlementType](#entitlementtype)                            | The type of entitlement.                                                |
| entitledArtifacts    | IEnumerable<[Artifact](#artifact)>.                            | The list of artifacts associated with the entitlement.                  |
| IncludedEntitlements | IEnumerable<[Entitlement](#artifact)>.                         | The list of entitlements which are implicitly included as a result of the ProductId / SkuId purchase from catalog. |

 

## <span id="ReferenceOrder"></span><span id="referenceorder"></span><span id="REFERENCEORDER"></span>ReferenceOrder


The order reference of an entitlement. 

| Property             | Type                                                           | Description                                                             |
|----------------------|----------------------------------------------------------------|-------------------------------------------------------------------------|
| id                   | string                                                         | The ID of the referenced order.                                         |
| lineItemId           | string                                                         | The ID of the referenced order line item.                               |



## <span id="EntitlementType"></span><span id="entitlementtype"></span><span id="ENTITLEMENTTYPE"></span>EntitlementType


An enumeration with values that indicate the type of entitlement.

| Value                                     | Description                                                                                |
|-------------------------------------------|--------------------------------------------------------------------------------------------|
| Software                                  | Indicates entitlement type related to software.                                            |
| VirtualMachineReservedInstance            | Indicates entitlement type related to Azure virtual machine reserved instances.            |



## <span id="Artifact"></span><span id="artifact"></span><span id="ARTIFACT"></span>Artifact


The artifact associated with the entitlement.  

| Property             | Type                                                           | Description                                                             |
|----------------------|----------------------------------------------------------------|-------------------------------------------------------------------------|
| artifactType         | [ArtifactType](#artifacttype)                                  | The type of artifact.                                                   |



## <span id="ArtifactType"></span><span id="artifacttype"></span><span id="ARTIFACTTYPE"></span>ArtifactType


An enumeration with values that indicate the type of entitlement artifact.

| Value                                     | Description                                                                                |
|-------------------------------------------|--------------------------------------------------------------------------------------------|
| ProductKey                                | Indicates the artifact aids with retrieval of product key.                                 |
| VirtualMachineReservedInstance            | Indicates the artifact aids with retrieval of Azure virtual machine reserved instances.    |



## <span id="VirtualMachineReservedInstanceArtifact"></span><span id="virtualmachinereservedinstanceartifact"></span><span id="VIRTUALMACHINERESERVEDARTIFACT"></span>VirtualMachineReservedInstanceArtifact


The artifact associated with a virtual machine reserved instance entitlement. It inherits from the [Artifact](#artifact) class.  

| Property             | Type                                                           | Description                                                             |
|----------------------|----------------------------------------------------------------|-------------------------------------------------------------------------|
| link                 | [Link](utility-resources.md#link)                              | The link to get all associated artifact details.                        |
| resourceID           | string                                                         | The ID of the Azure reservation order or resource.                      |



## <span id="VirtualMachineReservedInstanceArtifactDetails"></span><span id="virtualmachinereservedinstanceartifactdetails"></span><span id="VIRTUALMACHINERESERVEDARTIFACTDETAILS"></span>VirtualMachineReservedInstanceArtifactDetails


Represents the entity returned upon invocation of the virtual machine reserved instance artifact link.  

| Property                    | Type                                                                 | Description                                                   |
|-----------------------------|----------------------------------------------------------------------|---------------------------------------------------------------|
| type                        | [ArtifactType](#artifacttype)                                        | The type of artifact.                                         |
| virtualMachineReservations  | IEnumerable<[VirtualMachineReservation](#virtualmachinereservation)> | Indicates the azure resource or reservation order identifier. |



## <span id="VirtualMachineReservation"></span><span id="virtualmachinereservation"></span><span id="VIRTUALMACHINERESERVATION"></span>VirtualMachineReservation


Represents an individual virtual machine reservation.

| Property                | Type                                                           | Description                                                            |
|-------------------------|----------------------------------------------------------------|------------------------------------------------------------------------|
| reservationId           | string                                                         | The ID of the reservation.                                             |
| scopeType               | string                                                         | The type of scope associated with the virtual machine reservation.     |
| quantity                | int                                                            | The number of virtual machines in the reservation.                     |
| expiryDateTime          | string in UTC date-time format                                 | The expiry date of the reservation.                                    |
| effectiveDateTime       | string in UTC date-time format                                 | The effective date of the reservation.                                 |
| provisioningState       | string                                                         | The provisioning state of the reservation.                             |

 


