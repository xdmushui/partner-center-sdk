---
title: Create a subscription for commercial marketplace products
description: Developers can create and manage a subscription for commercial marketplace products using Partner Center APIs.

ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice:  partnercenter-sdk
ms.localizationpriority: medium
---

# Create a subscription for commercial marketplace products

**Applies to:**

* Partner Center

You can create a subscription for commercial marketplace products using Partner Center APIs. You must [get a list of offers for a market](#get-a-list-of-offers-for-a-market), [create and submit an order](#create-and-submit-an-order) for a commercial marketplace subscription, then [retrieve an activation link](#get-activation-link).

You can also [perform lifecycle management](#lifecycle-management) and [manage invoices](#invoice-and-reconciliation) for these subscriptions.

## Prerequisites

* [Partner Center authentication](partner-center-authentication.md) credentials. This scenario supports authentication with both standalone App and App+User credentials.
* The customer identifier. If you don't have a customer's identifier, follow the steps in [Get a list of customers](get-a-list-of-customers.md). Alternatively, sign in to Partner Center, choose the customer from the list of customers, select **Account**, then save their **Microsoft ID**.

## Get a list of offers for a market

You can check the available offers for a market using the following Partner Center API models:

* **[Product](product-resources.md#product)**: A grouping construct for purchasable goods or services. A product itself isn't a purchasable item.
* **[SKU](product-resources.md#sku)**: A purchasable Stock Keeping Unit (SKU) under a product. These represent the different shapes of the product.
* **[Availability](product-resources.md#availability)**: A configuration in which a SKU is available for purchase (such as country, currency, or industry segment).

Before you purchase an Azure reservation, complete the following steps:

1. Identify and retrieve the product and SKU that you want to purchase. If you already know the Product ID and SKU ID, select them.

    * [Get a list of products](get-a-list-of-products.md)
    * [Get a product using the product ID](get-a-product-by-id.md)
    * [Get a list of SKUs for a product](get-a-list-of-skus-for-a-product.md)
    * [Get a SKU using the SKU ID](get-a-sku-by-id.md)

    > [!NOTE]
    > You can identify commercial marketplace products by their **ProductType** property of **"Azure"** and their **SubType** property of **"SaaS"**.

2. If the SKUs are tagged with an **InventoryCheck** prerequisite, [check the inventory for a SKU](check-inventory.md).

    > [!NOTE]
    > At this time, there are no commercial marketplace products that support inventory check or are tagged with an **InventoryCheck** prerequisite.

3. Retrieve the availability for the SKU. You will need the **CatalogItemId** of the availability when placing the order, which you can retrieve through the following APIs:

    * [Get a list of availabilities for a SKU](get-a-list-of-availabilities-for-a-sku.md)
    * [Get an availability using the availability ID](get-an-availability-by-id.md)

## Create and submit an order

To submit your Azure reservation order, follow these steps:

1. [Create a cart](create-a-cart.md) to hold the collection of catalog items that you intend to buy. When you create a [cart](cart-resources.md#cart), the [cart line items](cart-resources.md#cartlineitem) are automatically grouped based on what can be purchased together in the same [order](order-resources.md#order). (You can also [update a cart](update-a-cart.md).)
2. [Check out the cart](checkout-a-cart.md), which results in the creation of an [order](order-resources.md#order).

### Get order details

You can [retrieve the details of an individual order using the order ID](get-an-order-by-id.md). You can also [retrieve a list of all orders for a specific customer](get-all-of-a-customer-s-orders.md).

> [!NOTE]
> After an order is submitted, there is a delay of up to 15 minutes before the order appears in that customer's order list.

## Get activation link

The partner or customer must activate subscriptions to Azure Marketplace products. You can [get an activation link by order line item](get-activation-link-by-order-line-item.md). You can also [get a subscription by ID](get-a-subscription-by-id.md), then enumerate its **Links** property to create an activation link.

## Lifecycle management

You can manage the lifecycle of your subscriptions to commercial marketplace products using the following methods:

* [Cancel a commercial marketplace subscription](cancel-an-azure-marketplace-subscription.md)
* [Enable or disable autorenew for a commercial marketplace subscription](update-autorenew-for-an-azure-marketplace-subscription.md)

## Quantity management

The quantity of a commercial marketplace subscription must be within the limits defined by its associated [SKU](product-resources.md#sku) (see the **minimumQuantity** and **maximumQuantity** attributes). To update the quantity of a commercial marketplace subscription, use the following method:

* [Change the quantity of a subscription](change-the-quantity-of-a-subscription.md)

## Invoice and reconciliation

You can manage customer [invoices](invoice-resources.md) (including charges for subscriptions to commercial marketplace products) using the following methods:

* [Get invoice billed commercial marketplace consumption line items](get-invoice-billed-consumption-lineitems.md)
* [Get invoice estimate links](get-invoice-estimate-links.md)
* [Get invoice unbilled commercial marketplace consumption line items](get-invoice-unbilled-consumption-lineitems.md)
* [Get invoice unbilled reconciliation line items](get-invoice-unbilled-recon-lineitems.md)

## Test using integration sandbox account

In production, after you have created a subscription to commercial marketplace SaaS products, you need to retrieve a personalized activation link from Partner Center and visit the publisher's site to complete the setup process. Subscription billing will begin only after setup is complete.

In the CSP sandbox environment, there is no integration with ISVs. If you try to retrieve an activation link from Partner Center, a dummy link will be returned. You cannot use this dummy link to complete the setup process at the publisher's site. To use the integration sandbox account to test billing for subscriptions to commercial marketplace SaaS products, use the following method to activate the subscription instead. Subscription billing will begin after successful activation:

* [Activate a sandbox subscription for commercial marketplace products](activate-sandbox-subscription-azure-marketplace-products.md)

