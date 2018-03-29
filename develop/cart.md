---
title: Cart
description: A partner places an order when a customer wants to buy a subscription from a list of offers.
ms.assetid: 
ms.author: v-thpr
ms.date: 03/16/2018
ms.topic: article
ms.prod: partner-center
ms.technology: partner-center-sdk
---

# Cart

[This information relates to pre-released product which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.]

<span class="sidebar_heading" style="font-weight: bold;">Applies
To</span>

-   Partner Center


A partner places an order when a customer wants to buy a subscription from a list of offers.



## <span id="cart"></span><span id="CART"></span>Cart


Describes a cart.

| Property            | Type                                                           | Description                                                 |
|---------------------|----------------------------------------------------------------|-------------------------------------------------------------|
| id                  | string                                                         | A cart identifier that is supplied upon successful creation of the cart.   |
|CreationTimeStamp    | DateTime                                                       | The date the cart was created, in date-time format. Applied upon successful creation of the cart. |
| LastModifiedTimeStamp | DateTime                                                     | The date the cart was last updated, in date-time format. Applied upon successful creation of the cart.   |
| ExpirationTimeStamp   | DateTime                                                     | The date the cart will expire, in date-time format. Applied upon successful creation of cart.                |
| LastModifiedUser    | string                                                         | The user who last updated the cart. Applied upon successful creation of cart.   |
| lineItems           | Array of objects                                               | An Array of [CartLineItem](#cart-line-item) resources.                          |



## <span id="cartLineItem"></span><span id="cartlineitem"></span><span id="CARTLINEITEM"></span>CartLineItem


Represents one item contained in a cart.

| Property             | Type                                      | Description                                                                                                                                                                                                                                |
|----------------------|-------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id                   | string                                    | A Unique identifier for a cart line item.
Applied upon successful creation of cart.                                                                                                                                                                                                                       |
| catalogId            | string                                    | The catalog item identifier.                                                                                                                                                                                                                |
| friendlyName         | string                                    | Optional. The friendly name for the item defined by the partner to help disambiguate.                                                                                                                                              |
| quantity             | int                                       | The number of licenses for a licence-based subscription or instances for an Azure reservation.                                                                                                                                                                                |
| currencyCode         | string                                    | The currency code.                                                                                                                                                                                |
| billingCycle         | Object                                    | The type of billing cycle set for the current period.    |
| Participants         | List of Object String pairs               | A collection of participants on the purchase.     |
| provisioningContext  | Dictionary<string, string>                | A context used for provisioning of offer.                                                                                                                                               |
| orderGroup           | string                                    | A group to indicate which items can be placed together.    |
| purchaseSystem       | string                                    | Which purchase system to place order to.    |
| error                | Object                                    | Applied after cart is created in case of an error.    |

 

## <span id="cartError"></span><span id="carterror"></span><span id="CARTERROR"></span>CartError


Represents an error that occurs after a cart is created.

| Property           | Type                                         | Description                                                                                   |
|--------------------|----------------------------------------------|-----------------------------------------------------------------------------------------------|
| <name>             | <type>                                       | The error description, including any notes about supported values, default values, or limits. |




 




