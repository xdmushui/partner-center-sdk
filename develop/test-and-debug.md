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

To test your code, you should use your integration sandbox account in Partner Center (and the corresponding tokens) so that you don't accidentally incur new charges that your company is responsible for paying. For more information about this test-in-production (TiP) environment, see [Set up Partner Center accounts for API access](pc_cloud_sltn_provider.access_the_crest_api_with_your_csp_account).

## <span id="Integration_sandbox_constraints"></span><span id="integration_sandbox_constraints"></span><span id="INTEGRATION_SANDBOX_CONSTRAINTS"></span>Integration sandbox constraints


If you run automated build verification tests, conduct testing in production, or perform manual testing in the integration sandbox, you may reach the maximum limits for the integration sandbox. These limits are 75 customers, 5 subscriptions per customer, 5 seats per subscription, and $200 of Azure usage per month.

Note that this means you cannot acquire an offer in the sandbox that has a minimum seat requirement that exceeds 5 seats. This includes trials.

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

 

 




