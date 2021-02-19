---
title: Purchase new commerce license-based services
description: Developers can purchase, create, and manage new commerce license-based services using the Partner Center APIs.
ms.date: 02/24/2020
ms.service: partner-dashboard
ms.subservice:  partnercenter-sdk
author: BrentSerbus
ms.author: brserbus
---

# Purchasing new commerce license-based services

**Applies to:**

* Partner Center

> [!Note] 
> New Commerce changes are currently available only to partners who are part of the M365/D365 new commerce experience technical preview.

You can purchase, create, and manage new commerce experience  license-based services using the Partner Center APIs. The process is similar to such as Azure plan and Marketplace offers.

## Prerequisites

* [Partner Center authentication](partner-center-authentication.md) credentials. The new commerce experience supports authentication with both standalone App and App+User credentials.
* The customer identifier. If you don't have a customer's identifier, follow the steps in [Get a list of customers](get-a-list-of-customers.md). Alternatively, sign in to Partner Center, choose the customer from the list of customers, select **Account**, then save their **Microsoft ID**.
* [Confirmation of the customer's acceptance of the Microsoft Customer Agreement](/partner-center/confirm-customer-agreement).

## Get the catalog item for new commerce license-based services

You need to retrieve new commerce license-based services catalog items. Retrieve catalog items using the existing Partner Center catalog APIs with the following resource models:

* **[Product](product-resources.md#product)**: A grouping construct for purchasable goods or services. A product itself isn't a purchasable item.
* **[SKU](product-resources.md#sku)**: A purchasable Stock Keeping Unit (SKU) under a product. SKUs represent the different shapes of the product.
* **[Availability](product-resources.md#availability)**: A configuration in which a SKU is available for purchase (such as country, currency, or industry segment).

To obtain the catalog items for new commerce license-based services offers:

1. Follow the steps in [Get a list of products](get-a-list-of-products.md) for products and specify the **targetView** as **OnlineServices**. (If you already know the product identifier for the offer you want to purchase, you can follow the steps in [Get a product using the product ID](get-a-product-by-id.md) instead.)

2. Retrieve the **SKU** from the product for the offer you are looking for. Follow the steps in [Get a list of SKUs for a product](get-a-list-of-skus-for-a-product.md). (If you already know the SKU identifier for the offer you want, you can follow the steps in [Get a SKU using the SKU ID](get-a-sku-by-id.md) instead.)

3. Retrieve the **availability** from the SKU for the offer. Different offers support specific terms. Some SKUs have more than one availability. Follow the steps in [Get a list of availabilities for a SKU](get-a-list-of-availabilities-for-a-sku.md). (If you already know the identifier for the availability you need, you can follow the steps in [Get an availability using the availability ID](get-an-availability-by-id.md) instead.) *Be sure to note the value of the **CatalogItemId** property of the availability for the offer. You will need this value to create an order*.

## Create and submit an order

To submit your order for an Azure plan (including new commerce orders), follow these steps:

1. [Create a cart](create-a-cart.md) to hold the collection of catalog items that you intend to buy. When you create a [cart](cart-resources.md#cart), the [cart line items](cart-resources.md#cartlineitem) are automatically grouped based on what can be purchased together in the same [order](order-resources.md#order). (You can also [update a cart](update-a-cart.md).)

2. [Check out the cart](checkout-a-cart.md), which results in the creation of an [order](order-resources.md#order).

## Get order details

You can [retrieve the details of an individual order using the order ID](get-an-order-by-id.md). You can also [retrieve a list of all orders for a specific customer](get-all-of-a-customer-s-orders.md).

>[!NOTE]
>After an order is submitted, there is a delay of up to 15 minutes before the order appears in that customer's order list. 
>Currently, EU partners can only purchase new commerce offers for: 1. New customers 2. Existing customers who don’t have a pre-existing Azure plan, marketplace, software subscriptions or perpetual software in a currency other than the partner’s country currency.

## Manage new commerce subscriptions

After the order is successfully processed, a Partner Center **Subscription** resource will be created for the Azure plan. You can use the following methods for managing Partner Center **Subscription** resources to manage the Azure plan:

* [Get a customer's subscriptions](get-all-of-a-customer-s-subscriptions.md)
* [Get a list of subscriptions by order](get-a-list-of-subscriptions-by-order.md)

There are differences and new capabilities specific to new commerce.

## Invoice and reconciliation

You can manage invoices and reconciliation data using the following methods:

* [Get a collection of invoices](get-a-collection-of-invoices.md)
* [Get invoice estimate links](get-invoice-estimate-links.md)
* [Get invoice by ID](get-invoice-by-id.md)
* [Get invoice statement](get-invoice-statement.md)
* [Get invoice summaries](get-invoice-summaries.md)
* [Get invoice billed consumption line items](get-invoice-billed-consumption-lineitems.md)
* [Get invoice unbilled consumption line items](get-invoice-unbilled-consumption-lineitems.md)
* [Get invoice billed recon line items](get-invoiceline-items.md)
* [Get invoice unbilled recon line items](get-invoice-unbilled-recon-lineitems.md)
