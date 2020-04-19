---
title: Auditing resources
description: Resources used with Partner Center audit operations.
ms.assetid: FEF0BED4-2CEB-46D2-9365-D7D3C50AF0E3
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice:  partnercenter-sdk
ms.localizationpriority: medium
---

# Auditing resources

**Applies to:**

- Partner Center

You can use the following resources with audit operations.

## AuditRecord

Represents a record of an operation performed by a partner user or application.

| Property | Type | Description |
| --- | --- | ---|
| customerId | string | A GUID-formatted string that identifies the customer. |
| customerName | string | The customer name. |
| userPrincipalName | string | The user principal name or user identifier. Typically, this is an Internet-style login name for a user in an email address format based on Internet standard RFC 822. |
| applicationId | string | A string that identifies the application that performed the operation. |
| resourceType | string | The type of resource acted upon by the operation. Possible values: &quot;customer&quot;, &quot;customer_user&quot;, &quot;order&quot;, &quot;subscription&quot;, &quot;license&quot;, &quot;third_party_add_on&quot;, &quot;mpn_association&quot;, &quot;transfer&quot;, &quot;application&quot;, &quot;application_credential&quot;, &quot;partner_user&quot;, &quot;partner_relationship&quot;. |
| resourceOldValue | string | The old value of the resource. |
| resourceNewValue | string | The new value of the resource. |
| operationType | string | The type of operation performed. Possible values: &quot;update_customer_qualification&quot;, &quot;update_subscription&quot;, &quot;upgrade_subscription&quot;, &quot;convert_trial_subscription&quot;, &quot;add_customer&quot;, &quot;update_customer_billing_profile&quot;, &quot;update_customer_partner_contract_company_name&quot;, &quot;update_customer_spending_budget&quot;, &quot;delete_customer&quot; (sandbox integration accounts only), &quot;remove_partner_customer_relationship&quot;, &quot;create_order&quot;, &quot;update_order&quot;, &quot;create_customer_user&quot;, &quot;delete_customer_user&quot;, &quot;update_customer_user&quot;, &quot;update_customer_user_licenses&quot;, &quot;reset_customer_user_password&quot;, &quot;update_customer_user_principal_name&quot;, &quot;restore_customer_user&quot;, &quot;create_mpn_association&quot;, &quot;update_mpn_association&quot;, &quot;update_sfb_customer_user_licenses&quot;, &quot;update_transfer&quot;, &quot;create_partner_relationship&quot;, &quot;register_application&quot;, &quot;unregister_application&quot;, &quot;add_application_credential&quot;, &quot;remove_application_credential&quot;, &quot;create_partner_user&quot;, &quot;update_partner_user&quot;, &quot;remove_partner_user&quot;. |
| operationDate | string in UTC date-time format | The date and time when the operation was performed. |
| operationStatus | string | The status of the operation being audited. Possible values: &quot;succeeded&quot;, &quot;failed&quot;, or &quot;progress&quot;, which means the operation is still in progress. |
| customizedData  | array of objects | Additional information. Each object contains two JSON key-value pairs: the first is &quot;key&quot; and a string value, the second is &quot;value&quot; and a string value. The number of objects in the array depends on the type of operation that was performed. |
| attributes | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes. |