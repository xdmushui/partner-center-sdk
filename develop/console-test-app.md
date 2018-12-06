---
title: Console test app
description: This console test app provides sample codes for all of the scenarios supported by the Partner Center APIs. You can also use it for testing.
ms.assetid: 56F5B4C6-CE87-4D13-9D8C-09F38E946292
ms.date: 09/30/2018
ms.localizationpriority: medium
---

# Console test app

**Applies To**

- Partner Center
- Partner Center operated by 21Vianet
- Partner Center for Microsoft Cloud Germany
- Partner Center for Microsoft Cloud for US Government

The console test app is provided in C# and Java, it provides sample codes for all of the scenarios supported by the Partner Center APIs. You can also use it for testing.

## <span id="Get_the_code"/><span id="get_the_code"/><span id="GET_THE_CODE"/>Get the code

### .NET

[Download the sample code](http://go.microsoft.com/fwlink/p/?LinkId=746682)

Before you build the application, update the values in the *App.config* file to reflect the Azure AD authentication information you created in [Partner Center authentication](partner-center-authentication.md). Specifically, you should use your integration sandbox account settings during early development or for testing in production.

Under **ScenarioSettings** in the App.config file, you can set parameters that will be automatically passed into the scenarios that you run.

To modify the list of scenarios that are run, comment out lines in **IPartnerScenario\[\] mainScenarios** or in an individual **Get Scenarios** method found in the *Program.cs* file.

### Java

[Download the sample code](http://go.microsoft.com/fwlink/p/?LinkId=2026887)

Before you build the application, update the values in the *SamplesConfigurations.json* file to reflect the Azure AD authentication information you created in [Partner Center authentication](partner-center-authentication.md). Specifically, you should use your integration sandbox account settings during early development or for testing in production.

Under **ScenarioSettings** in the *SamplesConfiguration.json* file, you can set parameters that will be automatically passed into the scenarios that you run.

To modify the list of scenarios that are run, comment out lines in **IPartnerScenario\[\] mainScenarios** or in an individual **Get Scenarios** method found in the *Program.java* file.

## <span id="What_to_change"/><span id="what_to_change"/><span id="WHAT_TO_CHANGE"/>What to change

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Setting category</th>
<th>Settings to change</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>PartnerServiceSettings</p></td>
<td><p>Do not change:</p>
<ul>
<li><strong>PartnerServiceApiEndpoint</strong></li>
<li><strong>AuthenticationAuthorityEndpoint</strong></li>
<li><strong>GraphEndpoint</strong></li>
<li><strong>CommonDomain</strong></li>
</ul>
All of these settings are necessary for the sample API calls to properly function.</td>
</tr>
<tr class="even">
<td><p>UserAuthentication</p></td>
<td><p>Required to change:</p>
<ul>
<li><strong>ApplicationId</strong>: Your Azure Active Directory application ID, used for login.</li>
<li><strong>UserName</strong>: Your active directory user name.</li>
<li><strong>Password</strong>: Your active directory password.</li>
</ul>
<p>Do not change:</p>
<ul>
<li><strong>ResourceUrl</strong></li>
<li><strong>RedirectUrl</strong></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>AppAuthentication</p></td>
<td><p>Required to change:</p>
<ul>
<li><strong>ApplicationId</strong>: Your active directory application ID, used for application login.</li>
<li><strong>ApplicationSecret</strong>: Your active directory application secret, used for application login.</li>
<li><strong>Domain</strong>: Your active directory domain on which the application is hosted.</li>
</ul></td>
</tr>
<tr class="even">
<td><p>ScenarioSettings</p></td>
<td><p>Do not change:</p>
<ul>
<li><strong>CustomerDomainSuffix</strong>: The domain suffix used when creating a new customer.</li>
</ul>
<p>Optional. If left blank, information will need to be inputted when running a scenario where it is necessary:</p>
<ul>
<li><strong>CustomerIdToDelete</strong>: The ID of the customer used for deletion.</li>
<li><strong>DefaultCustomerId</strong>: The customer ID to use in customer-related scenarios.</li>
<li><strong>DefaultInvoiceID</strong>: The invoice ID to use in invoice scenarios.</li>
<li><strong>PartnerMpnId</strong>: The partner MPN ID to use in indirect partner scenarios.</li>
<li><strong>DefaultServiceRequestId</strong>: The service request ID to use in service request scenarios.</li>
<li><strong>DefaultSupportTopicID</strong>: The support topic ID to use in service request scenarios.</li>
<li><strong>DefaultOfferID</strong>: The offer ID to use in offer scenarios.</li>
<li><strong>DefaultOrderID</strong>: The order ID to use in order scenarios.</li>
<li><strong>DefaultSubscriptionID</strong>: The subscription ID to use in subscription scenarios.</li>
</ul>
<p>Optional to change:</p>
<ul>
<li><strong>CustomerPageSize</strong></li>
<li><strong>InvoicePageSize</strong></li>
<li><strong>ServiceRequestPageSize</strong></li>
<li><strong>DefaultOfferPageSize</strong></li>
<li><strong>SubscriptionPageSize</strong></li>
</ul>
All of these settings specify the amount of entries per page when retrieving paged content.</td>
</tr>
</tbody>
</table>