---
title: Auditing
description: The resources detailed here are used with audit operations.
ms.assetid: FEF0BED4-2CEB-46D2-9365-D7D3C50AF0E3
ms.author: v-thpr
ms.date: 12/15/2017
ms.topic: article
ms.prod: partner-center
ms.technology: partner-center-sdk
---

# Auditing


<span class="sidebar_heading" style="font-weight: bold;">Applies
To</span>

-   Partner Center

The resources detailed here are used with audit operations.

## <span id="AuditRecord"></span><span id="auditrecord"></span><span id="AUDITRECORD"></span>AuditRecord


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
<td>The type of resource acted upon by the operation. Possible values: &quot;customer&quot;, &quot;customer_user&quot;, &quot;order&quot;, &quot;subscription&quot;, &quot;license&quot;, or &quot;third_party_add_on.&quot;</td>
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
<li>&quot;add_customer&quot;</li>
<li>&quot;update_customer_billing_profile&quot;</li>
<li>&quot;update_customer_spending_budget&quot;</li>
<li>&quot;delete_customer&quot; (sandbox integration accounts only)</li>
<li>&quot;create_order&quot;</li>
<li>&quot;update_order&quot;</li>
<li>&quot;create_customer_user&quot;</li>
<li>&quot;delete_customer_user&quot;</li>
<li>&quot;update_customer_user&quot;</li>
<li>&quot;update_customer_user_licenses&quot;</li>
<li>&quot;reset_customer_user_password&quot;</li>
<li>&quot;update_customer_user_principal_name&quot;</li>
<li>&quot;restore_customer_user&quot;</li>
</ul></td>
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
<td>[ResourceAttributes](utility-resources.md#resourceattributes)</td>
<td>The metadata attributes.</td>
</tr>
</tbody>
</table>

 

 

 




