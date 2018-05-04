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

# Entitlement

>[!IMPORTANT]   
>This information relates to pre-released product which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here. 

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
| quantity             | int                                                            | The quantity of entitlements (excludes Unfulfilled/Transfered entitlements). |
| quantityDetails      | IEnumerable<[QuantityDetail](#quantitydetail)>                 | The list of entitlement quantity details (the number of items and status of each quantity). |
| entitlementType      | [EntitlementType](#entitlementtype)                            | The type of entitlement.                                                |
| entitledArtifacts    | IEnumerable<[Artifact](#artifact)>                             | The list of artifacts associated with the entitlement.                  |
| IncludedEntitlements | IEnumerable<[Entitlement](#artifact)>                          | The list of entitlements which are implicitly included as a result of the ProductId / SkuId purchase from catalog. |

 

## <span id="ReferenceOrder"></span><span id="referenceorder"></span><span id="REFERENCEORDER"></span>ReferenceOrder


The order reference of an entitlement. 

| Property             | Type                                                           | Description                                                             |
|----------------------|----------------------------------------------------------------|-------------------------------------------------------------------------|
| id                   | string                                                         | The ID of the referenced order.                                         |
| lineItemId           | string                                                         | The ID of the referenced order line item.                               |



## <span id="QuantityDetail"></span><span id="quantitydetail"></span><span id="QUANTITYDETAIL"></span>QuantityDetail


Represents the details of an entitlement quantity.

| Property             | Type                                            | Description                                                             |
|----------------------|-------------------------------------------------|-------------------------------------------------------------------------|
| quantity             | int                                             | The number of items.                                                    |
| status               | string                                          | The status of quantity.                                                 |



## <span id="EntitlementType"></span><span id="entitlementtype"></span><span id="ENTITLEMENTTYPE"></span>EntitlementType


An [Enum](https://docs.microsoft.com/en-us/dotnet/api/system.enum) with values that indicate the type of entitlement.

| Value                                     | Description                                                                                |
|-------------------------------------------|--------------------------------------------------------------------------------------------|
| Software                                  | Indicates entitlement type related to software.                                            |
| VirtualMachineReservedInstance            | Indicates entitlement type related to Azure Reserved Virtual Machine Instances.            |



## <span id="Artifact"></span><span id="artifact"></span><span id="ARTIFACT"></span>Artifact


The artifact associated with the entitlement.  

| Property             | Type                                                           | Description                                                             |
|----------------------|----------------------------------------------------------------|-------------------------------------------------------------------------|
| artifactType         | [ArtifactType](#artifacttype)                                  | The type of artifact.                                                   |



## <span id="ArtifactType"></span><span id="artifacttype"></span><span id="ARTIFACTTYPE"></span>ArtifactType


An [Enum](https://docs.microsoft.com/en-us/dotnet/api/system.enum) with values that indicate the type of entitlement artifact.

| Value                                     | Description                                                                                |
|-------------------------------------------|--------------------------------------------------------------------------------------------|
| ProductKey                                | Indicates the artifact aids with retrieval of product key.                                 |
| VirtualMachineReservedInstance            | Indicates the artifact aids with retrieval of Azure Reserved Virtual Machine Instances.    |



## <span id="VirtualMachineReservedInstanceArtifact"></span><span id="virtualmachinereservedinstanceartifact"></span><span id="VIRTUALMACHINERESERVEDARTIFACT"></span>VirtualMachineReservedInstanceArtifact


The artifact associated with an Azure Reserved Virtual Machine Instance entitlement. It inherits from the [Artifact](#artifact) class.  

| Property             | Type                                                           | Description                                                             |
|----------------------|----------------------------------------------------------------|-------------------------------------------------------------------------|
| link                 | [Link](utility-resources.md#link)                              | The link to get all associated artifact details.                        |
| resourceID           | string                                                         | The ID of the Azure reservation order or resource.                      |



## <span id="VirtualMachineReservedInstanceArtifactDetails"></span><span id="virtualmachinereservedinstanceartifactdetails"></span><span id="VIRTUALMACHINERESERVEDARTIFACTDETAILS"></span>VirtualMachineReservedInstanceArtifactDetails


Represents the entity returned upon invocation of the Azure Reserved Virtual Machine Instance artifact link.  

| Property                    | Type                                                                 | Description                                                   |
|-----------------------------|----------------------------------------------------------------------|---------------------------------------------------------------|
| type                        | [ArtifactType](#artifacttype)                                        | The type of artifact.                                         |
| virtualMachineReservations  | IEnumerable<[VirtualMachineReservation](#virtualmachinereservation)> | Indicates the Azure resource or reservation order identifier. |



## <span id="VirtualMachineReservation"></span><span id="virtualmachinereservation"></span><span id="VIRTUALMACHINERESERVATION"></span>VirtualMachineReservation


Represents an individual virtual machine reservation.

| Property                | Type                                                           | Description                                                            |
|-------------------------|----------------------------------------------------------------|------------------------------------------------------------------------|
| reservationId           | string                                                         | The ID of the reservation.                                             |
| scopeType               | string                                                         | The type of scope associated with the virtual machine reservation.     |
| displayName             | string                                                         | The display name of the reservation.                                   |
| appliedScopes           | IEnumerable<string>                                            | The list of applied scopes associated with the reservation. (Only available when scopeType is not shared.)  |
| quantity                | int                                                            | The number of virtual machines in the reservation.                     |
| expiryDateTime          | string in UTC date-time format                                 | The expiry date of the reservation.                                    |
| effectiveDateTime       | string in UTC date-time format                                 | The effective date of the reservation.                                 |
| provisioningState       | string                                                         | The provisioning state of the reservation.                             |

 


