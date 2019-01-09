---
title: Scenarios
description: This section describes the ways that partners in the Cloud Solution Provider program can use the Partner Center API to programmatically manage customer accounts, partner accounts, orders, subscriptions, support, and billing.
ms.assetid: D278B9D1-D5B9-4FAD-89D8-44244715D6C9
ms.date: 12/15/2017
ms.localizationpriority: medium
---

# Scenarios


**Applies To**

 - Partner Center
 - Partner Center operated by 21Vianet
 - Partner Center for Microsoft Cloud Germany
 - Partner Center for Microsoft Cloud for US Government

This section describes the ways that partners in the Cloud Solution Provider program can use the Partner Center API to programmatically manage customer accounts, partner accounts, orders, subscriptions, support, and billing.

Note that there are different versions of Partner Center available that include different capabilities. Not all scenarios are supported in all versions of Partner Center. To learn more, see [Developing for Partner Center for Microsoft National Cloud](developing-for-partner-center-for-microsoft-national-cloud.md).

## <span id="Scenarios_supported_by_the_Partner_Center_SDK"/><span id="scenarios_supported_by_the_partner_center_sdk"/><span id="SCENARIOS_SUPPORTED_BY_THE_PARTNER_CENTER_SDK"/>Scenarios supported by the Partner Center SDK


All of the following scenarios can be completed three different ways:

 - manually in the [Partner Center](http://go.microsoft.com/fwlink/p/?LinkId=620294) dashboard.
 - programmatically by using the Partner Center managed API.
 - programmatically by using the Partner Center REST API.

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr>
<td><p><a href="usage-analytics.md">Analytics</a></p></td>
<td><p>Retrieve analytics</p>
<ul>
<li><p><a href="partner-center-analytics-resources.md">Partner Center Analytics - Resources</a></p></li>
<li><p><a href="get-all-azure-usage-analytics.md">Get all Azure usage analytics information</a></p></li>
<li><p><a href="get-all-indirect-resellers-analytics.md">Get all indirect resellers analytics information</a></p></li>
<li><p><a href="get-all-referrals-analytics.md">Get all referrals analytics information</a></p></li>
<li><p><a href="get-all-search-analytics.md">Get all search analytics information</a></p></li>
<li><p><a href="get-all-subscription-analytics.md">Get all subscription analytics information</a></p></li>
<li><p><a href="get-subscription-analytics-by-search-query.md">Get subscription analytics information filtered by a search query</a></p></li>
<li><p><a href="get-subscription-analytics-grouped-by-dates-or-terms.md">Get subscription analytics information grouped by dates or terms</a></p></li>
<li><p><a href="get-licenses-deployment-information.md">Get licenses deployment information</a></p></li>
<li><p><a href="get-licenses-usage-information.md">Get licenses usage information</a></p></li>
<li><p><a href="get-customer-licenses-deployment-information.md">Get customer licenses deployment information</a></p></li>
<li><p><a href="get-customer-licenses-usage-information.md">Get customer licenses usage information</a></p></li>
<li><p><a href="get-partner-licenses-deployment-information.md">Get partner licenses deployment information</a></p></li>
<li><p><a href="get-partner-licenses-usage-information.md">Get partner licenses usage information</a></p></li>
</ul></td>
</tr>
<tr>
<td><p><a href="device-deployment.md">Device Deployment</a></p></td>
<td><p>Configuration policies</p>
<p>Add, delete, update and retrieve device configuration policies.</p>
<ul>
<li><p><a href="create-a-new-configuration-policy-for-the-specified-customer.md">Create a new configuration policy for the specified customer</a></p></li>
<li><p><a href="delete-a-configuration-policy-for-the-specified-customer.md">Delete a configuration policy for the specified customer</a></p></li>
<li><p><a href="get-a-list-of-a-customer-s-policies.md">Get a list of a customer&#39;s policies</a></p></li>
<li><p><a href="retrieve-a-customer-s-configuration-policy.md">Retrieve a customer&#39;s configuration policy</a></p></li>
<li><p><a href="update-a-configuration-policy-for-the-specified-customer.md">Update a configuration policy for the specified customer</a></p></li>
</ul>
<p>Devices</p>
<p>Work with and upload device batches and device metadata.</p>
<ul>
<li><p><a href="get-the-status-of-a-device-batch-upload.md">Get the status of a device batch upload</a></p></li>
<li><p><a href="get-the-list-of-device-batches-for-the-specified-customer.md">Get a list of device batches for the specified customer</a></p></li>
<li><p><a href="get-a-list-of-devices-for-the-specified-batch-and-customer.md">Get a list of devices for the specified batch and customer</a></p></li>
<li><p><a href="upload-a-list-of-devices-to-create-a-new-batch-for-the-specified-customer.md">Upload a list of devices to create a new batch for the specified customer</a></p></li>
<li><p><a href="upload-a-list-of-devices-for-the-specified-customer.md">Upload a list of devices to an existing batch for the specified customer</a></p></li>
<li><p><a href="delete-a-device-for-the-specified-customer.md">Delete a device for the specified customer</a></p></li>
</ul></td>
</tr>
<tr>
<td><p><a href="manage-customers.md">Manage customer accounts</a></p></td>
<td><p>Create a customer</p>
<ul>
<li><p><a href="create-a-customer.md">Create a customer</a></p></li>
<li><p><a href="create-a-customer-for-an-indirect-reseller.md">Create a customer for an indirect reseller</a></p></li>
<li><p><a href="request-reseller-relationship.md">Retrieve a relationship request URL</a></p></li>
<li><p><a href="remove-a-reseller-relationship-with-a-customer.md">Remove a reseller relationship with a customer</a></p></li> 
</ul>
<p>Look up a customer</p>
<ul>
<li><p><a href="get-a-customer-by-id.md">Get a customer by ID</a></p></li>
<li><p><a href="get-a-customer-by-name.md">Get a list of customers filtered by a search field</a></p></li>
<li><p><a href="get-a-list-of-customers.md">Get a list of customers</a></p></li>
</ul>
<p>Manage customer orders and subscriptions</p>
<ul>
<li><p><a href="get-all-of-a-customer-s-orders.md">Get all of a customer&#39;s orders</a></p></li>
<li><p><a href="get-a-list-of-orders-by-customer-and-billing-cycle-type.md">Get a list of orders by customer and billing cycle type</a></p></li>
<li><p><a href="get-a-collection-of-entitlements.md">Get a collection of entitlements</a></p></li> 
<li><p><a href="get-all-of-a-customer-s-subscriptions.md">Get a customer&#39;s subscriptions</a></p></li>
<li><p><a href="update-the-nickname-for-a-subscription.md">Update the nickname for a subscription</a></p></li>
</ul>
<p>Manage customer account details</p>
<ul>
<li><p><a href="get-all-of-a-customer-s-billing-profiles.md">Get a customer&#39;s billing profile</a></p></li>
<li><p><a href="update-a-customer-s-billing-profile.md">Update a customer&#39;s billing profile</a></p></li>
<li><p><a href="get-a-customer-s-company-profile.md">Get a customer&#39;s company profile</a></p></li>
<li><p><a href="update-a-customer-s-usage-spending-budget.md">Update a customer&#39;s usage spending budget</a></p></li>
<li><p><a href="add-a-verified-domain-for-a-customer.md">Add a verified domain for a customer</a></p></li>
<li><p><a href="confirm-customer-consent.md">Confirm customer acceptance of Microsoft Cloud agreement</a></p></li>
<li><p><a href="get-agreement-metadata.md">Get agreement metadata for Microsoft Cloud Agreement</a></p></li>
<li><p><a href="get-confirmation-of-customer-consent.md">Get confirmation of customer acceptance of Microsoft Cloud agreement</a></p></li>
<li><p><a href="get-a-partner-s-validation-codes.md">Get a partner's validation codes</a></p></li>
<li><p><a href="get-a-customer-s-qualification.md">Get a customer's qualification</a></p></li>
<li><p><a href="update-a-customer-s-qualification.md">Update a customer's qualification</a></p></li>
</ul>
<p>Manage user accounts and assign licenses</p>
<ul>
<li><p><a href="get-a-user-account-by-id.md">Get a user account by ID</a></p></li>
<li><p><a href="create-user-accounts-for-a-customer.md">Create user accounts for a customer</a></p></li>
<li><p><a href="delete-user-accounts-for-a-customer.md">Delete a user account for a customer</a></p></li>
<li><p><a href="update-user-accounts-for-a-customer.md">Update user accounts for a customer</a></p></li>
<li><p><a href="view-a-deleted-user.md">View deleted users for a customer</a></p></li>
<li><p><a href="restore-a-user-for-a-customer.md">Restore a deleted user for a customer</a></p></li>
<li><p><a href="get-a-list-of-all-user-accounts-for-a-customer.md">Get a list of all user accounts for a customer</a></p></li>
<li><p><a href="reset-user-password-for-a-customer.md">Reset user password for a customer</a></p></li>
<li><p><a href="get-user-roles-for-a-customer.md">Get user roles for a customer</a></p></li>
<li><p><a href="set-user-roles-for-a-customer.md">Set user roles for a customer</a></p></li>
<li><p><a href="remove-customer-user-from-a-role.md">Remove a customer user from a role</a></p></li>
<li><p><a href="get-a-list-of-available-licenses.md">Get a list of available licenses</a></p></li>
<li><p><a href="assign-licenses-to-a-user.md">Assign licenses to a user</a></p></li>
<li><p><a href="check-which-licenses-are-assigned-to-a-user.md">Get licenses assigned to a user</a></p></li>
<li><p><a href="get-licenses-assigned-to-a-user-by-license-group.md">Get licenses assigned to a user by license group</a></p></li>
<li><p><a href="get-a-list-of-available-licenses-by-license-group.md">Get a list of available licenses by license group</a></p></li>
</ul></td>
</tr>
<tr>
<td><p><a href="manage-orders.md">Manage orders</a></p></td>
<td><p>Purchase Azure Reserved VM Instances</p>
<ul>
<li><p><a href="purchase-azure-reservations.md">Purchase Azure reservations</a></p></li>
</ul>
<p>Make a one-time purchase</p>
<ul>
<li><p><a href="make-a-one-time-purchase.md">Make a one-time purchase</a></p></li> 
</ul>
<p>Get offers from the catalog</p>
<ul>
<li><p><a href="get-a-list-of-offer-categories-by-country-and-locale.md">Get a list of offer categories by market</a></p></li>
<li><p><a href="get-a-list-of-offers-for-a-market.md">Get a list of offers for a market</a></p></li>
<li><p><a href="get-an-offer-by-id.md">Get an offer by ID</a></p></li>
<li><p><a href="get-addon-offers-by-offer-id.md">Get add-ons for an offer ID</a></p></li>
<li><p><a href="get-a-list-of-products.md">Get a list of products</a></p></li>
<li><p><a href="get-a-product-by-id.md">Get a product by ID</a></p></li>
<li><p><a href="get-a-list-of-skus-for-a-product.md">Get a list of SKUs for a product</a></p></li>
<li><p><a href="get-a-sku-by-id.md">Get a list of availabilities for a SKU</a></p></li>
<li><p><a href="get-an-availability-by-id.md">Get an availability by ID</a></p></li>
<li><p><a href="check-inventory.md">Check Inventory</a></p></li>
</ul>
<p>Create an order</p>
<ul>
<li><p><a href="create-a-cart.md">Create a cart</a></p></li>
<li><p><a href="create-a-cart-with-add-ons.md">Create a cart with add-ons</a></p></li>
<li><p><a href="update-a-cart.md">Update a cart</a></p></li>
<li><p><a href="checkout-a-cart.md">Checkout a cart</a></p></li>
<li><p><a href="create-an-order.md">Create an order</a></p></li>
<li><p><a href="create-an-order-for-a-customer-of-an-indirect-reseller.md">Create an order for a customer of an indirect reseller</a></p></li>
<li><p><a href="get-an-order-by-id.md">Get an order by ID</a></p></li>
<li><p><a href="purchase-an-add-on-to-a-subscription.md">Purchase an add-on to a subscription</a></p></li>
<li><p><a href="purchase-catalog-items.md">Purchase catalog items</a></p></li>
</ul>
<p>Enable a subscription for Azure Reserved VM Instance purchases</p>
<ul>
<li><p><a href="register-a-subscription.md">Register a subscription</a></p></li>
<li><p><a href="get-subscription-registration-status.md">Get subscription registration status</a></p></li>
</ul>
<p>Trial conversions</p>
<ul>
<li><p><a href="get-a-list-of-trial-conversion-offers.md">Get a list of trial conversion offers</a></p></li>
<li><p><a href="convert-a-trial-subscription-to-paid.md">Convert a trial subscription to paid</a></p></li>
</ul>
<p>Get subscription details</p>
<ul>
<li><p><a href="get-a-subscription-by-id.md">Get a subscription by ID</a></p></li>
<li><p><a href="get-a-list-of-subscriptions-by-order.md">Get a list of subscriptions by order</a></p></li>
<li><p><a href="get-a-list-of-add-ons-for-a-subscription.md">Get a list of add-ons for a subscription</a></p></li>
<li><p><a href="get-subscription-provisioning-status.md">Get subscription provisioning status</a></p></li>
</ul>
<p>Manage a subscription</p>
<ul>
<li><p><a href="change-the-quantity-of-a-subscription.md">Change the quantity of a subscription</a></p></li>
<li><p><a href="suspend-a-subscription.md">Suspend a subscription</a></p></li>
<li><p><a href="reactivate-a-suspended-a-subscription.md">Reactivate a suspended subscription</a></p></li>
<li><p><a href="transition-a-subscription.md">Transition a subscription</a></p></li>
<li><p><a href="cancel-a-subscription.md">Cancel a subscription</a></p></li>
</ul></td>
</tr>
<tr>
<td>
<p><a href="manage-billing.md">Manage billing</a></p></td>
<td><p>Billing cycle</p>
<ul>
<li><p><a href="change-the-billing-cycle.md">Change the billing cycle</a></p></li>
</ul>
<p>Get Azure rates and utilization records</p>
<ul>
<li><p><a href="get-prices-for-microsoft-azure.md">Get prices for Microsoft Azure</a></p></li>
<li><p><a href="get-a-customer-s-utilization-record-for-azure.md">Get a customer&#39;s utilization records for Azure</a></p></li>
</ul>
<p>Get invoices</p>
<ul>
<li><p><a href="get-the-reseller-s-current-account-balance.md">Get the partner&#39;s current account balance</a></p></li>
<li><p><a href="get-invoice-by-id.md">Get an invoice by ID</a></p></li>
<li><p><a href="get-invoiceline-items.md">Get invoice line items</a></p></li>
<li><p><a href="get-invoice-statement.md">Get invoice statement</a></p></li>
<li><p><a href="get-invoice-summaries.md">Get invoice summaries</a></p></li>
<li><p><a href="get-a-collection-of-invoices.md">Get a collection of invoices</a></p></li>
</ul>
<p>Check your Azure spending budget</p>
<ul>
<li><p><a href="get-a-subscriptions-resource-usage-information.md">Get usage data for a subscription</a></p></li>
<li><p><a href="get-a-customers-rated-usage-information.md">Get a usage summary for all of a customer&#39;s subscriptions</a></p></li>
</ul>
<p>Get service costs</p>
<ul>
<li><p><a href="get-a-customer-s-service-costs-summary.md">Get a customer&#39;s service costs summary</a></p></li>
<li><p><a href="get-a-customer-s-service-costs-line-items.md">Get a customer&#39;s service costs line items</a></p></li>
</ul></td>
</tr>
<tr>
<td><p><a href="provide-support.md">Provide support</a></p></td>
<td><p>Administer services for a customer</p>
<ul>
<li><p><a href="get-the-managed-services-for-a-customer-by-id.md">Get the managed services for a customer by ID</a></p></li>
</ul>
<p>Manage support contacts</p>
<ul>
<li><p><a href="get-a-subscription-s-support-contact.md">Get a subscription&#39;s support contact</a></p></li>
<li><p><a href="update-a-subscription-s-support-contact.md">Update a subscription&#39;s support contact</a></p></li>
</ul>
<p>Manage service requests</p>
<ul>
<li><p><a href="create-a-service-request-.md">Create a service request</a></p></li>
<li><p><a href="get-service-request-support-topics--pending-.md">Get service request support topics</a></p></li>
<li><p><a href="get-all-service-requests-for-a-customer.md">Get all service requests for a customer</a></p></li>
<li><p><a href="get-service-request-details-by-id.md">Get service request details by ID</a></p></li> 
<li><p><a href="update-a-service-request.md">Update a service request</a></p></li>
</ul></td>
</tr>
<tr>
<td><p><a href="manage-profiles-and-information.md">Manage accounts and profiles</a></p></td>
<td><p>Work with accounts and profiles</p>
<ul>
<li><p><a href="get-legal-business-profile.md">Get the partner legal business profile</a></p></li>
<li><p><a href="get-an-organization-profile.md">Get an organization profile</a></p></li>
<li><p><a href="get-partner-billing-profile.md">Get partner billing profile</a></p></li>
<li><p><a href="get-partner-network-profile.md">Get Microsoft Partner Network profile</a></p></li>
<li><p><a href="get-support-profile.md">Get support profile</a></p></li>
<li><p><a href="update-legal-business-profile.md">Update the partner legal business profile</a></p></li>
<li><p><a href="update-partner-billing-profile.md">Update the partner billing profile</a></p></li>
<li><p><a href="update-support-profile.md">Update support profile</a></p></li>
<li><p><a href="update-an-organization-profile.md">Update an organization profile</a></p></li>
<li><p><a href="get-partner-by-mpn-id.md">Verify a partner MPN ID</a></p></li>
<li><p><a href="get-all-subscriptions-by-partner.md">Get a customer&#39;s subscriptions by partner MPN ID</a></p></li>
<li><p><a href="get-customers-of-an-indirect-reseller.md">Get customers of an indirect reseller</a></p></li>
<li><p><a href="get-indirect-resellers-of-a-customer.md">Get indirect resellers of a customer</a></p></li>
<li><p><a href="retrieve-a-list-of-indirect-resellers.md">Retrieve a list of indirect resellers</a></p></li>
</ul></td>
</tr>
<tr>
<td><p><a href="utilities.md">Utilities</a></p></td>
<td><ul>
<li><p><a href="validate-an-address.md">Validate an address</a></p></li>
<li><p><a href="get-market-specific-validation-data.md">Get address formatting rules by market</a></p></li>
<li><p><a href="verify-domain-availability.md">Verify domain availability</a></p></li>
<li><p><a href="delete-a-customer-account-from-the-integration-sandbox.md">Delete a customer account from the integration sandbox</a></p></li>
<li><p><a href="get-a-record-of-partner-center-activity-by-user.md">Get a record of Partner Center activity</a></p></li>
</ul></td>
</tr>
</tbody>
</table>


## <span id="background"/><span id="BACKGROUND"/>Background

### <span id="Who_is_involved_in_the_order_process_"/><span id="who_is_involved_in_the_order_process_"/><span id="WHO_IS_INVOLVED_IN_THE_ORDER_PROCESS_"/>Who is involved in the order process?

Microsoft, distributors, resellers, and customers. The distributors and resellers are often referred to as **partners**.

Sometimes, Microsoft works directly with resellers who sell to customers. Alternately, Microsoft also works with distributors, and those distributors work with their own set or channel of resellers who sell to customers.

### <span id="What_s_getting_sold_______"/><span id="what_s_getting_sold_______"/><span id="WHAT_S_GETTING_SOLD_______"/>What's getting sold?

Microsoft provides a list of **offers**. These are specific SKUs of products like Office 365 or Intune. Offers are either **license-based** (the cost depends on the number of machines they get installed on) or **usage-based** (the cost depends on the amount of memory and computation used). For more information, see [Partner offers in the Cloud Solution Provider program](https://docs.microsoft.com/partner-center/csp-offers).

CSP partners are resellers who have customers and sell them Microsoft products from the current offer list. After the customers sign their agreement, the reseller places an **order** for one or more offers. Some offers include **add-ons** like more space or extra features, which are tracked together with the parent offer. The orders are processed, and then the customer is able to use their **subscriptions**. Microsoft bills the reseller or distributor each month based on the number of licenses and the usage for each customer.

Subscriptions can be added, and the number of seats or add-ons can be increased or decreased. If a customer fails to pay, misuses the subscription, or engages in fraud, then Microsoft, the distributor, or the reseller are all able to suspend the subscription. It will be permanent if it's not reactivated within the limits of the CSP program.

You can check which subscriptions a customer is **entitled** to use (ie, which ones are currently paid for, not suspended, and not replaced by a newer order).
