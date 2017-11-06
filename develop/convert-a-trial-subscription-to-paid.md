---
title: Convert a trial subscription to paid
description: How to convert a trial subscription to paid.
MSHAttr:
- 'PreferredSiteName:MSDN'
- 'PreferredLib:/library/PartnerCenter'
ms.assetid: 06EB96D7-6260-47E0-ACAE-07D4213BEBB7
---

# Convert a trial subscription to paid


**Applies To**

-   Partner Center

How to convert a trial subscription to paid.

## <span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>Prerequisites


-   Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with App+User credentials only.
-   A customer identifier.
-   A subscription ID for an active trial subscription.
-   An available conversion offer.

## <span id="Convert_a_trial_subscription_to_paid_through_code"></span><span id="convert_a_trial_subscription_to_paid_through_code"></span><span id="CONVERT_A_TRIAL_SUBSCRIPTION_TO_PAID_THROUGH_CODE"></span>Convert a trial subscription to paid through code


To convert a trial subscription to paid, you must first obtain a collection of the trial conversions available and then choose the conversion offer that you want to purchase. The conversion offers will specify a quantity that defaults to the same number of licenses as the trial subscription. You can change that by setting the [**Quantity**](pc_sdk_models_subscrpt.conversion_quantity) property to the number of licenses that you want to purchase. Note that regardless of the number of licenses purchased, the subscription ID of the trial is reused for the purchased licenses. Thus, the trial in effect disappears and is replaced by the purchase.

Here are the steps to convert a trial subscription through code:

1.  Get an interface to the subscription operations available. You must identify the customer and specify the subscription identifier of the trial subscription.
    ```
    var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);
    ```

2.  Get a collection of the available conversion offers. For more information and details on the request/response for this method, see [Get a list of trial conversion offers](get-a-list-of-trial-conversion-offers.md).
    ```
    var conversions = subscriptionOperations.Conversions.Get();
    ```

3.  Choose a conversion offer. The following code chooses the first conversion offer in the collection.
    ```
    var selectedConversion = conversions.Items.ToList()[0];
    ```

4.  Optionally, specify the number of licenses to purchase. The default is the number of licenses in the trial subscription.
    ```
    selectedConversion.Quantity = 10;
    ```

5.  Call the [**Create**](pc_sdk_subscrpt.isubscriptionupgradecollection_create) or [**CreateAsync**](pc_sdk_subscrpt.isubscriptionupgradecollection_createasync) method to convert the trial subscription to paid.
    ```
    var convertResult = subscriptionOperations.Conversions.Create(selectedConversion);
    ```

## <span id="C_"></span><span id="c_"></span>C#


To convert a trial subscription to paid, first use the [**IAggregatePartner.Customers.ById**](pc_sdk_cust.icustomercollection_byid) method with the customer ID to identify the customer. Then, get an interface to subscription operations by calling the [**Subscriptions.ById**](pc_sdk_cust_user.icustomerusercollection_byid) method with the trial subscription ID. Save a reference to the subscription operations interface in a local variable.

Next, use the [**Conversions**](pc_sdk_subscrpt.isubscription_conversions) property to obtain an interface to the available operations on conversions, and then call the [**Get**](pc_sdk_subscrpt.isubscriptionconversioncollection_get) or [**GetAsync**](pc_sdk_subscrpt.isubscriptionconversioncollection_getasync) method to retrieve a collection of available [**Conversion**](pc_sdk_models_subscrpt.conversion) offers. You must choose one. In the example below, we default to the first conversion available.

Having selected a conversion offer, the next step is to use the reference to the subscription operations interface that you saved in a local variable and use the [**Conversions**](pc_sdk_subscrpt.isubscription_conversions) property to obtain an interface to the available operations on conversions. Then pass the selected conversion offer object to the [**Create**](pc_sdk_subscrpt.isubscriptionupgradecollection_create) or [**CreateAsync**](pc_sdk_subscrpt.isubscriptionupgradecollection_createasync) method to attempt the trial conversion.

```
// IAggregatePartner partnerOperations;
// string customerId;
// string subscriptionId; 

// Get subscription operations for the trial subscription.
var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);

// Get the available conversions.
var conversions = subscriptionOperations.Conversions.Get();

// If there are no conversions available, we&#39;re done. 
// Otherwise, convert the trial to the first available conversion offer.
if (conversions.TotalCount <= 0)
{
    System.Console.WriteLine("This subscription has no conversions");
}
else
{
    // Default to the first conversion.
    var selectedConversion = conversions.Items.ToList()[0];

    // Convert the trial and return the result.
    var convertResult = subscriptionOperations.Conversions.Create(selectedConversion);
}
```

## <span id="_Request"></span><span id="_request"></span><span id="_REQUEST"></span> Request


**Request syntax**

| Method   | Request URI                                                                                                                 |
|----------|-----------------------------------------------------------------------------------------------------------------------------|
| **POST** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/conversions HTTP/1.1 |

 

**URI parameter**

Use the following path parameters to identify the customer and trial subscription.

| Name            | Type   | Required | Description                                                     |
|-----------------|--------|----------|-----------------------------------------------------------------|
| customer-id     | string | Yes      | A GUID formatted string that identifies the customer.           |
| subscription-id | string | Yes      | A GUID formatted string that identifies the trial subscription. |

 

**Request headers**

-   See [Partner Center REST headers](headers.md) for more information.

**Request body**

A populated [Conversion](conversions.md#conversion) resource must be included in the request body.

**Request example**

```
POST https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/488745B5-2086-4912-802C-6ABB9F7C3638/conversions HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: bd0cde7f-ba87-4010-8a73-1190b641f2a4
MS-CorrelationId: 8daa6d54-72ab-4d6b-9c7d-9266d3734a47
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 234
Expect: 100-continue

{
    "OfferId": "C0BD2E08-11AC-4836-BDC7-3712E744922F",
    "TargetOfferId": "031C9E47-4802-4248-838E-778FB1D2CC05",
    "OrderId": "D51A052E-043C-4A2A-AA37-2BB938CEF6C1",
    "Quantity": 25,
    "BillingCycle": "monthly",
    "Attributes": {
        "ObjectType": "Conversion"
    }
}
```

## <span id="_Response"></span><span id="_response"></span><span id="_RESPONSE"></span> Response


If successful, the response body contains a [ConversionResult](conversions.md#conversionresult) resource.

**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center error codes](error-codes.md).

**Response example**

```
HTTP/1.1 200 OK
Content-Length: 211
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 8daa6d54-72ab-4d6b-9c7d-9266d3734a47
MS-RequestId: bd0cde7f-ba87-4010-8a73-1190b641f2a4
MS-CV: kW4GzmhvHEqCq1ls.0
MS-ServerId: 030020643
Date: Thu, 15 Jun 2017 23:10:40 GMT

﻿{
    "subscriptionId": "488745B5-2086-4912-802C-6ABB9F7C3638",
    "offerId": "C0BD2E08-11AC-4836-BDC7-3712E744922F",
    "targetOfferId": "031C9E47-4802-4248-838E-778FB1D2CC05",
    "attributes": {
        "objectType": "ConversionResult"
    }
}
```

 

 




