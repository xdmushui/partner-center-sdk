---
title: Auditing resources
description: The resources detailed here are used with audit operations.
ms.assetid: FEF0BED4-2CEB-46D2-9365-D7D3C50AF0E3
ms.date: 08/06/2018
ms.localizationpriority: medium
---

# Auditing resources


**Applies To**

- Partner Center

The resources detailed here are used with audit operations.

## <span id="AuditRecord"/><span id="auditrecord"/><span id="AUDITRECORD"/>AuditRecord


Represents a record of an operation performed by a partner user or
application.

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Property</th>
<th>Type</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>customerId</td>
<td>string</td>
<td>A GUID-formatted string that identifies the customer.</td>
</tr>
<tr class="even">
<td>customerName</td>
<td>string</td>
<td>The customer name.</td>
</tr>
<tr class="odd">
<td>userPrincipalName</td>
<td>string</td>
<td>The user principal name or user identifier. Typically, this is an Internet-style login name for a user in an email address format based on Internet standard RFC 822.</td>
</tr>
<tr class="even">
<td>applicationId</td>
<td>string</td>
<td>A string that identifies the application that performed the operation.</td>
</tr>
<tr class="odd">
<td>resourceType</td>
<td>string</td>
<td>The type of resource acted upon by the operation. Possible values: 
<ul>
<li>&quot;customer&quot;</li>
<li>&quot;customer_user&quot;</li>
<li>&quot;order&quot;</li>
<li>&quot;subscription&quot;</li>
<li>&quot;license&quot;</li>
<li>&quot;third_party_add_on&quot;</li>
<li>&quot;mpn_association&quot;</li>
<li>&quot;transfer&quot;</li>
<li>&quot;application&quot;</li>
<li>&quot;application_credential&quot;</li>
<li>&quot;partner_user&quot;</li>
<li>&quot;partner_relationship&quot;</li>
</ul>
</td>
</tr>
<tr class="even">
<td>resourceOldValue</td>
<td>string</td>
<td>The old value of the resource.</td>
</tr>
<tr class="odd">
<td>resourceNewValue</td>
<td>string</td>
<td>The new value of the resource.</td>
</tr>
<tr class="even">
<td>operationType</td>
<td>string</td>
<td>The type of operation performed. Possible values:
<ul>
<li>&quot;update_customer_qualification&quot;</li>
<li>&quot;update_subscription&quot;</li>
<li>&quot;upgrade_subscription&quot;</li>
<li>&quot;convert_trial_subscription&quot;</li>
<li>&quot;add_customer&quot;</li>
<li>&quot;update_customer_billing_profile&quot;</li>
<li>&quot;update_customer_partner_contract_company_name&quot;</li>
<li>&quot;update_customer_spending_budget&quot;</li>
<li>&quot;delete_customer&quot; (sandbox integration accounts only)</li>
<li>&quot;remove_partner_customer_relationship&quot;</li>
<li>&quot;create_order&quot;</li>
<li>&quot;update_order&quot;</li>
<li>&quot;create_customer_user&quot;</li>
<li>&quot;delete_customer_user&quot;</li>
<li>&quot;update_customer_user&quot;</li>
<li>&quot;update_customer_user_licenses&quot;</li>
<li>&quot;reset_customer_user_password&quot;</li>
<li>&quot;update_customer_user_principal_name&quot;</li>
<li>&quot;restore_customer_user&quot;</li>
<li>&quot;create_mpn_association&quot;</li>
<li>&quot;update_mpn_association&quot;</li>
<li>&quot;update_sfb_customer_user_licenses&quot;</li>
<li>&quot;update_transfer&quot;</li>
<li>&quot;create_partner_relationship&quot;</li>
<li>&quot;register_application&quot;</li>
<li>&quot;unregister_pplication&quot;</li>
<li>&quot;add_application_credential&quot;</li>
<li>&quot;remove_application_credential&quot;</li>
<li>&quot;create_partner_user&quot;</li>
<li>&quot;update_partner_user&quot;</li>
<li>&quot;remove_partner_user&quot;</li>
</ul>
</td>
</tr>
<tr class="odd">
<td>operationDate</td>
<td>string in UTC date-time format</td>
<td>The date and time when the operation was performed.</td>
</tr>
<tr class="even">
<td>operationStatus</td>
<td>string</td>
<td>The status of the operation being audited. Possible values: &quot;succeeded&quot;, &quot;failed&quot;, or &quot;progress&quot;, which means the operation is still in progress.</td>
</tr>
<tr class="odd">
<td>customizedData</td>
<td>array of objects</td>
<td>Additional information. Each object contains two JSON key-value pairs: the first is &quot;key&quot; and a string value, the second is &quot;value&quot; and a string value. The number of objects in the array depends on the type of operation that was performed.</td>
</tr>
<tr class="even">
<td>attributes</td>
<td><a href="utilityauditing-resources.md.md#resourceattributes">ResourceAttributes</a></td>
<td>The metadata attributes.</td>
</tr>
</tbody>
</table>

 

 

 




