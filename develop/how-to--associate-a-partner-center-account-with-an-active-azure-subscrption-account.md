---
title: Associate a Partner Center Account with an Active Azure Subscription Account
description: The following topic describes how to associate an existing Partner Center account with an active Azure subscription account.
MSHAttr:
- 'PreferredSiteName:MSDN'
- 'PreferredLib:/library/PartnerCenter'
ms.assetid: A12C3DF9-B05E-4E32-9F33-CAE19F99A9AE
---

# Associate a Partner Center Account with an Active Azure Subscription Account


**Applies To**

-   Partner Center
-   Partner Center for Microsoft Cloud Germany
-   Partner Center for Microsoft Cloud for US Government

The following topic describes how to associate an existing Partner Center account with an active Azure subscription account.

## <span id="What_you_need_to_know"></span><span id="what_you_need_to_know"></span><span id="WHAT_YOU_NEED_TO_KNOW"></span>What you need to know


### <span id="Technologies"></span><span id="technologies"></span><span id="TECHNOLOGIES"></span>Technologies

-   [Partner Center](partner-center-api-and-sdk.md)

### <span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>Prerequisites

-   An existing Partner Center account
-   An active Azure subscription

Instructions
------------

### <span id="Set_up_your_Azure_account_to_use_an_existing_Partner_Center_directory"></span><span id="set_up_your_azure_account_to_use_an_existing_partner_center_directory"></span><span id="SET_UP_YOUR_AZURE_ACCOUNT_TO_USE_AN_EXISTING_PARTNER_CENTER_DIRECTORY"></span>Step 1: Set up your Azure account to use an existing Partner Center directory

1.  Log on to the [Azure Portal](https://manage.windowsazure.com) using your Microsoft Azure (MSA) account.

2.  On the left navigation bar, select **Settings**, and then select the **New** button at the bottom of the page.

3.  On the **New** dialog, select **AppServices**, then select **Active Directory**, then select **Directory**, and then select **Custom Create**.

4.  On the **Add directory** dialog, select **Use existing directory**, and then select the check mark at the bottom-right hand corner of the page.

    selecting the check mark will log you out of the Azure Portal site.

### <span id="Associate_the_Partner_Center_credentials_with_the_Azure_account"></span><span id="associate_the_partner_center_credentials_with_the_azure_account"></span><span id="ASSOCIATE_THE_PARTNER_CENTER_CREDENTIALS_WITH_THE_AZURE_ACCOUNT"></span>Step 2: Associate the Partner Center credentials with the Azure account

1.  Log back into the Azure Portal with your Partner Center account credentials.

    When you log back in, you will be greeted with a pop-up dialog, asking if you wish to use your Partner Center directory with Azure.

2.  Select **Continue**, and then select **Sign out now**.

### <span id="_Map_the_directory"></span><span id="_map_the_directory"></span><span id="_MAP_THE_DIRECTORY"></span>Step 3: Map the directory

1.  Log back in to the Azure Portal using your MSA account.
2.  From the left navigation bar, select **Active Directory**.

    In the **Active Directory** table, you will see your newly-added Partner Center account.

3.  In the left navigation bar, select **Settings**, and then select the **Edit Directory** button at the bottom of the page.

4.  On the **Change the Associated Directory** page, in the **Directory** drop-down, select your Partner Center account, and then select the **Next** arrow.

5.  On the **Confirm Directory Mapping** page, confirm that the information is correct, and then select the check mark.

    The Azure Portal page will now re-load with the updated information.

### <span id="Add_the_Partner_Center_administrator_credentials_to_the_Azure_account"></span><span id="add_the_partner_center_administrator_credentials_to_the_azure_account"></span><span id="ADD_THE_PARTNER_CENTER_ADMINISTRATOR_CREDENTIALS_TO_THE_AZURE_ACCOUNT"></span>Step 4: Add the Partner Center administrator credentials to the Azure account

1.  On the Azure Portal page, in the left navigation bar, select **Settings**, and then select your subscription.

    Note that the information in the Directory column has now been updated with the new directory.

2.  select on the **Administrators** tab, and then select on the **Add** button at the bottom of the page.

3.  On the **Specify a co-Administrator for subscriptions** dialog, enter the e-mail address of the Partner Center admin account.

4.  Select the **Subscription** check-box, and then select on the check in the lower-right hand corner.

### <span id="Confirm_your_changes"></span><span id="confirm_your_changes"></span><span id="CONFIRM_YOUR_CHANGES"></span>Step 5: Confirm your changes

-   Log on to the Partner Center site, and navigate to the **Web storefront** deployment link.

    In the **Subscription** drop-down, you should now find the newly-added subscription.

 

 




