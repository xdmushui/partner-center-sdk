---
title: Manage payouts using the Payout Service API
description: Learn how to use Partner Center Payout Service API to access payout data
ms.date: 06/23/2021
ms.service: partner-dashboard
ms.subservice:  partnercenter-sdk
author: jasongroce
ms.author: sabaja
---

# Manage payouts using the Payout Service API

This article explains how a partner can access their Payout data directly through the available APIs instead of Partner center.

Partners can download their payout statement by logging in to Partner Center. Additionally, they can directly access their payout statement without logging onto Partner center using the Partner payout service API. These APIs provide a programmatic way to provide the capability of the [Export data](https://partner.microsoft.com/dashboard/payouts/reports/incentiveexport) feature in Partner Center.

## Available APIs

You can view all available APIs at [Partner Payouts](https://apidocs.microsoft.com/services/partnerpayouts) section of Microsoft's Partner API Docs site. The following actions are available.

- Transaction history export actions:
  - [Post](https://apidocs.microsoft.com/services/partnerpayouts#/ExportRequests/transactionhistory) a new request
  - [Get](https://apidocs.microsoft.com/services/partnerpayouts#/ExportRequests/transactionhistoryAll) an existing request
  - [Delete](https://apidocs.microsoft.com/services/partnerpayouts#/ExportRequests/transactionhistory2) an existing request

- Payments export actions:
  - [Post](https://apidocs.microsoft.com/services/partnerpayouts#/ExportRequests/payments) a new request
  - [Get](https://apidocs.microsoft.com/services/partnerpayouts#/ExportRequests/paymentsAll) an existing request
  - [Delete](https://apidocs.microsoft.com/services/partnerpayouts#/ExportRequests/payments2) an existing request

## Prerequisites

- [Register an application with AAD/Microsoft Identity](/graph/auth-register-app-v2) in the Azure portal, and add appropriate owners and roles to the application.
- Install [Visual Studio](https://visualstudio.microsoft.com/downloads/).

## Register an application with the Microsoft identity platform

The [Microsoft identity platform](/azure/active-directory/develop/v2-overview) helps you build applications your users and customers can sign in to using their Microsoft identities or social accounts, and provide authorized access to your own APIs or Microsoft APIs like Microsoft Graph.

1. Sign in to the [Azure portal](https://portal.azure.com/) using either a work or school account or a personal Microsoft account.

   If your account gives you access to more than one tenant, select your account in the upper right corner and set your portal session to the correct Azure AD tenant.

2. In the left navigation pane, select the Azure Active Directory service, then **App registrations**, then **New registration**. The **Register an application** page appears.

   :::image type="content" source="./images/manage-payouts/new-app-registration.png" alt-text="Screenshot showing the Register an app screen in the Azure portal.":::

3. Enter your application's registration information:

   - Name: Enter a meaningful application name that will be displayed to users of the app.
   - Supported account types: Select which accounts your application will support.

    | **Supported account types**                             | **Description**                                                                                            |
    |---------------------------------------------------------|------------------------------------------------------------------------------------------------------------|
    | Only accounts in this organizational directory          | Select this option if you're building a line-of-business (LOB) application. This option is not available if you're not registering the application in a directory. This option maps to Azure AD only single-tenant.  This is the default option unless you're registering the app outside of a directory. In cases where the app is registered outside of a directory, the default is Azure AD multi-tenant and personal Microsoft accounts.             |
    | Accounts in any organizational directory                | Select this option if you would like to target all business and educational customers.  This option maps to an Azure AD only multi-tenant. If you registered the app as Azure AD only single-tenant, you can update it to be Azure AD multi-tenant and back to single-tenant through the Authentication blade.                                                                                                                                                  |
    | Accounts in any organizational directory and personal Microsoft accounts | Select this option to target the widest set of customers. This option maps to Azure AD multi-tenant and personal Microsoft accounts.  If you registered the app as Azure AD multi-tenant and personal Microsoft accounts, you cannot change this in the UI. Instead, you must use the application manifest editor to change the supported account types.                                                                          |

   - *(optional)* Redirect URI: Select the type of app you're building, Web or Public client (mobile & desktop), and then enter the redirect URI (or reply URL) for your application. (The redirect URL is where the authentication response will be sent after the user authenticates.) 

      For web applications, provide the base URL of your app. For example, `http://localhost:31544` might be the URL for a web app running on your local machine. Users would use this URL to sign in to a web client application.
      For public client applications, provide the URI used by Azure AD to return token responses. Enter a value specific to your application, such as `myapp://auth`.

4. Select **Register**. Azure AD assigns a unique application (client) ID to your application, and the application's overview page loads.

   :::image type="content" source="./images/manage-payouts/register-an-application.png" alt-text="<alt text>":::

5. If you want to add additional capabilities to your application, you can select other configuration options including branding, certificates and secrets, API permissions, and more.

## Platform-specific properties

The following table shows the properties that you need to configure and copy for different kinds of apps. **Assigned** means that you should use the value assigned
by Azure AD.

| App type              | Platform | Application (client) ID | Client Secret | Redirect URI/URL | Implicit Flow                                                         |
|-----------------------|----------|-------------------------|---------------|------------------|-----------------------------------------------------------------------|
| Native/Mobile         | Native   | Assigned                | No            | Assigned         | No                                                                    |
| Web App               | Web      | Assigned                | Yes           | Yes              | Optional Open ID Connect middleware uses hybrid flow by default (Yes) |
| Single Page App (SPA) | Web      | Assigned                | Yes           | Yes              | Yes SPAs use Open ID Connect implicit Flow                            |
| Service/Daemon        | Web      | Assigned                | Yes           | Yes              | No                                                                    |

## Create a service principal

To access resources in your subscription, you must assign a role to the application. For help deciding which role offers the right permissions for the application, see [Azure built-in roles](/azure/role-based-access-control/built-in-roles).

> [!NOTE]
> You can set the scope at the level of the subscription, resource group, or resource. Permissions are inherited to lower levels of scope. For example, adding an application to the Reader role for a resource group means it can read the resource group and any resources it contains.

1. In the Azure portal, select the level of scope to assign the application to. For example, to assign a role at the subscription scope, search for and select **Subscriptions**, or select **Subscriptions** on the home page.

:::image type="content" source="./images/manage-payouts/search-for-subscriptions.png" alt-text="Screenshot showing the Subscriptions screen search.":::

2. Select the subscription to assign the application to.

:::image type="content" source="./images/manage-payouts/internal-testing-subscription.png" alt-text="Screenshot showing the Subscriptions screen with Internal Testing flag set to true.":::

> [!NOTE]
> If you don't see the subscription you're looking for, select the global subscriptions filter and ensure the subscription you want is selected for the portal.

3. Select **Access control (IAM)**, and then select **Add role assignment**.

4. Select the role you wish to assign to the application. For example, to allow the application to execute actions like reboot, start and stop instances, select the Contributor role. Read more about [available roles](/azure/role-based-access-control/built-in-roles).

   By default, Azure AD applications aren't displayed in the available options. To find your application, search on the name and select it from the results. In the below screenshot, `example-app` is the AAD app which you registered.

:::image type="content" source="./images/manage-payouts/add-role-assignment.png" alt-text="Screenshot showing the user interface for adding a role assignment for a test application.":::

5. Select **Save**. You can then see your application in the list of users with a role for that scope.

   You can start using your service principal to run your scripts or apps. To manage your service principal's permissions, see user consent status, review permissions, see sign-in information, and more), view your Enterprise applications in the [Azure portal](https://portal.azure.com).

## Set up API permissions

This section provides instruction on how to set up the required API permissions. For additional information about setting up Partner Center API permissions, see [Partner API authentication](/partner/develop/api-authentication).

**Grant permission to Graph API**

1. Open the [App registrations](https://go.microsoft.com/fwlink/?linkid=2083908) in the Azure portal.

2. Select an application, or [create an app](/azure/active-directory/develop/quickstart-register-app) if you don't already have one.

3. On the application's Overview page, under **Manage**, select **API Permissions**, then **Add a permission**.

4. Select **Microsoft Graph** from the list of available APIs.

5. Select **Delegated permissions** and add required permissions. For more information, see [Configure app access](/azure/active-directory/develop/quickstart-configure-app-access-web-apis).

:::image type="content" source="./images/manage-payouts/graph-request-api-permissions.png" alt-text="Screenshot showing the request permissions screen in the Azure portal with Microsoft Graph selected.":::

**Consent to API access to Partner Center API via AAD app**

6. For your application, select **API permissions**, then, from the Request API permissions screen, select **Add a permission**, then **APIs my organization uses**.

7. Search for **Microsoft Partner (Microsoft Dev Center) API (4990cffe-04e8-4e8b-808a-1175604b879f)**.

:::image type="content" source="./images/manage-payouts/partner-api-request-permissions.png" alt-text="Screenshot showing the API permissions screen with Microsoft Partner selected.":::

8. Set the Delegated Permissions to **Partner Center**.

:::image type="content" source="./images/manage-payouts/partner-api-request-permissions.png" alt-text="Screenshot showing the Delegated Permissions selected for Partner Center in the Request API permissions screen.":::

9. Grant **Admin consent** for the APIs.

:::image type="content" source="./images/manage-payouts/api-permissions.png" alt-text="Screenshot showing the toggle for Admin Consent on the API permissions screen.":::

You can verify that Admin consent is enabled in the Admin consent status screen.

:::image type="content" source="./images/manage-payouts/admin-consent-verification.png" alt-text="Screenshot showing the Admin consent status screen":::

9. In the **Authentication** section, make sure the **Allow public client flows** option is set to **Yes**.

:::image type="content" source="./images/manage-payouts/allow-public-client-flows.png" alt-text="Screenshot showing the Authentication screen with Allow public client flows set to Yes.":::

## Run the sample code in Visual Studio

Sample code showing how the API can be used for payment and transaction history be found in the [Partner-Center-Payout-APIs](https://github.com/microsoft/Partner-Center-Payout-APIs) GitHub repo.

### Sample code notes

- Configuration of Client secrets and Certificates as discussed in the Authentication: Two options section of [How to create a service principal in the Azure portal](/azure/active-directory/develop/howto-create-service-principal-portal) is not required.
- Accounts with multi-factor authentication (MFA) are not currently supported and will cause an error.
- Payout API only supports user/password-based credentials.

## Next steps

- [Use the portal to create an Azure AD application and service principal that can access resources](/azure/active-directory/develop/howto-create-service-principal-portal)
- [Register an application with the Microsoft identity platform](/graph/auth-register-app-v2)
- [Configure a client application to access a web API](/azure/active-directory/develop/quickstart-configure-app-access-web-apis)
