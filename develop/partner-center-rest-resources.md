---
title: Partner Center REST resources
description: 
    This section provides definitions for the JSON elements needed to create
    requests and parse responses using the Partner Center REST API.
ms.assetid: E7C51D19-C6A7-4A4C-9F17-B4D39195972A
ms.author: v-thpr
ms.date: 12/15/2017
ms.topic: article
ms.prod: partner-center
ms.technology: partner-center-sdk
---

# Partner Center REST resources


<span class="sidebar_heading" style="font-weight: bold;">Applies
To</span>

-   Partner Center
-   Partner Center operated by 21Vianet
-   Partner Center for Microsoft Cloud Germany
-   Partner Center for Microsoft Cloud for US Government

This section provides definitions for the JSON elements needed to create
requests and parse responses using the Partner Center REST API. For more
information about how to use these elements, including sample code, see
the [Scenarios](scenarios.md) section and the [Partner Center
samples](partner-center-samples.md) section.

## <span id="In_this_section"></span><span id="in_this_section"></span><span id="IN_THIS_SECTION"></span>In this section


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td>[Analytics](analytics.md)</td>
<td><ul>
<li>PartnerLicensesDeploymentInsights</li>
<li>PartnerLicensesUsageInsights</li>
<li>CustomerLicensesDeploymentInsights</li>
<li>PartnerLicensesUsageInsights</li>
</ul></td>
</tr>
<tr class="even">
<td>[Auditing](auditing.md)</td>
<td><ul>
<li>AuditRecord</li>
</ul></td>
</tr>
<tr class="odd">
<td>[Azure Rate Card](azure-rate-card.md)</td>
<td><ul>
<li>AzureRateCard</li>
<li>AzureMeter</li>
<li>AzureOfferTerm</li>
</ul></td>
</tr>
<tr class="even">
<td>[Azure Utilization Record](azure-utilization-record.md)</td>
<td><ul>
<li>AzureUtilizationRecord</li>
<li>AzureResource</li>
<li>AzureInstanceData</li>
</ul></td>
</tr>
<tr class="odd">
<td>[Conversions](conversions.md)</td>
<td><ul>
<li>Conversion</li>
<li>ConversionError</li>
<li>ConversionResult</li>
</ul></td>
</tr>
<tr class="even">
<td>[CountryInformation](countryinformation.md)</td>
<td><ul>
<li>CountryInformation</li>
<li>CountryValidationRules</li>
</ul></td>
</tr>
<tr class="odd">
<td>[Customer](customers.md)</td>
<td><ul>
<li>Customer</li>
<li>CustomerCompanyProfile</li>
<li>CustomerBillingProfile</li>
<li>CustomerRelationshipRequest</li>
</ul></td>
</tr>
<tr class="even">
<td>[Customer Usage Budgeting](customer-usage.md)</td>
<td><ul>
<li>CustomerMonthlyUsageRecord</li>
<li>CustomerUsageSummary</li>
<li>PartnerUsageSummary</li>
<li>SpendingBudget</li>
</ul></td>
</tr>
<tr class="odd">
<td>[Invoice](invoice.md)</td>
<td><ul>
<li>Invoice</li>
<li>InvoiceDetail</li>
<li>InvoiceLineItem</li>
<li>InvoiceSummary</li>
</ul></td>
</tr>
<tr class="even">
<td>[License](licenses.md)</td>
<td><ul>
<li>License</li>
<li>LicenseUpdate</li>
<li>LicenseAssignment</li>
<li>LicenseWarning</li>
<li>ProductSku</li>
<li>ServicePlan</li>
<li>SubscribedSku</li>
</ul></td>
</tr>
<tr class="odd">
<td>[ManagedService](managedservice.md)</td>
<td><ul>
<li>ManagedService</li>
<li>ManagedServiceLinks</li>
</ul></td>
</tr>
<tr class="even">
<td>[Offer](offer.md)</td>
<td><ul>
<li>Offer</li>
<li>OfferCategory</li>
<li>OfferLinks</li>
<li>OfferProduct</li>
</ul></td>
</tr>
<tr class="odd">
<td>[Order](orders.md)</td>
<td><ul>
<li>Order</li>
<li>OrderLineItem</li>
<li>OrderLineItemLinks</li>
</ul></td>
</tr>
<tr class="even">
<td>[Profile](profiles.md)</td>
<td><ul>
<li>BillingProfile</li>
<li>LegalBusinessProfile</li>
<li>MpnProfile</li>
<li>OrganizationProfile</li>
<li>SupportProfile</li>
</ul></td>
</tr>
<tr class="odd">
<td>[Product](product.md)</td>
<td><ul>
<li>Product</li>
</ul></td>
</tr>
<tr class="even">
<td>[Relationships](relationships.md)</td>
<td><ul>
<li>PartnerRelationship</li>
<li>RelationshipRequest</li>
</ul></td>
</tr>
<tr class="odd">
<td>[ServiceCosts](servicecosts.md)</td>
<td><ul>
<li>ServiceCostsSummary</li>
<li>ServiceCostsLineItem</li>
<li>ServiceCostsSummaryLinks</li>
</ul></td>
</tr>
<tr class="even">
<td>[ServiceRequest](servicerequest.md)</td>
<td><ul>
<li>ServiceRequest</li>
<li>ServiceRequestContact</li>
<li>ServiceRequestNote</li>
<li>ServiceRequestOrganization</li>
<li>SupportTopic</li>
</ul></td>
</tr>
<tr class="odd">
<td>[Subscription](subscriptions.md)</td>
<td><ul>
<li>Subscription</li>
<li>SubscriptionLinks</li>
<li>SubscriptionProvisioningStatus</li>
<li>SupportContact</li>
</ul></td>
</tr>
<tr class="even">
<td>[Subscription Usage](subscriptionusage.md)</td>
<td><ul>
<li>SubscriptionDailyUsageRecord <em>(Obsolete)</em></li>
<li>SubscriptionMonthlyUsageRecord</li>
<li>SubscriptionUsageSummary</li>
</ul></td>
</tr>
<tr class="odd">
<td>[Upgrade](upgrade.md)</td>
<td><ul>
<li>Upgrade</li>
<li>UpgradeError</li>
<li>UpgradeResult</li>
<li>UserLicenseError</li>
</ul></td>
</tr>
<tr class="even">
<td>[User](user.md)</td>
<td><ul>
<li>User</li>
<li>CustomerUser</li>
<li>UserCredentials</li>
<li>UserMember</li>
</ul></td>
</tr>
<tr class="odd">
<td>[Utility Resources](utility-resources.md)</td>
<td><ul>
<li>Address</li>
<li>Contact</li>
<li>FieldFilter</li>
<li>FileInfo</li>
<li>Link</li>
<li>PasswordProfile</li>
<li>ResourceLinks</li>
<li>ResourceAttributes</li>
<li>SecureString</li>
</ul></td>
</tr>
</tbody>
</table>

 

 

 




