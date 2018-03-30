---
title: Scenarios
description: This section describes the ways that partners in the Cloud Solution Provider program can use the Partner Center API to programmatically manage customer accounts, partner accounts, orders, subscriptions, support, and billing.
ms.assetid: D278B9D1-D5B9-4FAD-89D8-44244715D6C9
ms.author: v-thpr
ms.date: 12/15/2017
ms.topic: article
ms.prod: partner-center
ms.technology: partner-center-sdk
---

# Scenarios

[This information relates to pre-released product which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.]

**Applies To**

-   Partner Center
-   Partner Center operated by 21Vianet
-   Partner Center for Microsoft Cloud Germany
-   Partner Center for Microsoft Cloud for US Government

This section describes the ways that partners in the Cloud Solution Provider program can use the Partner Center API to programmatically manage customer accounts, partner accounts, orders, subscriptions, support, and billing.

Note that there are different versions of Partner Center available that include different capabilities. Not all scenarios are supported in all versions of Partner Center. To learn more, see [Developing for Partner Center for Microsoft National Cloud](developing-for-partner-center-for-microsoft-national-cloud.md).

## <span id="Scenarios_supported_by_the_Partner_Center_SDK"></span><span id="scenarios_supported_by_the_partner_center_sdk"></span><span id="SCENARIOS_SUPPORTED_BY_THE_PARTNER_CENTER_SDK"></span>Scenarios supported by the Partner Center SDK


All of the following scenarios can be completed three different ways:

-   manually in the [Partner Center](http://go.microsoft.com/fwlink/p/?LinkId=620294) dashboard.
-   programmatically by using the Partner Center managed API.
-   programmatically by using the Partner Center REST API.

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>[Analytics](usage-analytics.md)</p></td>
<td><p>Retrieve analytics</p>
<ul>
<li><p>[Get partner licenses deployment information](get-partner-licenses-deployment-information.md)</p></li>
<li><p>[Get partner licenses usage information](get-partner-licenses-usage-information.md)</p></li>
<li><p>[Get customer licenses deployment information](get-customer-licenses-deployment-information.md)</p></li>
<li><p>[Get customer licenses usage information](get-customer-licenses-usage-information.md)</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>[Device Deployment](device-deployment.md)</p></td>
<td><p>Configuration policies</p>
<p>Add, delete, update and retrieve device configuration policies.</p>
<ul>
<li><p>[Create a new configuration policy for the specified customer](create-a-new-configuration-policy-for-the-specified-customer.md)</p></li>
<li><p>[Delete a configuration policy for the specified customer](delete-a-configuration-policy-for-the-specified-customer.md)</p></li>
<li><p>[Get a list of a customer's policies](get-a-list-of-a-customer-s-policies.md)</p></li>
<li><p>[Retrieve a customer's configuration policy](retrieve-a-customer-s-configuration-policy.md)</p></li>
<li><p>[Update a configuration policy for the specified customer](update-a-configuration-policy-for-the-specified-customer.md)</p></li>
</ul>
<p>Devices</p>
<p>Work with and upload device batches and device metadata.</p>
<ul>
<li><p>[Get the status of a device batch upload](get-the-status-of-a-device-batch-upload.md)</p></li>
<li><p>[Get a list of device batches for the specified customer](get-the-list-of-device-batches-for-the-specified-customer.md)</p></li>
<li><p>[Get a list of devices for the specified batch and customer](get-a-list-of-devices-for-the-specified-batch-and-customer.md)</p></li>
<li><p>[Upload a list of devices to create a new batch for the specified customer](upload-a-list-of-devices-to-create-a-new-batch-for-the-specified-customer.md)</p></li>
<li><p>[Upload a list of devices to an existing batch for the specified customer](upload-a-list-of-devices-for-the-specified-customer.md)</p></li>
<li><p>[Delete a device for the specified customer](delete-a-device-for-the-specified-customer.md)</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>[Manage customer accounts](manage-customers.md)</p></td>
<td><p>Create a customer</p>
<ul>
<li><p>[Create a customer](create-a-customer.md)</p></li>
<li><p>[Create a customer for an indirect reseller](create-a-customer-for-an-indirect-reseller.md)</p></li>
<li><p>[Retrieve a relationship request URL](request-reseller-relationship.md)</p></li>
<li><p>[Remove a reseller relationship with a customer](remove-a-reseller-relationship-with-a-customer.md)</p></li> 
</ul>
<p>Look up a customer</p>
<ul>
<li><p>[Get a customer by ID](get-a-customer-by-id.md)</p></li>
<li><p>[Get a list of customers filtered by a search field](get-a-customer-by-name.md)</p></li>
<li><p>[Get a list of customers](get-a-list-of-customers.md)</p></li>
</ul>
<p>Manage customer orders and subscriptions</p>
<ul>
<li><p>[Get all of a customer's orders](get-all-of-a-customer-s-orders.md)</p></li>
<li><p>[Get a list of orders by customer and billing cycle type](get-a-list-of-orders-by-customer-and-billing-cycle-type.md)</p></li>
<li><p>[Get a collection of entitlements](get-a-collection-of-entitlements.md)</p></li> 
<li><p>[Get a customer's subscriptions](get-all-of-a-customer-s-subscriptions.md)</p></li>
<li><p>[Update the nickname for a subscription](update-the-nickname-for-a-subscription.md)</p></li>
</ul>
<p>Manage customer account details</p>
<ul>
<li><p>[Get a customer's billing profile](get-all-of-a-customer-s-billing-profiles.md)</p></li>
<li><p>[Update a customer's billing profile](update-a-customer-s-billing-profile.md)</p></li>
<li><p>[Get a customer's company profile](get-a-customer-s-company-profile.md)</p></li>
<li><p>[Update a customer's usage spending budget](update-a-customer-s-usage-spending-budget.md)</p></li>
<li><p>[Add a verified domain for a customer](add-a-verified-domain-for-a-customer.md)</p></li>
</ul>
<p>Manage user accounts and assign licenses</p>
<ul>
<li><p>[Get a user account by ID](get-a-user-account-by-id.md)</p></li>
<li><p>[Create user accounts for a customer](create-user-accounts-for-a-customer.md)</p></li>
<li><p>[Delete a user account for a customer](delete-user-accounts-for-a-customer.md)</p></li>
<li><p>[Update user accounts for a customer](update-user-accounts-for-a-customer.md)</p></li>
<li><p>[View deleted users for a customer](view-a-deleted-user.md)</p></li>
<li><p>[Restore a deleted user for a customer](restore-a-user-for-a-customer.md)</p></li>
<li><p>[Get a list of all user accounts for a customer](get-a-list-of-all-user-accounts-for-a-customer.md)</p></li>
<li><p>[Reset user password for a customer](reset-user-password-for-a-customer.md)</p></li>
<li><p>[Get user roles for a customer](get-user-roles-for-a-customer.md)</p></li>
<li><p>[Set user roles for a customer](set-user-roles-for-a-customer.md)</p></li>
<li><p>[Remove a customer user from a role](remove-customer-user-from-a-role.md)</p></li>
<li><p>[Get a list of available licenses](get-a-list-of-available-licenses.md)</p></li>
<li><p>[Assign licenses to a user](assign-licenses-to-a-user.md)</p></li>
<li><p>[Get licenses assigned to a user](check-which-licenses-are-assigned-to-a-user.md)</p></li>
<li><p>[Get licenses assigned to a user by license group](get-licenses-assigned-to-a-user-by-license-group.md)</p></li>
<li><p>[Get a list of available licenses by license group](get-a-list-of-available-licenses-by-license-group.md)</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>[Place orders](place-orders.md)</p></td>
<td><p>Purchase Azure Reserved VM Instances</p>
<ul>
<li><p>[Purchase Azure Reserved VM Instances](purchase-azure-reserved-vm-instances.md)</p></li>
</ul>
<p>Get offers from the catalog</p>
<ul>
<li><p>[Get a list of offer categories by market](get-a-list-of-offer-categories-by-country-and-locale.md)</p></li>
<li><p>[Get a list of offers for a market](get-a-list-of-offers-for-a-market.md)</p></li>
<li><p>[Get an offer by ID](get-an-offer-by-id.md)</p></li>
<li><p>[Get add-ons for an offer ID](get-addon-offers-by-offer-id.md)</p></li>
<li><p>[Get a list of products](get-a-list-of-products.md)</p></li>
<li><p>[Get a product by ID](get-a-product-by-id.md)</p></li>
<li><p>[Get a list of SKUs for a product](get-a-list-of-skus-for-a-product.md)</p></li>
<li><p>[Get a SKU by ID](get-a-sku-by-id.md)</p></li>
<li><p>[Get a list of availabilities for a SKU](get-a-list-of-availabilities-for-a-sku.md)</p></li>
<li><p>[Get an availability by ID](get-an-availability-by-id.md)</p></li>
<li><p>[Check Inventory](check-inventory.md)</p></li>
</ul>
<p>Create an order</p>
<ul>
<li><p>[Create a cart](create-a-cart.md)</p></li>
<li><p>[Update a cart](update-a-cart.md)</p></li>
<li><p>[Checkout a cart](checkout-a-cart.md)</p></li>
<li><p>[Create an order](create-an-order.md)</p></li>
<li><p>[Create an order for a customer of an indirect reseller](create-an-order-for-a-customer-of-an-indirect-reseller.md)</p></li>
<li><p>[Get an order by ID](get-an-order-by-id.md)</p></li>
<li><p>[Purchase an add-on to a subscription](purchase-an-add-on-to-a-subscription.md)</p></li>
</ul>
<p>Enable a subscription for Azure Reserved VM Instance purchases</p>
<ul>
<li><p>[Register a subscription](register-a-subscription.md)</p></li>
<li><p>[Get subscription registration status](get-subscription-registration-status.md)</p></li>
</ul>
<p>Trial conversions</p>
<ul>
<li><p>[Get a list of trial conversion offers](get-a-list-of-trial-conversion-offers.md)</p></li>
<li><p>[Convert a trial subscription to paid](convert-a-trial-subscription-to-paid.md)</p></li>
</ul>
<p>Get subscription details</p>
<ul>
<li><p>[Get a subscription by ID](get-a-subscription-by-id.md)</p></li>
<li><p>[Get a list of subscriptions by order](get-a-list-of-subscriptions-by-order.md)</p></li>
<li><p>[Get a list of add-ons for a subscription](get-a-list-of-add-ons-for-a-subscription.md)</p></li>
<li><p>[Get subscription provisioning status](get-subscription-provisioning-status.md)</p></li>
</ul>
<p>Change, suspend, or reactivate a subscription</p>
<ul>
<li><p>[Change the quantity of a subscription](change-the-quantity-of-a-subscription.md)</p></li>
<li><p>[Suspend a subscription](suspend-a-subscription.md)</p></li>
<li><p>[Reactivate a suspended subscription](reactivate-a-suspended-a-subscription.md)</p></li>
<li><p>[Transition a subscription](transition-a-subscription.md)</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>[Manage billing](manage-invoices.md)</p></td>
<td><p>Get Azure rates and utilization records</p>
<ul>
<li><p>[Get prices for Microsoft Azure](get-prices-for-microsoft-azure.md)</p></li>
<li><p>[Get a customer's utilization records for Azure](get-a-customer-s-utilization-record-for-azure.md)</p></li>
</ul>
<p>Get invoices</p>
<ul>
<li><p>[Get the partner's current account balance](get-the-reseller-s-current-account-balance.md)</p></li>
<li><p>[Get an invoice by ID](get-invoice-by-id.md)</p></li>
<li><p>[Get invoice line items](get-invoiceline-items.md)</p></li>
<li><p>[Get invoice statement](get-invoice-statement.md)</p></li>
<li><p>[Get invoice summaries](get-invoice-summaries.md)</p></li>
<li><p>[Get a collection of invoices](get-a-collection-of-invoices.md)</p></li>
</ul>
<p>Check your Azure spending budget</p>
<ul>
<li><p>[Get usage data for a subscription](get-a-subscriptions-resource-usage-information.md)</p></li>
<li><p>[Get a usage summary for all of a customer's subscriptions](get-a-customers-rated-usage-information.md)</p></li>
</ul>
<p>Get service costs</p>
<ul>
<li><p>[Get a customer's service costs summary](get-a-customer-s-service-costs-summary.md)</p></li>
<li><p>[Get a customer's service costs line items](get-a-customer-s-service-costs-line-items.md)</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>[Provide support](provide-support.md)</p></td>
<td><p>Administer services for a customer</p>
<ul>
<li><p>[Get the managed services for a customer by ID](get-the-managed-services-for-a-customer-by-id.md)</p></li>
</ul>
<p>Manage support contacts</p>
<ul>
<li><p>[Get a subscription's support contact](get-a-subscription-s-support-contact.md)</p></li>
<li><p>[Update a subscription's support contact](update-a-subscription-s-support-contact.md)</p></li>
</ul>
<p>Manage service requests</p>
<ul>
<li><p>[Create a service request](create-a-service-request-.md)</p></li>
<li><p>[Get service request support topics](get-service-request-support-topics--pending-.md)</p></li>
<li><p>[Get all service requests for a customer](get-all-service-requests-for-a-customer.md)</p></li>
<li><p>[Get service request details by ID](get-service-request-details-by-id.md)</p></li> 
<li><p>[Update a service request](update-a-service-request.md)</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>[Manage accounts and profiles](manage-profiles-and-information.md)</p></td>
<td><p>Work with accounts and profiles</p>
<ul>
<li><p>[Get the partner legal business profile](get-legal-business-profile.md)</p></li>
<li><p>[Get an organization profile](get-an-organization-profile.md)</p></li>
<li><p>[Get partner billing profile](get-partner-billing-profile.md)</p></li>
<li><p>[Get Microsoft Partner Network profile](get-partner-network-profile.md)</p></li>
<li><p>[Get support profile](get-support-profile.md)</p></li>
<li><p>[Update the partner legal business profile](update-legal-business-profile.md)</p></li>
<li><p>[Update the partner billing profile](update-partner-billing-profile.md)</p></li>
<li><p>[Update support profile](update-support-profile.md)</p></li>
<li><p>[Update an organization profile](update-an-organization-profile.md)</p></li>
<li><p>[Verify a partner MPN ID](get-partner-by-mpn-id.md)</p></li>
<li><p>[Get a customer's subscriptions by partner MPN ID](get-all-subscriptions-by-partner.md)</p></li>
<li><p>[Get customers of an indirect reseller](get-customers-of-an-indirect-reseller.md)</p></li>
<li><p>[Get indirect resellers of a customer](get-indirect-resellers-of-a-customer.md)</p></li>
<li><p>[Retrieve a list of indirect resellers](retrieve-a-list-of-indirect-resellers.md)</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>[Utilities](utilities.md)</p></td>
<td><ul>
<li><p>[Validate an address](validate-an-address.md)</p></li>
<li><p>[Get address formatting rules by market](get-market-specific-validation-data.md)</p></li>
<li><p>[Verify domain availability](verify-domain-availability.md)</p></li>
<li><p>[Delete a customer account from the integration sandbox](delete-a-customer-account-from-the-integration-sandbox.md)</p></li>
<li><p>[Get a record of Partner Center activity](get-a-record-of-partner-center-activity-by-user.md)</p></li>
</ul></td>
</tr>
</tbody>
</table>

 

## <span id="background"></span><span id="BACKGROUND"></span>Background


### <span id="Who_is_involved_in_the_order_process_"></span><span id="who_is_involved_in_the_order_process_"></span><span id="WHO_IS_INVOLVED_IN_THE_ORDER_PROCESS_"></span>Who is involved in the order process?

Microsoft, distributors, resellers, and customers. The distributors and resellers are often referred to as **partners**.

Sometimes, Microsoft works directly with resellers who sell to customers. Alternately, Microsoft also works with distributors, and those distributors work with their own set or channel of resellers who sell to customers.

### <span id="What_s_getting_sold_______"></span><span id="what_s_getting_sold_______"></span><span id="WHAT_S_GETTING_SOLD_______"></span>What's getting sold?

Microsoft provides a list of **offers**. These are specific SKUs of products like Office 365 or Intune. Offers are either **license-based** (the cost depends on the number of machines they get installed on) or **usage-based** (the cost depends on the amount of memory and computation used). For more information, see [CSP agreements, price lists, and offers](https://msdn.microsoft.com/partner-center/csp-documents-and-learning-resources).

CSP partners are resellers who have customers and sell them Microsoft products from the current offer list. After the customers sign their agreement, the reseller places an **order** for one or more offers. Some offers include **add-ons** like more space or extra features, which are tracked together with the parent offer. The orders are processed, and then the customer is able to use their **subscriptions**. Microsoft bills the reseller or distributor each month based on the number of licenses and the usage for each customer.

Subscriptions can be added, and the number of seats or add-ons can be increased or decreased. If a customer fails to pay, misuses the subscription, or engages in fraud, then Microsoft, the distributor, or the reseller are all able to suspend the subscription. It will be permanent if it's not reactivated within the limits of the CSP program.

You can check which subscriptions a customer is **entitled** to use (ie, which ones are currently paid for, not suspended, and not replaced by a newer order).

 

 




