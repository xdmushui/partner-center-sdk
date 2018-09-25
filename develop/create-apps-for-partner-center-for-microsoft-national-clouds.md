---
title: Register app details for Partner Center for Microsoft National Cloud
description: Developers must register details about their application with Azure AD through the Azure portal. This helps ensure that only specified apps are able to connect to partner and customer data.
MS-HAID:
- 'pc\_apiv2.create\_apps\_for\_partner\_center\_for\_microsoft\_cloud\_germany'
- 'pc\_apiv2.create\_apps\_for\_partner\_center\_for\_microsoft\_national\_clouds'
ms.assetid: 73C5926A-0DEB-42E5-8982-7E44A2031F0B
ms.date: 12/15/2017
ms.localizationpriority: medium
---

# Register app details for Partner Center for Microsoft National Cloud


**Applies To**

-   Partner Center for Microsoft Cloud Germany
-   Partner Center for Microsoft Cloud for US Government

Developers must register details about their application with Azure AD through the Azure portal. This helps ensure that only specified apps are able to connect to partner and customer data.

>[!NOTE]
>For Partner Center for Microsoft Cloud for US Government, you currently must manage applications through PowerShell. For more information, see the [Azure PowerShell reference documentation](https://docs.microsoft.com/powershell/module/Azuread/?view=azureadps-2.0#applications).

 

Be aware of the following additional requirements when you create an app for Partner Center for Microsoft Cloud Germany or Partner Center for Microsoft Cloud for US Government.

## <span id="Web_apps"></span><span id="web_apps"></span><span id="WEB_APPS"></span>Web apps


For web applications, use the following procedure to register your app ID.

**Create or update your web app**

1.  Go to App registrations in the Active directory section of the Azure portal.
2.  Create or update your Web application as explained in [Integrating applications with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-app-registration).

**Configure API access permissions**

1.  Click on your application. Go to **Settings** of the Web application.
2.  In **API Access** section, click on **Required permissions**
3.  For Windows Azure Active directory permissions:
    1.  Click on **Windows Azure Active Directory permissions**
    2.  In **Applications permissions**, select Read directory data
    3.  Save the permissions
4.  Note the application ID in the **Properties** section of your web application

**Add a secret key to your app**

1.  Go to the **Keys** section of your web application
2.  Enter key description and select duration as 1 or 2 years, as you need
3.  Save and copy the secret key value         
    **Note** This value will not be shown again once you leave this page.

     

You should have the following details from the web app configuration:

-   Application ID
-   Application secret

**Register the Web app in Partner center**

1.  Log in to <https://partnercenter.microsoft.com>
2.  Go to **Dashboard** &gt; **Account Settings** &gt; **App Management**
3.  In the **Web App** section, click on **Register existing app**
4.  Select the web application you created in Azure management portal
5.  Click on **register your app**

## <span id="Native_applications_"></span><span id="native_applications_"></span><span id="NATIVE_APPLICATIONS_"></span>Native applications


Native applications do not need to be registered to partner center. But these applications need to be configured to provide access to Partner center APIs.

>[!NOTE]
>Before creating native application in the Azure management portal, log in into partner center using the admin user credentials from the partner tenant. This creates the settings on the tenant to enable application permissions.

 

**Create Native application**

1.  Go to **App registrations** in the Active directory section of the Azure portal
2.  Create or update your Web application as explained in [Integrating applications with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-app-registration)

**Configure API access permissions**

1.  Click on your application. Go to **Settings**
2.  In API Access, click **Required permissions**
3.  Click on **Windows Azure Active Directory permissions**. In **Delegated permissions**, select these permissions:
    -   Sign in and read user profile
    -   Read directory data
    -   Access the directory as the signed-in user
    -   Read all groups
4.  Save the permissions
5.  Click on **Add** in **Required permissions**
6.  Click on **Select an API**
    1.  In the search box, type **Microsoft Partner Center** and select it from the results list
    2.  Click **Select**
7.  Click on **Select permissions**
    1.  Select **Access Partner Center PPE**
    2.  Click **Select**
8.  Click **Done**

Note the application ID in the Properties of your app.

You do not need to register native apps in Partner Center, however the native app must be admin consented . Note the application ID of your native app.

 

 




