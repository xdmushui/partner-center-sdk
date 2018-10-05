---
title: Change the billing cycle
description: Updates a subscription from monthly to annual billing or from annual to monthly billing.
ms.assetid: 
ms.date: 10/10/2018
ms.localizationpriority: medium
---

# Change the billing cycle


**Applies To**

<!-- TODO: Verify that this is the correct Applies To values -->
-   Partner Center
-   Partner Center operated by 21Vianet
-   Partner Center for Microsoft Cloud Germany
-   Partner Center for Microsoft Cloud for US Government

Updates a [Subscription](subscriptions.md) from monthly to annual billing or from annual to monthly billing.

In the Partner Center dashboard, this operation can be performed by... <!-- TODO: Link to Pete's new doc -->

## <span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>Prerequisites

<!-- TODO: Is this all correct?-->
- Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.
- A customer ID (customer-tenant-id). If you do not have a customer's ID, you can look up the ID in Partner Center by choosing the customer from the customers list, selecting Account, then saving their Microsoft ID.
- A subscription ID.


## <span id="C_"></span><span id="c_"></span>C#

To change the frequency of the billing cycle... <!-- TODO: Fill out this description and add a C# code snippet -->

<!-- TODO: Add code snippet here -->
``` csharp

```


## <span id="REST_Request"></span><span id="rest_request"></span><span id="REST_REQUEST"></span>REST Request

**Request syntax**

<!-- TODO: Update with the correct request URI -->
| Method    | Request URI                                                                                                               |
|-----------|---------------------------------------------------------------------------------------------------------------------------|
| **PATCH** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1 |

 
**URI parameter**

<!-- TODO: Update with any required parameters or delete this section if there are no parameters -->
This table lists the required query parameter to change the quantity of the subscription.

| Name                    | Type     | Required | Description                               |
|-------------------------|----------|----------|-------------------------------------------|
| **customer-tenant-id**  | **guid** | Y        | A GUID corresponding to the customer.     |
| **id-for-subscription** | **guid** | Y        | A GUID corresponding to the subscription. |
 

**Request headers**

-   See [Headers](headers.md) for more information.


**Request body**

<!-- TODO: Verify that these are the correct request body requirements -->
A full **Subscription** resource is required in the request body. Ensure that the **billingCycle** property has been updated.


**Request examples**

**Update to annual billing**
<!-- TODO: Add a request example to change to annual billing -->
```http

```

**Update to monthly billing**
<!-- TODO: Add a request example to change to monthly billing -->
```http

```

## <span id="REST_Response"></span><span id="rest_response"></span><span id="REST_RESPONSE"></span>REST Response

If successful, this method returns <!-- TODO: Add what is returned -->  in the response body.


**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Error Codes](error-codes.md).


**Response example**
<!-- Do we need multiple response examples for both annual and monthly? -->

<!-- TODO: Update with an example of a response -->
```http

```
