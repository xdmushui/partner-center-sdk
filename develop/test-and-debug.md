---
title: Test and debug
description: To test your code, you should use your integration sandbox account in Partner Center (and the corresponding tokens) so that you don't accidentally incur new charges that your company is responsible for paying.
ms.assetid: 0A84F92F-CE66-42DF-B686-4D9E6FFECB16
ms.author: v-thpr
ms.date: 12/15/2017
ms.topic: article
ms.prod: partner-center
ms.technology: partner-center-sdk
---

# Test and debug


**Applies To**

-   Partner Center
-   Partner Center operated by 21Vianet
-   Partner Center for Microsoft Cloud Germany
-   Partner Center for Microsoft Cloud for US Government

To test your code, you should use your integration sandbox account in Partner Center (and the corresponding tokens) so that you don't accidentally incur new charges that your company is responsible for paying. For more information about this test-in-production (TiP) environment, see [Set up API access in Partner Center](set-up-api-access-in-partner-center.md).

## <span id="Integration_sandbox_constraints"></span><span id="integration_sandbox_constraints"></span><span id="INTEGRATION_SANDBOX_CONSTRAINTS"></span>Integration sandbox constraints


If you run automated build verification tests, conduct testing in production, or perform manual testing in the integration sandbox, you may reach the maximum limits for the integration sandbox. These limits are 75 customers, 5 subscriptions per customer, 25 seats per subscription, and $200 of Azure usage per month.

Note that this means you cannot acquire an offer in the sandbox that has a minimum seat requirement that exceeds 25 seats. This includes trials.

If you are [purchasing an Azure Reserved VM Instance](purchase-azure-reserved-vm-instances.md) with your sandbox account, you are limited to 2 VM Instances per customer. You are also limited to selecting only from the following Azure Reserved VM Instance product SKUs: 

| Product Title  | Effective Date  | Sku Title                                               | Region [ArmRegionName] | Instance Key [ArmSkuName] | Duration | Consumption Meter Id       |
|----------------|-----------------|---------------------------------------------------------|------------------------|--------------|----------|----------------------------|
| B Series       | 12/1/2017 0:00  | Reserved VM instance, Standard_B1s, KR South, 1 year    | KoreaSouth             | Standard_B1s | 1Year    | 3f913071-0dd7-4258-8ec4-6fad05bd976d |
| B Series       | 12/1/2017 0:00  | Reserved VM instance, Standard_B1s, US East, 1 year     | eastus                 | Standard_B1s | 1Year    | f4d7a5a5-1b67-45ea-b1a0-282fbdd34b05 |
| B Series       | 12/1/2017 0:00  | Reserved VM instance, Standard_B1s, US West 2, 1 year   | westus2                | Standard_B1s | 1Year    | 222e39f5-e99f-4fa3-a323-f46402977888 |
| B Series       | 12/1/2017 0:00  | Reserved VM instance, Standard_B1s, US North Central, 1 year    | northcentralus | Standard_B1s | 1Year    | 4e1716fc-4842-43f1-aa96-7c1b1b1395a7 |
| B Series       | 12/1/2017 0:00  | Reserved VM instance, Standard_B1s, CA East, 1 year     | CanadaEast             | Standard_B1s | 1Year    | ab8a5993-5db7-47c8-b3b1-2e1365b353fb |
     

To clean up at the end of your test run so there's space for the next round of testing, see the following topics:

-   [Delete a customer account from the integration sandbox](delete-a-customer-account-from-the-integration-sandbox.md)

-   [Decrease the quantity of a subscription](change-the-quantity-of-a-subscription.md)

-   [Suspend a subscription](suspend-a-subscription.md) so that you can remove it.

## <span id="Best_practices_for_REST_development"></span><span id="best_practices_for_rest_development"></span><span id="BEST_PRACTICES_FOR_REST_DEVELOPMENT"></span>Best practices for REST development


-   Use a network trace tool so that you can see your request, the response, and if there were any errors in the HTTP status code in the response. For more information about error handling, see [Partner Center REST error codes](error-codes.md).

-   Use a new Correlation ID for each call made to the Partner Center REST API. This ensures better logging and will help during debugging. For more information, see [Partner Center REST headers](headers.md).

## <span id="Troubleshooting_tips_for_common_REST_problems"></span><span id="troubleshooting_tips_for_common_rest_problems"></span><span id="TROUBLESHOOTING_TIPS_FOR_COMMON_REST_PROBLEMS"></span>Troubleshooting tips for common REST problems


-   Review all header properties, including the URL and API version.

-   Ensure properties are included if required, and correctly formatted.

-   Incorrect array formatting is a common error.

-   **ETags** are temporary and therefore should not be stored. When a function call requires an **ETags**, use the latest **ETags** value by getting the resource again. **ETags** values should be included in double quotation marks, like a string:

    ```
    If-Match : "eyJpZCI6IjUwMWE4NjBjLTE2OTgtNDQyYi04MDhjLTRiNjEyY2NmMzVmMiIsInZlcnNpb24iOjF9"
    ```

 

 




