---
title: Test and debug with integration sandbox
description: Learn how to use your Partner Center integration sandbox account (and related tokens) to test and debug your code so you don't accidentally incur new charges.
ms.date: 09/11/2018
ms.service: partner-dashboard
ms.subservice:  partnercenter-sdk
---

# Test and debug with your Partner Center integration sandbox to avoid paying unexpected charges

**Applies To**

- Partner Center
- Partner Center operated by 21Vianet
- Partner Center for Microsoft Cloud Germany
- Partner Center for Microsoft Cloud for US Government

To test your code, you should use your integration sandbox account in Partner Center (and the corresponding tokens) so that you don't accidentally incur new charges that your company is responsible for paying. For more information about this test-in-production (TiP) environment, see [Set up API access in Partner Center](set-up-api-access-in-partner-center.md).

## Integration sandbox constraints

If you run automated build verification tests, conduct testing in production, or perform manual testing in the integration sandbox, you may reach the maximum limits for the integration sandbox. These limits are 75 customers, 5 subscriptions per customer, and 25 licenses per subscription.

- The 25-licenses limit means you cannot acquire an offer in the sandbox that has a minimum license requirement that exceeds 25 licenses. This limitation includes trials.

- Usage summary can't be obtained on sandbox accounts, as those accounts are for testing purposes.

- APIs related to billing and invoice will not work in the sandbox, as no invoices are generated for the test account.


### Azure plan

By default, partners cannot provision Azure plans using their sandbox accounts. Partners who need to do so with their sandbox account must apply for access. To apply for access, reach out to your Microsoft account manager or business contact. Partners who have previously applied for access to provision Microsoft Azure (MS-AZR-0145P) subscriptions in their sandbox accounts do not need to apply for access again. They will be granted access to provision Azure plans automatically.

For partners whose sandbox accounts have been approved to provision Azure plans, the following limits apply:

- Each sandbox partner account can have up to 10 Azure plans across all customer tenants (no matter how the plans are distributed among the customers).

- A direct bill partner can create up to one Azure plan per customer tenant.

- An indirect provider can create up to three Azure plans per customer tenant (for different indirect resellers specified as the Partner-of-Record).

- Each Azure plan can have up to three Azure subscriptions.

- Each CSP Azure subscription under your sandbox account is limited to four virtual machine (VM) cores per data center. Therefore, you cannot provision VM SKUs that require more than four VM cores. Certain specialized VM SKUs such as GPU cores are also excluded.

- Each sandbox partner account has a spending limit of $2000 (USD) per billing cycle across all Azure plans. Once a partner reaches the spend limit, all Azure plans will be temporarily disabled until the next billing cycle.

### Cloud Solution Provider (CSP) Azure subscription offers

CSP Azure subscription offers are no longer available by default to sandbox accounts. These include MS-AZR-0146P, MS-AZR-DE-0146P and MS-AZR-USGOV-0146P for CSP Azure subscriptions in Microsoft Public Cloud, German Cloud, and Government Cloud respectively. Partners who need access to these offers with their sandbox account must apply for access. To apply for access, discuss with your Microsoft account manager or business contact.

For partners whose sandbox accounts have been approved for CSP Azure subscription offers, the following limits apply:

- You can have up to a maximum of 375 active subscriptions (75 customers x 5 subscriptions per customer). However, only 10 of which can be CSP Azure subscriptions.

- When a CSP Azure subscription reaches $200 of Azure usage, its resources are temporarily disabled until its next billing cycle. It is still considered an active subscription and is counted towards the 10 active Azure subscriptions limit.

- Each CSP Azure subscription under your sandbox account is limited to four virtual machine (VM) cores per data center. Therefore, you cannot provision VM SKUs that require more than four VM cores. Certain specialized VM SKUs such as GPU cores are also excluded.

> [!Important]
> All existing CSP Azure subscriptions provisioned with sandbox accounts prior to August 1, 2018 are no longer supported and will be deprovisioned by Microsoft between October 16 - October 31, 2018. After the subscriptions have been deprovisioned, they cannot be re-enabled, and associated data are no longer accessible. Partners who have valuable data stored under these subscriptions must back up the data before October 16, 2018.

### Azure Reserved VM instance

If you are [purchasing an Azure Reserved VM instance](purchase-azure-reservations.md) with your sandbox account, you are limited to two VM instances per customer. You are also limited to selecting only from the following Azure Reserved VM instance product SKUs:

| Product Title  | Effective Date  | Sku Title                                               | Region [ArmRegionName] | Instance Key [ArmSkuName] | Duration | Consumption Meter Id       |
|----------------|-----------------|---------------------------------------------------------|------------------------|--------------|----------|----------------------------|
| B Series       | 12/1/2017 0:00  | Reserved VM instance, Standard_B1s, KR South, 1 year    | KoreaSouth             | `Standard_B1s` | `1Year`    | 3f913071-0dd7-4258-8ec4-6fad05bd976d |
| B Series       | 12/1/2017 0:00  | Reserved VM instance, Standard_B1s, US East, 1 year     | eastus                 | `Standard_B1s` | `1Year`    | f4d7a5a5-1b67-45ea-b1a0-282fbdd34b05 |
| B Series       | 12/1/2017 0:00  | Reserved VM instance, Standard_B1s, US West 2, 1 year   | westus2                | `Standard_B1s` | `1Year`    | 222e39f5-e99f-4fa3-a323-f46402977888 |
| B Series       | 12/1/2017 0:00  | Reserved VM instance, Standard_B1s, US North Central, 1 year    | northcentralus | `Standard_B1s` | `1Year`    | 4e1716fc-4842-43f1-aa96-7c1b1b1395a7 |
| B Series       | 12/1/2017 0:00  | Reserved VM instance, Standard_B1s, CA East, 1 year     | CanadaEast             | `Standard_B1s` | `1Year`    | ab8a5993-5db7-47c8-b3b1-2e1365b353fb |

### Subscriptions for commercial marketplace products

In production, after you have [created a subscription to commercial marketplace SaaS products](create-subscription-azure-marketplace-products.md), you need to retrieve a personalized activation link from Partner Center and visit the publisher's site to complete the setup process. Subscription billing will begin only after setup is complete.

In the CSP sandbox environment, there is no integration with ISVs. If you try to retrieve an activation link from Partner Center, a dummy link will be returned. You cannot use this dummy link to complete the setup process at the publisher's site. To use the integration sandbox account to test billing for subscriptions to commercial marketplace SaaS products, see [Activate a sandbox subscription for commercial marketplace products](activate-sandbox-subscription-azure-marketplace-products.md) instead. Subscription billing will begin after successful activation.

To clean up at the end of your test run so there's space for the next round of testing, see the following articles:

- [Delete a customer account from the integration sandbox](delete-a-customer-account-from-the-integration-sandbox.md)

- [Decrease the quantity of a subscription](change-the-quantity-of-a-subscription.md)

- [Suspend a subscription](suspend-a-subscription.md) so that you can remove it.

## Best practices for REST development

- Use a network trace tool so that you can see your request, the response, and if there were any errors in the HTTP status code in the response. For more information about error handling, see [Partner Center REST error codes](error-codes.md).

- Use a new Correlation ID for each call made to the Partner Center REST API. This practice ensures better logging and will help during debugging. For more information, see [Partner Center REST headers](headers.md).

## Troubleshooting tips for common REST problems

- Review all header properties, including the URL and API version.

- Ensure properties are included if necessary, and correctly formatted.

- Incorrect array formatting is a common error.

- **ETags** are temporary and as result, should not be stored. When a function call requires an **ETags**, use the latest **ETags** value by getting the resource again. **ETags** values should be included in double quotation marks, like a string:

   ```rest
   If-Match : "eyJpZCI6IjUwMWE4NjBjLTE2OTgtNDQyYi04MDhjLTRiNjEyY2NmMzVmMiIsInZlcnNpb24iOjF9"
   ```
