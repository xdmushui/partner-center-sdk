---
title: Products
description: Resources that represent products in a catalog to support Azure Reserved Instance. Includes resources for holding a Sku, checking product availability, and checking an inventory of products.
ms.assetid: 
ms.author: v-thpr
ms.date: 03/20/2018
ms.topic: article
ms.prod: partner-center
ms.technology: partner-center-sdk
---

# Products

[This information relates to pre-released product which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.]

<span class="sidebar_heading" style="font-weight: bold;">Applies
To</span>

-   Partner Center

Resources that represent products in a catalog to support Azure Reserved Instance. This includes resources for holding a Sku, checking product availability, and checking an inventory of products.


## <span id="Product"></span><span id="product"></span><span id="PRODUCT"></span>Product


Represents a product listed in a catalog. This resource is used as a means to discover [skus](#sku) that correspond to a particular product grouping.

| Property        | Type                          | Description                                                              |
|-----------------|-------------------------------|--------------------------------------------------------------------------|
| id              | string                        | The product identifier.                                                  |
| title           | string                        | The product title.                                                       |
| description     | string                        | The product description.                                                 |
| productType     | [ItemType](#itemtype)         | An object that describes the type categorization of this product.        |
| links           | [ProductLinks](#productlinks) | The resource links contained within the product.                         |



## <span id="ItemType"></span><span id="itemtype"></span><span id="ITEMTYPE"></span>Item Type


Represents the type categorization of an item.

| Property        | Type                          | Description                                                                          |
|-----------------|-------------------------------|--------------------------------------------------------------------------------------|
| id              | string                        | The type identifier.                                                                 |
| displayName     | string                        | The display name for this type.                                                      |
| subType         | [ItemType](#itemtype)         | Optional. An object that describes a sub-type categorization for this item type.     |

 

## <span id="ProductLinks"></span><span id="productlinks"></span><span id="PRODUCTLINKS"></span>Product Links


Contains a list of links for a [Product](#product).

| Property        | Type                          | Description                                                                        |
|-----------------|-------------------------------|------------------------------------------------------------------------------------|
| skus            | Link                          | The link for accessing the underlying skus.                                        |



## <span id="Sku"></span><span id="sku"></span><span id="SKU"></span>Sku


Represents a purchasable Stock Keeping Unit (sku) item listed in a catalog. 

| Property        | Type                          | Description                                                                          |
|-----------------|-------------------------------|--------------------------------------------------------------------------------------|
| id              | string                        | The sku identifier. This ID is unique only within the context of its parent product. |
| title           | string                        | The title of the sku.                                                                |
| description     | string                        | The description of the sku.                                                          |
| productId       | string                        | The identifier of the [Product](#product) that contains this sku.                    |
| minimumQuantity | int                           | The minimum quantity allowed for purchase.                                           |
| maximumQuantity | int                           | The maximum quantity allowed for purchase.                                           |
| isTrial         | bool                          | Indicates whether this sku represents a trial item.                                  |
| supportedBillingCycles  | array of strings      | The list of supported billing cycles for this sku. Supported values are the member names found in [BillingCycleType](#billingcycletype). |
| purchasePrerequisites   | array of strings      | The list of variables needed to execute an inventory check on this item. Supported values are: **InventoryCheck** (Indicates that the item's inventory should be evaluated before attempting to purchase this item.), **AzureSubscriptionRegistration** (Indicates that an Azure subscription is needed and must be registered before attempting to purchase this item.)  |
| inventoryVariables      | array of strings      | The list of prerequisite steps or actions that are needed prior to purchasing this item. Supported values are: **CustomerId** (The ID of the customerthat the purchase would be for.), **AzureSubscriptionId** (The ID of the Azure Subscription that would be used for an Azure Reserved Instance purchase.)  |
| provisioningVariables   | array of strings      | The list of variables that must be provided into the provisioning context of a [cart line item](cart.md#cartlineitem) when purchasing this item. Supported values are: **Scope** (The scope for an Azure Reserved Instance purchase (Single, Shared).), **AzureSubscriptionId** (The ID of the Azure Subscription that would be used for an Azure Reserved Instance purchase.)  |
| dynamicAttributes       | key/value pairs       | The dictionary of dynamic properties that apply to this item.                        |
| links           | [ResourceLinks](utility-resources.md#resourcelinks) | The resource links contained within the sku.                   |



## <span id="Availability"></span><span id="availability"></span><span id="AVAILABILITY"></span>Availability


Represents a configuration in which the parent sku is available for purchase. 

| Property        | Type                          | Description                                                                         |
|-----------------|-------------------------------|-------------------------------------------------------------------------------------|
| id              | string                        | The identifier for this availability. This ID is unique only within the context of its parent [product](#product) and [sku](#sku). **Note** This ID can change over time. You should only rely on this value within a short time span after retrieving it.  |
| productId       | string                        | The identifier of the [product](#product) that contains this availability.           |
| skuId           | string                        | The identifier of the [sku](#sku) that contains this availability.                   |
| catalogItemId   | string                        | The unique identifier for this item in the catalog. This is the ID that must be populated into the [OrderLineItem.OfferId](orders.md#orderlineitem) or [CartLineItem.CatalogItemId](cart.md#cartlineitem) properties when purchasing the parent [sku](#sku). **Note** This ID can change over time. You should only rely on this value within a short time after retrieving it. It should only be accessed and used at the time of purchase.  |
| defaultCurrency | string                        | The default currency supported for this availability.                               |
| segment         | string                        | The industry segment for this availability. Supported values are: Commercial, Education, Government, NonProfit. |
| country         | string                        | The country or region (in ISO country code format) where this availability applies. |
| links           | [ResourceLinks](utility-resources.md#resourcelinks) | The resource links contained within the product that contains this availability. |



## <span id="InventoryCheckRequest"></span><span id="inventorycheckrequest"></span><span id="INVENTORYCHECKREQUEST"></span>InventoryCheckRequest


Represents a request to check inventory against certain products. 

| Property         | Type                                                | Description                                                                                 |
|------------------|-----------------------------------------------------|---------------------------------------------------------------------------------------------|
| targetItems      | array of [InventoryItem](#inventoryitem)            | The list of catalog items that the inventory check will evaluate.                           |
| inventoryContext | key/value pairs                                     | The dictionary of context values that are needed to carry out an inventory check. Each [sku](#sku) of the products will define which values (if any) are needed to carry out this operation.  |
| links            | [ResourceLinks](utility-resources.md#resourcelinks) | The resource links contained within the inventory check request.                     |



## <span id="InventoryItem"></span><span id="inventoryitem"></span><span id="INVENTORYITEM"></span>InventoryItem


Represents a single item in an inventory check operation. This resource is used for specifying the target items in an input request, and is also used to represent the output results of the inventory check operation.  

| Property         | Type                                                              | Description                                                                      |
|------------------|-------------------------------------------------------------------|----------------------------------------------------------------------------------|
| productId        | string                                                            | (Required) The identifier of the [product](#product).                            |
| skuId            | string                                                            | The identifier of the [sku](#sku). When using this resource as input to an inventory request, this value is optional. If this value is not provided, then all skus under the product will be considered as target items of the inventory check operation.      |
| isRestricted     | bool                                                              | Indicates whether this item was found to have a restricted inventory.            |
| restrictions     | array of [InventoryRestriction](#inventoryrestriction)            | The details of any restrictions that are found for this item. This property will only be populated if **isRestricted** = "true". |



## <span id="InventoryRestriction"></span><span id="inventoryrestriction"></span><span id="INVENTORYRESTRICTION"></span>InventoryRestriction


Represents the details of an inventory restriction. This is only applicable for inventory check output results, not for input requests.

| Property         | Type                  | Description                                                                                 |
|------------------|-----------------------|---------------------------------------------------------------------------------------------|
| reasonCode       | string                | The code that identifies the reason for the restriction.                                    |
| description      | string                | The description of the inventory restriction.                                               |
| properties       | key/value pairs       | The dictionary of properties that may provide further details on the restriction.           |



## <span id="billingCycleType"></span><span id="billingcycletype"></span><span id="BILLINGCYCLETYPE"></span>BillingCycleType


An enumeration with values that indicate a type of billing cycle.

| Value              | Position     | Description                                                                                |
|--------------------|--------------|--------------------------------------------------------------------------------------------|
| Unknown            | 0            | Enum initializer.                                                                          |
| Monthly            | 1            | Indicates that the partner will be charged monthly.                                        |
| Annual             | 2            | Indicates that the partner will be charged annually.                                       |
| None               | 3            | Indicates that the partner will not be charged. This value may be used for trial items.    |
| OneTime            | 4            | Indicates that the partner will be charged one time.                                       |





