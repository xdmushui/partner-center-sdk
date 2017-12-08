---
title: Developing for Partner Center for Microsoft National Cloud
MS-HAID:
- 'pc\_apiv2.developing\_with\_different\_partner\_center\_versions'
- 'pc\_apiv2.developing\_for\_partner\_center\_for\_microsoft\_national\_cloud'
ms.assetid: 13D45776-4837-48F5-AB8B-605FD1D3D52D
description: 
ms.author: v-thpr
ms.date: 12/15/2017
ms.topic: article
ms.prod: partner-center
ms.technology: partner-center-sdk
---

# Developing for Partner Center for Microsoft National Cloud


**Applies To**

-   Partner Center operated by 21Vianet
-   Partner Center for Microsoft Cloud Germany
-   Partner Center for Microsoft Cloud for US Government

Partner Center has one set of SDK documentation. However, some functionality might not be available in the versions of Partner Center for Microsoft National Clouds. Developers need to consider the following changes to the SDK for these versions of Partner Center:

-   [Partner Center operated by 21Vianet](#partner-center-operated-by-21vianet)
-   [Partner Center for Microsoft Cloud Germany](#partner-center-cloud-germany)
-   [Partner Center for Microsoft Cloud for US Government](#partner-center-msftcloudus)

Each overview topic contains an **Applies To** block at the top that describes which versions of Partner Center the topic applies to. Similarly, each managed reference topic contains the version information in the **Requirements** block at the bottom.

## <span id="partner_center_operated_by_21vianet"></span><span id="PARTNER_CENTER_OPERATED_BY_21VIANET"></span>Partner Center operated by 21Vianet


The following list describes the differences for partners between Partner Center and Partner Center operated by 21Vianet:

-   You cannot programmatically reset a password for a customer user or full partner user.
-   Subscriptions to Azure are not available.
-   You cannot manage the licenses for your customer's user. Instead, your customers must use the Office365 admin center to manage their licenses.
-   All support requests are managed through Partner Center operated by 21Vianet. Service requests and service updates do not apply.

## <span id="partner_center_cloud_germany"></span><span id="PARTNER_CENTER_CLOUD_GERMANY"></span>Partner Center for Microsoft Cloud Germany


The following list describes the differences for partners between Partner Center and Partner Center for Microsoft Cloud Germany:

-   Partners cannot create users for their customer's organization or assign roles. Partners can read fields, but cannot write or update them. Partners must manually create or update their customers' users in the Office365 admin center or through the Azure portal. See [Azure Active Directory Documentation](https://docs.microsoft.com/en-us/azure/active-directory/).
-   You cannot manage the licenses for your customer's users using thePartner Center for Microsoft Cloud Germany portal or APIs. Instead, you must use the Office365 admin center or Azure Active Directly Group license management (coming soon) to manage their licenses.

    Optionally, you can use Azure AD Graph API. See [Add or Remove Licenses from a user](https://msdn.microsoft.com/en-us/library/azure/ad/graph/api/functions-and-actions#assignLicense ). Note that for Partner Center for Microsoft Cloud Germany, the Graph endpoint should be https://graph.cloudapi.de instead of https://graph.windows.net.

-   You cannot programmatically reset a password for a customer user or full partner user. Use the Office365 admin center or Azure portal. See [Reset the password for a user in Azure Active Directory](https://azure.microsoft.com/en-us/documentation/articles/active-directory-users-reset-password-azure-portal/). Note that in Step 1, you need to sign into the Azure portal for Microsoft Cloud Germany.
-   App ID creation. Developers who want to integrate Partner Center API/SDK functionality in their app for Partner Center for Microsoft Cloud Germany must register their app ID manually. See [Register app details for Partner Center for Microsoft National Cloud] (https://msdn.microsoft.com/en-us/library/partnercenter/mt745084.aspx).   

## <span id="partner_center_msftcloudUS"></span><span id="partner_center_msftcloudus"></span><span id="PARTNER_CENTER_MSFTCLOUDUS"></span>Partner Center for Microsoft Cloud for U.S. Government


-   Office 365 subscriptions are not currently available for Partner Center for Microsoft Cloud for US Government.

-   Existing partners supporting Microsoft Cloud for U.S. Government must create new accounts in Partner Center for Microsoft Cloud for US Government.

-   Multichannel and multipartner and request relationship with an existing customer within Microsoft Cloud for U.S. Government scenarios do not apply. This is because Office 365 is not currently available. Microsoft Cloud for U.S. Government customers must transact with a single partner.

-   Partners cannot create users for their customer's organization or assign roles. Partners can read fields, but cannot write or update them. Partners must manually create or update their customers' users in the Office365 admin center or through the Azure portal. See [Azure Active Directory Documentation](https://docs.microsoft.com/en-us/azure/active-directory/).

-   You cannot programmatically reset a password for a customer user or full partner user. Use the Azure portal. See [Reset the password for a user in Azure Active Directory](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-users-reset-password-azure-portal). Note that in Step 1, you need to sign into the Azure portal for Microsoft Cloud for U.S. Government.

-   REST endpoints for Partner Center for Microsoft Cloud for US Government are the same as for Partner Center: https://api.partnercenter.microsoft.com.

-   App ID creation. Developers who want to integrate Partner Center API/SDK functionality in their app for Partner Center for Microsoft Cloud for US Government must register their app ID manually. See [Register app details for Partner Center for Microsoft National Cloud] (https://msdn.microsoft.com/en-us/library/partnercenter/mt745084.aspx).

 

 




