---
title: CSP Customer Storefront Builder Quick Start Guide
description: Create an online marketplace to sell cloud solution provider (CSP) offers by using the CSP Customer Storefront Builder.
ms.assetid: 333EE80D-E49E-4E89-87FB-3F02AC48C236
ms.date: 12/15/2017
ms.localizationpriority: medium
---

# CSP Customer Storefront Builder Quick Start Guide


**Applies To**

-   Partner Center

Create an online marketplace to sell cloud solution provider (CSP) offers by using the CSP Customer Storefront Builder.

## <span id="What_is_the_CSP_Customer_Storefront_Builder__"></span><span id="what_is_the_csp_customer_storefront_builder__"></span><span id="WHAT_IS_THE_CSP_CUSTOMER_STOREFRONT_BUILDER__"></span>What is the CSP Customer Storefront Builder?


The CSP Customer Storefront Builder helps partners easily create an online marketplace to sell CSP offers to their customers. Most partners and small sales organizations want to focus on selling rather than developing an online marketplace, and the Partner Center SDK sample app requires software development skills to create and deploy a website. With the CSP Customer Storefront Builder, you can quickly and easily create your own website. You can also download the site as sample code or deploy directly to your Azure subscription with a Ready to Transact website.

This website is fully owned, supported, and maintained by partners, and Microsoft does not collect any data or telemetry from the site. The CSP Customer Storefront Builder creates a website for the partner that is fully compliant with the [Payment Card Industry Data Security Standard](https://www.pcisecuritystandards.org/)(PCI DSS).

The CSP Customer Storefront Builder code is subject to the license available in the [Partner Center SDK EULA](https://partnercenter.microsoft.com/partner/EULA_Partner_Center_SDK).

>[!NOTE]
>You are responsible for the storefront site management, maintenance, and any issues that might result from site creation. Read and understand the terms in the [Partner Center SDK EULA](https://partnercenter.microsoft.com/partner/EULA_Partner_Center_SDK).

 

## <span id="How_can_partners_use_the_CSP_Customer_Storefront_Builder__"></span><span id="how_can_partners_use_the_csp_customer_storefront_builder__"></span><span id="HOW_CAN_PARTNERS_USE_THE_CSP_CUSTOMER_STOREFRONT_BUILDER__"></span>How can partners use the CSP Customer Storefront Builder?


CSP partner admins on Partner Center can deploy a CSP Customer Storefront directly from Partner Center. With minimal effort, a new website can be deployed on the partner's tenant. Once deployed, partners can use the website to configure branding, offers, and payment-related information, and then share the site URL address with customers.

The process for creating a website is shown in the following table.

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>1. Deploy</th>
<th>2. Configure</th>
<th>3. Transact</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li><p>Deploy your website from Partner Center</p></li>
<li><p>Integrate with Azure to deploy the configured website</p></li>
<li><p>Deploy on an existing subscription, or bring your own subscription.</p></li>
</ul></td>
<td><ul>
<li><p>Practically anyone can customize a storefront. No developer skills are needed.</p></li>
<li><p>Log in with your Partner Center admin credentials to configure:</p>
<ul>
<li>Branding - Your company name, logo, contacts, and more.</li>
<li>Offers - View all CSP offers and select the offers you want your customers to view and purchase. Personalize offer information and add your price.</li>
<li>PayPal Payment Configuration - Add your PayPal payment account information. If you do not have a PayPal account, you can go to PayPal.com and create a new account. This account will be used for PayPal to credit the payments made by customers. Microsoft is not responsible for the relationship between partners and PayPal. Use of PayPal may require the partner or partner's customers to agree to additional terms.</li>
<li>For India: PayU Payment Configuration - Add your PayU Money payment account information. If you do not have a PayU Money account, you can go to PayUmoney.com and create a new account. This account will be used for PayU to credit the payments made by customers. Microsoft is not responsible for the relationship between partners and PayU. Use of PayU may require the partner or partner's customers to agree to additional terms.</li>
</ul></li>
</ul></td>
<td><ul>
<li><p>After deployment, customers can immediately purchase and transact.</p></li>
<li><p>Customers can buy directly from the partner portal integrated with the Partner Center SDK.</p></li>
</ul></td>
</tr>
</tbody>
</table>

 

## <span id="Considerations"></span><span id="considerations"></span><span id="CONSIDERATIONS"></span>Considerations


The CSP Customer Storefront Builder is intended as a quick way to create a website. Be aware of the following considerations during your planning:

-   Once deployed, Microsoft and Partner Center does not maintain a copy of the partner website or any information added into the CSP Customer Storefront Builder.
-   Partner Center can only deploy a CSP Customer Storefront website to a partner's Azure subscriptions.
-   This site, once deployed, is fully owned and managed by the partner. Microsoft does not have access to this site, or any data related to the site. Partners are responsible for maintenance and management of the website. Microsoft will not provide any live site or other support related to the CSP Customer Storefront Builder or any website created by using the CSP Customer Storefront Builder.
-   Partner Center cannot directly access or upgrade this website with new or changed SDK or API features. Any new features or enhancements must be owned, developed, and managed by partners, including adding new Partner Center SDK or API features.
-   This CSP Customer Storefront Builder currently provides the ability to configure payment to a PayPal Pro/PayU Money (for India) account. If partners need to change the payment processor, they will need to change the code to support their preferred payment method.
-   Any payment related information added in the CSP Customer Storefront Builder is not stored or maintained in Partner Center.
-   PayPal payment configuration will work in any geographies where PayPal is available. PayPal availability and support is solely controlled by PayPal, and may be discontinued at any time by PayPal.
-   PayU payment configuration will work only in India currently. PayU availability and support is solely controlled by PayU and may be discontinued at any time by PayU.
-   Read and understand the terms in the [Partner Center SDK EULA](https://partnercenter.microsoft.com/partner/EULA_Partner_Center_SDK).

## <span id="Additional_resources"></span><span id="additional_resources"></span><span id="ADDITIONAL_RESOURCES"></span>Additional resources


To enhance or customize your CSP Customer Storefront:

-   Download the web sample from here and make additional customizations: <https://github.com/PartnerCenterSamples/Reseller-Web-Application>
-   Use Microsoft Visual Studio 2015 (or later) to develop, build for additional changes and enhancements (including authorizations, certifications, manifest changes, and other items).

## <span id="Scenario__Partner_experience"></span><span id="scenario__partner_experience"></span><span id="SCENARIO__PARTNER_EXPERIENCE"></span>Scenario: Partner experience


1.  Deploy
    -   A partner admin can use Partner Center to deploy the site. In Account settings, choose **Web storefront** to deploy a new website.
    -   On this page, partners can see the availability of a new site name and change it (if available).
    -   This page shows all active Azure subscriptions associated to this partner tenant and that a partner can choose to use to deploy the website.
    -   If a partner does not have an active subscription associated to this Partner Center account, they can add this account as an admin to an existing Azure subscription, and refresh to see that subscription in this list.
    -   Partners choose the data center location where this site will be deployed.
    -   The **Deploy your store** link will deploy this new website based on the information provided and show the URL.
    -   Be sure to copy this URL as Partner Center does not maintain the state or history of these sites. If you close the browser page, you will lose the website name.
    -   During deployment, the site will be deployed with the web app credentials created in Partner Center. If you did not register a web app, this will be registered during deployment.
2.  Configure
    -   The newly created website is linked to a partner tenant and has access to all admin accounts of this partner tenant. Partners can login to this new website using their Partner Center admin credentials.
    -   The storefront application currently supports French, Spanish, Dutch, German and Japanese along with English which serves as the fallback language. The storefront uses the partner's default locale to configure the Locale (Currencies, Date formats, Localized offers in the repository) using the Partner Profile from partner center.
    -   Partners can update branding, offers and PayPal/PayU (for India) payment information.
    -   Partners can update the company name, company logo, header image, sales and support contacts and more.
    -   Partners can see all CSP offers available based on their territory. Partners can choose which offers they want to show to all of their customers. A CSP partner can select one or more offers and update name, quantity, and feature description as well as price. The price should be the annual price. Customers subscribe annually.
    -   Partners can at any time configure pre-approved transactions for (a) all current and future customers OR (b) specific customers. Pre-approved customers are not required to pay on the portal when they add new subscriptions, purchase additional seats to existing subscriptions, or renew a subscription. Pre-approved customers will not be redirected to PayPal/PayU (for India) for payment during these transactions. Pre-approved customer transactions allow a partner to perform offline billing and invoicing to their pre-approved customers.
    -   A CSP partner can input their PayPal account information such as PayPal Client ID, secret, and also select whether they want to test using a sandbox or a live account. Partners can find this information on developer.paypal.com in **my apps & credentials**. You can get this info from a current app or create a new app in PayPal. Create a new PayPal account if you don't already have one. This account will be used for PayPal to credit the payments made by customers.

        To create a PayPal sandbox account see <https://developer.paypal.com/docs/classic/lifecycle/ug_sandbox/>.

        To open a PayPal business account, see <https://developer.paypal.com/docs/classic/lifecycle/goingLive/#register>. 
    
    -   For India: A CSP partner can input their PayU Money account information such as PayU Client ID and password. Partners can find more information on payumoney.com/dev-guide/. Create a new PayU Money account if you don't already have one. This account will be used for PayU to credit the payments made by customers.

        To open a PayU Money account, go to <https://www.payumoney.com/merchant-account/#/>. 

## <span id="Scenario__Customer_experience"></span><span id="scenario__customer_experience"></span><span id="SCENARIO__CUSTOMER_EXPERIENCE"></span>Scenario: Customer experience


1.  New customer sign up and purchase
    -   By default, the site is publicly available and shows the partner's catalog on the homepage.
    -   Customers can now belong to a large number of countries (listed [here](#countries)). The focus has been on the European Free Trade Association (EFTA) countries, North America, Japan, India, Australia, and New Zealand regions. This feature uses the Regional authorization support in the Partner Center SDK.
    -   Customers can select an offer from the catalog to purchase They can add their customer name, address, and domain related information.
    -   Customers will be directed to the PayPal/PayU (for India) checkout experience to provide payment either using their existing PayPal/PayU (for India) account or using funding instruments supported in that country by PayPal/PayU (for India) (including credit cards, debit cards and bank accounts as may apply).
    -   This creates a customer tenant for this customer. After successful creation of the tenant order, customers are provided the account username, password and subscription details.
    -   Customers can save the username and password to login for further purchases.
    -   Each subscription is purchased for a year and customers can renew in the 30 days prior to the subscription end date.
2.  Sign in experience to view prior purchases
    -   Customer signs in with Customer tenant username and password and goes to the **My Orders** section.
    -   Customers can navigate to the **My Orders** page where they can view purchased subscriptions and make updates if required.
    -   Customers can navigate to the **My Subscriptions** page where they can view all subscriptions (license based as well as usage based), including those maintained in Partner Center.
3.  Add more seats to existing subscriptions
    -   From the **My Orders** section, customers can add more seats to existing subscriptions. Customers can add more seats anytime during a subscription year.
    -   Each added seat does not change the end date of the subscription. However, the price of the subscription changes based on the date on which you add the seat, and where that date is in the year. Pricing is prorated on a daily basis to only charge for the remaining days of the year.
4.  Add more subscriptions
    -   Customers can buy any number of subscriptions at any time from **My Orders**, **Add subscriptions** section.
    -   A customer can select a subscription, add a quantity, and pay to complete the transaction and start using the subscription immediately. If a customer is a pre-approved customer, the subscription is available for use immediately and an invoice will be sent to the customer for payment.
5.  Renew
    -   A customer can renew a subscription during the last 30 days prior to the subscription end date.
    -   This is available only in the last 30 days.
    -   If not renewed in last 30 days, the subscription will be removed from the list of subscriptions for this Customer tenant.
    -   You cannot update the quantity during renewal.
6.  Payments
    -   If the customer is pre-approved for transactions by the admin, the payment experience is not presented for the above scenarios. Instead, the partner can send the invoice for payment to the pre-approved customer.
    -   For all new purchases, you can add more seats, add subscriptions and renew. A customer can pay a partner using this website (through PayPal/PayU (for India)).
    -   This website is integrated with PayPal/PayU (for India) and allows partners to accept payments from their customers. PayPal/PayU (for India) credits this amount in a partner's account. PayPal/PayU (for India) Bank account management is outside of this site and is managed on PayPal.com or PayUmoney.com respectively.
    -   This is dependent on partners configuring their PayPal/PayU (for India) Payment configuration at PayPal.com or PayUmoney.com. Microsoft does not save this information or actual payment transactions resulting from the use of this option.
7.  Prorated pricing
    -   This site supports prorated pricing in cases when customers add more seats to an existing subscription.
    -   Each subscription expires after one year and cannot be changed after the subscription is purchased.
    -   The end date of the subscription will not change by adding additional seats. Customers will be charged for the remaining number of days until the end date. For example, if on day one the subscription cost is $365, and you add one more seat on day two, the price for new seat will be $364. If you add one more 10 days later, the price will be $354.

## <span id="Countries"></span><span id="countries"></span><span id="COUNTRIES"></span>Customers can belong to these countries:


| Country Code | Country Name   |
|--------------|----------------|
| AU           | Australia      |
| AT           | Austria        |
| BE           | Belgium        |
| BG           | Bulgaria       |
| CA           | Canada         |
| HR           | Croatia        |
| CY           | Cyprus         |
| CZ           | Czech Republic |
| DK           | Denmark        |
| EE           | Estonia        |
| FI           | Finland        |
| FR           | France         |
| DE           | Germany        |
| GR           | Greece         |
| HU           | Hungary        |
| IS           | Iceland        |
| IN           | India          |
| IE           | Ireland        |
| IT           | Italy          |
| JP           | Japan          |
| LV           | Latvia         |
| LI           | Liechtenstein  |
| LT           | Lithuania      |
| LU           | Luxembourg     |
| MT           | Malta          |
| MC           | Monaco         |
| NL           | Netherlands    |
| NZ           | New Zealand    |
| NO           | Norway         |
| PO           | Poland         |
| PT           | Portugal       |
| RO           | Romania        |
| SK           | Slovakia       |
| SL           | Slovenia       |
| ES           | Spain          |
| SE           | Sweden         |
| CH           | Switzerland    |
| GB           | United Kingdom |
| US           | United States  |

 

## <span id="See_Also"></span><span id="see_also"></span><span id="SEE_ALSO"></span>See Also


[CSP customer web storefront](csp-customer-web-storefront.md)


[Console test app](console-test-app.md)


 

 




