---
title: Set up API access in Partner Center
description: This topic describes the accounts you need to develop against the Partner Center SDK, how to create an integration sandbox account, and how to test in the integration sandbox.
MSHAttr:
- 'PreferredSiteName:MSDN'
- 'PreferredLib:/library/PartnerCenter'
ms.assetid: 182A6831-6F00-4762-9A86-327BF87EA6AC
---

# Set up API access in Partner Center


**Applies To**

-   Partner Center
-   Partner Center operated by 21Vianet
-   Partner Center for Microsoft Cloud for US Government
-   Partner Center for Microsoft Cloud Germany

This topic describes the accounts you need to develop against the Partner Center SDK, how to create an integration sandbox account, and how to test in the integration sandbox.

## <span id="supportedAccountTypes"></span><span id="supportedaccounttypes"></span><span id="SUPPORTEDACCOUNTTYPES"></span>Account definitions


To help you integrate and test your API integration, Partner Center supports two kinds of accounts:

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><strong>Primary Partner Center account</strong></td>
<td><p>This account is where you create real orders for real customers. If you make any changes or transactions when you are signed in to the primary account, by using either the Partner Center SDK or the Partner Center UI, they will be treated as official orders for real customers. They will be reflected in your invoice, and your company is responsible for paying for them.</p></td>
</tr>
<tr class="even">
<td><strong>Integration sandbox account</strong></td>
<td><p>This account is for testing your code and its integration with the Partner Center APIs before you deploy it broadly. Changes and transactions you make when you are signed into the integration sandbox account will not appear in your invoice.</p>
<ul>
<li><p>The integration sandbox account and the primary account act independently, and do not share admin accounts, user accounts, customers, orders, subscriptions, or other data.</p></li>
<li><p>The integration sandbox supports transactions with a limited number of customers, orders, subscriptions, seats, etc.</p></li>
<li><p>By policy, integration sandbox accounts are for integration testing purposes only.</p></li>
<li><p>By default, there is no integration sandbox account. You must create one yourself if you plan to use the Partner Center SDK.</p></li>
</ul></td>
</tr>
</tbody>
</table>

 

## <span id="Set__up_your_accounts"></span><span id="set__up_your_accounts"></span><span id="SET__UP_YOUR_ACCOUNTS"></span>Set up your accounts


<span id="createIntegrationSandbox"></span><span id="createintegrationsandbox"></span><span id="CREATEINTEGRATIONSANDBOX"></span>
**Create an integration sandbox**

1.  Sign in into Partner Center with a global admin account. (This is your primary Partner Center account.)
2.  From the **Dashboard** menu, select **Account settings**, then **Integration sandbox**.

    **Note**  If you don't see an Integration sandbox option, you might not have a global admin account, or the integration sandbox has already been set up and you're using an integration sandbox account.

     

3.  Fill in the contact information for the integration sandbox admin account, and then click **Set up account**. You might need to wait a few minutes for the account to be created.

4.  After you see the confirmation message, sign out of Partner Center, then sign back in with your new integration sandbox admin account, in the form *username*@*domain* and with the password you just specified.

5.  After you sign back in with your new integration sandbox admin account, above **Current Tasks**, click **Set Up Account** to complete the sandbox account setup.

<span id="enableAPIAccess"></span><span id="enableapiaccess"></span><span id="ENABLEAPIACCESS"></span>
After your account is set up, you must enable API access before you can use the Partner Center SDK with the integration sandbox. You need to enable access to the API separately for both your primary Partner Center account and your integration sandbox account.

**Enable API access**

1.  Sign into Partner Center using a global admin account.

2.  From the **Dashboard** menu, select **Account settings**, then **App management**.

3.  Select an existing app or create a new app with default settings. Existing apps show up only if the Azure AD account has existing apps.

4.  On the confirmation page, copy the app registration information, especially the **Key** if you're creating a Web App, and store it in a safe place.

5.  Sign out of Partner Center, then sign back in with your integration sandbox account. Repeat steps 2-4 to enable API access in the integration sandbox.

## <span id="writeTestCode"></span><span id="writetestcode"></span><span id="WRITETESTCODE"></span>Write and test code in the integration sandbox


To write code and test code in Partner Center, you'll need to set up authentication with Azure AD, as described in [Partner Center authentication](partner-center-authentication.md). You'll need the following pieces of information:

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Item name</strong></p></td>
<td><p><strong>Where to find it</strong></p></td>
</tr>
<tr class="even">
<td><p>App ID / Client ID</p></td>
<td><p>From the <strong>Dashboard</strong> menu, select <strong>Account settings</strong>, then <strong>App Management</strong> The App ID/Client ID is listed as the Registered application <strong>App ID</strong>.</p></td>
</tr>
<tr class="odd">
<td><p>Key</p></td>
<td><p>If you created a web app, this is the key that you saved in Step 4 of &quot;Enable API access&quot;.</p></td>
</tr>
<tr class="even">
<td><p>Domain</p></td>
<td><p>This is the domain for the integration sandbox.</p></td>
</tr>
</tbody>
</table>

 

## <span id="runTestedCode"></span><span id="runtestedcode"></span><span id="RUNTESTEDCODE"></span>Use your solution for real customer data


**Change credentials from integration sandbox to primary account**

1.  When you are ready to use your tested code in your primary Partner Center account, you must get an Azure AD security token based on your Partner Center app/key/domain instead of the integration sandbox app/key/domain.

    Repeat the same steps for [Partner Center authentication](partner-center-authentication.md) that you used to get an Azure AD security token in the integration sandbox, but use your primary Partner Center credentials instead.

2.  After you replace the integration security token with the one for your primary Partner Center account, the rest of your code should work correctly.

 

 




