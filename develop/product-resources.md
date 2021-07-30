---
title: Products resources
description: Resources that represent purchasable goods or services. Includes resources for describing the product type and shape (SKU), and for checking the availability of the product in an inventory.
ms.date: 04/01/2019
ms.service: partner-dashboard
ms.subservice:  partnercenter-sdk
---

# Products resources

Resources that represent purchasable goods or services. Includes resources for describing the product type and shape (SKU), and for checking the availability of the product in an inventory.

## Product

Represents a purchasable good or service. A product by itself isn't a purchasable item.

| Property           | Type                          | Description                                                              |
|--------------------|-------------------------------|--------------------------------------------------------------------------|
| id                 | string                        | The ID for this product.                                                 |
| title              | string                        | The product title.                                                       |
| description        | string                        | The product description.                                                 |
| productType        | [ItemType](#itemtype)         | An object that describes the type categorization(s) of this product.     |
| isMicrosoftProduct | bool                          | Indicates whether this is a Microsoft product.                          |
| publisherName      | string                        | The name of the product's publisher if available.                          |
| links              | [ProductLinks](#productlinks) | The resource links contained within the product.                         |

## ItemType

Represents the type of a product.

| Property        | Type                          | Description                                                                          |
|-----------------|-------------------------------|--------------------------------------------------------------------------------------|
| id              | string                        | The type identifier.                                                                 |
| displayName     | string                        | The display name for this type.                                                      |
| subType         | [ItemType](#itemtype)         | Optional. An object that describes a subtype categorization for this item type.     |

## ProductLinks

Contains a list of links for a [Product](#product).

| Property        | Type                                                          | Description                                          |
|-----------------|---------------------------------------------------------------|------------------------------------------------------|
| skus            | [Link](utility-resources.md#link)                             | The link for accessing the underlying SKUs.          |
| links           | [ResourceLinks](utility-resources.md#resourcelinks)           | The resource links contained within this resource.   |

## Sku

Represents a purchasable Stock Keeping Unit (SKU) under a product. These represent the different shapes of the product.

| Property               | Type             | Description                                                                           |
|------------------------|------------------|---------------------------------------------------------------------------------------|
| id                     | string           | The ID for this SKU. This ID is unique only within the context of its parent product. |
| title                  | string           | The title of the SKU.                                                                 |
| description            | string           | The description of the SKU.                                                           |
| productId              | string           | The ID of the parent [Product](#product) that contains this SKU.                      |
| minimumQuantity        | int              | The minimum quantity allowed for purchase.                                            |
| maximumQuantity        | int              | The maximum quantity allowed for purchase.                                            |
| isTrial                | bool             | Indicates whether this SKU is a trial item.                                           |
| supportedBillingCycles | array of strings | The list of supported billing cycles for this SKU. Supported values are the member names found in [BillingCycleType](#billingcycletype). |
| purchasePrerequisites  | array of strings | The list of prerequisite steps or actions that are needed prior to purchasing this item. The supported values are:<br/>  "InventoryCheck" - Indicates that the item's inventory should be evaluated before attempting to purchase this item.<br/> "AzureSubscriptionRegistration" - Indicates that an Azure subscription is needed and must be registered before attempting to purchase this item.  |
| inventoryVariables     | array of strings | The list of variables needed to execute an inventory check on this item. The supported values are:<br/> "CustomerId" - The ID of the customer that the purchase would be for.<br/> "AzureSubscriptionId" - The ID of the Azure subscription that would be used for an Azure reservation purchase.</br> "ArmRegionName" - The region for which to verify inventory. This value must match the "ArmRegionName" from the SKU's DynamicAttributes. |
| provisioningVariables  | array of strings | The list of variables that must be provided into the provisioning context of a [cart line item](cart-resources.md#cartlineitem) when purchasing this item. The supported values are:<br/> Scope - The scope for an Azure reservation purchase: "Single", "Shared".<br/> "SubscriptionId" - The ID of the Azure subscription that would be used for an Azure reservation purchase.<br/> "Duration" - The duration of the Azure reservation: "1Year", "3Year".  |
| dynamicAttributes      | key/value pairs  | The dictionary of dynamic properties that apply to this item. The properties in this dictionary are dynamic and can change without notice. You should not create strong dependencies on particular keys existing in the value of this property.    |
| links                  | [ResourceLinks](utility-resources.md#resourcelinks) | The resource links contained within the SKU.                   |
| AttestationProperties                  | [AttestationProperties](#attestationproperties) | The attestation properties for a SKU.                   |

## Availability

Represents a configuration in which a SKU is available for purchase (such as country, currency, and industry segment).

| Property        | Type                        | Description                                                                         |
|-----------------|-----------------------------------------------------|-------------------------------------------------------------------------------------|
| id              | string                        | The ID for this availability. This ID is unique only within the context of its parent [product](#product) and [SKU](#sku). **Note** This ID can change over time. You should only rely on this value within a short time span after retrieving it.  |
| productId       | string                        | The ID of the [product](#product) that contains this availability.           |
| skuId           | string                        | The ID of the [SKU](#sku) that contains this availability.                   |
| catalogItemId   | string                        | The unique identifier for this item in the catalog. This is the ID that must be populated into the [OrderLineItem.OfferId](order-resources.md#orderlineitem) or [CartLineItem.CatalogItemId](cart-resources.md#cartlineitem) properties when purchasing the parent [SKU](#sku). **Note** This ID can change over time. You should only rely on this value within a short time after retrieving it. It should only be accessed and used at the time of purchase.  |
| defaultCurrency | string                        | The default currency supported for this availability.                               |
| segment         | string                        | The industry segment for this availability. Supported values are: Commercial, Education, Government, NonProfit. |
| country         | string                                              | The country or region (in ISO country code format) where this availability applies. |
| isPurchasable   | bool                                                | Indicates whether this availability is purchasable. |
| isRenewable     | bool                                                | Indicates whether this availability is renewable. |
| product      | [Product](#product)               | The product this availability corresponds to. |
| sku          | [Sku](#sku)            | The SKU this availability corresponds to. |
| terms           | array of [Term](#term) resources  | The collection of terms that are applicable to this availability. |
| links           | [ResourceLinks](utility-resources.md#resourcelinks) | The resource links contained within the availability. |

## Term

Represents a term for which the availability can be purchased.

| Property              | Type                                        | Description                                                                         |
|-----------------------|-----------------------------------------------------------------------------------|-------------------------------------------------------------------------------------|
| duration              | string                                      | An ISO 8601 representation of the term's duration. The current supported values are P1M (1 month), P1Y (1 year) and P3Y (3 years). |
| description           | string                                      | The description of the term.           |

## InventoryCheckRequest

Represents a request to check inventory against certain catalog items.

| Property         | Type                                                | Description                                                                                 |
|------------------|-----------------------------------------------------|---------------------------------------------------------------------------------------------|
| targetItems      | array of [InventoryItem](#inventoryitem)            | The list of catalog items that the inventory check will evaluate.                           |
| inventoryContext | key/value pairs                                     | The dictionary of context values that are needed to carry out the inventory check(s). Each [SKU](#sku) of the products will define which values (if any) are needed to carry out this operation.  |
| links            | [ResourceLinks](utility-resources.md#resourcelinks) | The resource links contained within the inventory check request.                            |

## InventoryItem

Represents a single item in an inventory check operation. This resource is used for specifying the target items in an input request and is also used to represent the output results of the inventory check operation.

| Property         | Type                                                              | Description                                                                      |
|------------------|-------------------------------------------------------------------|----------------------------------------------------------------------------------|
| productId        | string                                                            | (Required) The ID of the [product](#product).                            |
| skuId            | string                                                            | The ID of the [SKU](#sku). When using this resource as input to an inventory request, this value is optional. If this value isn't provided, then all SKUs under the product will be considered as target items of the inventory check operation.      |
| isRestricted     | bool                                                              | Indicates whether this item was found to have a restricted inventory.            |
| restrictions     | array of [InventoryRestriction](#inventoryrestriction)            | The details of any restrictions that are found for this item. This property will only be populated if **isRestricted** = "true". |

## InventoryRestriction

Represents the details of an inventory restriction. This is only applicable for inventory check output results, not for input requests.

| Property         | Type                  | Description                                                                                 |
|------------------|-----------------------|---------------------------------------------------------------------------------------------|
| reasonCode       | string                | The code that identifies the reason for the restriction.                                    |
| description      | string                | The description of the inventory restriction.                                               |
| properties       | key/value pairs       | The dictionary of properties that may provide further details on the restriction.           |

## BillingCycleType

An [Enum/dotnet/api/system.enum) with values that indicate a type of billing cycle.

| Value              | Position     | Description                                                                                |
|--------------------|--------------|--------------------------------------------------------------------------------------------|
| Unknown            | 0            | Enum initializer.                                                                          |
| Monthly            | 1            | Indicates that the partner will be charged monthly.                                        |
| Annual             | 2            | Indicates that the partner will be charged annually.                                       |
| None               | 3            | Indicates that the partner will not be charged. This value may be used for trial items.    |
| OneTime            | 4            | Indicates that the partner will be charged one time.                                       |

## AttestationProperties

Represents an attestation type and if it is required for purchase.

| Property              | Type                                        | Description                                                                         |
|-----------------------|-----------------------------------------------------------------------------------|-------------------------------------------------------------------------------------|
| attestationType              | string                                      | Indicates the attestation type. For Windows 365 the value is Windows365. Windows 365 attestation text is "I understand that each person using Windows 365 Business with Windows Hybrid Benefit also needs to have a valid copy of Windows 10/11 Pro installed on their primary work device." |
| enforceAttestation           | boolean                                      | Indicates whether attestation is required for purchase.           |
