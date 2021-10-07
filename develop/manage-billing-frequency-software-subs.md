---
title: Manage billing frequency for software subscriptions
description: Update billing frequency for a Subscription resource that matches the customer and subscription ID.

ms.date: 02/23/2021
ms.service: partner-dashboard
ms.subservice:  partnercenter-sdk
---

# Update billing frequency for software subscriptions

**Applies To**: Partner Center

Update the billing frequency for a software [Subscription](subscription-resources.md) resource that matches the customer and subscription ID.

In the Partner Center dashboard, this operation is performed by first [selecting a customer](get-a-customer-by-name.md). Then, select the subscription that you wish to update. Finally, click Manage scheduled changed to select option, then select **Save**.

## Prerequisites

- Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.

- A customer ID (`customer-tenant-id`). If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard). Select **CSP** from the Partner Center menu, followed by **Customers**. Select the customer from the customer list, then select **Account**. On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section. The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).

- A subscription ID.

## C\#

To update a customer's software subscription, first [Get the subscription](get-a-subscription-by-id.md), then set the subscription's [**billingCycle**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.billingCycle) property. Once the change is made, use your **IAggregatePartner.Customers** collection and call the **ById()** method. Then call the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, followed by the [**ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method. Then, finish by calling the **Patch()** method.

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;
// Subscription selectedSubscription;

this.Context.ConsoleHelper.StartProgress("Updating subscription scheduled change");
selectedSubscription.ScheduledNextTermInstructions = new ScheduledNextTermInstructions
{
    Product = new ProductTerm
    {
        ProductId = changeToProductId,
        SkuId = changeToSkuId,
        AvailabilityId = changeToAvailabilityId,
        BillingCycle = changeToBillingCycle,
        TermDuration = changeToTermDuration,
    },
    Quantity = changeToQuantity,
};

var updatedSubscription = subscriptionOperations.Patch(selectedSubscription);
```

**Sample**: [Console test app](console-test-app.md). **Project**: PartnerSDK.FeatureSample **Class**: UpdateSubscription.cs

## REST request

### Request syntax

| Method    | Request URI                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------|
| **PATCH** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1 |

### URI parameter

This table lists the required query parameter to suspend the subscription.

| Name                    | Type     | Required | Description                               |
|-------------------------|----------|----------|-------------------------------------------|
| **customer-tenant-id**  | **GUID** | Y        | A GUID corresponding to the customer.     |
| **id-for-subscription** | **GUID** | Y        | A GUID corresponding to the subscription. |

### Request headers

For more information, see [Partner Center REST headers](headers.md).

### Request body

A full commercial marketplace **Subscription** resource is required in the request body. Ensure that the **AutoRenewEnabled** property has been updated.

### Request example for a software subscription

```http
{ 
    "id": "d3b7c9a2-9a4b-40b2-b075-6e442909e3e7", 
    "offerId": "DG7GMGF0DVSV:000P:DG7GMGF0F3Q9", 
    "offerName": "Windows Server Remote Desktop Services CAL - 1 User CAL – 3 year", 
    "friendlyName": "Windows Server Remote Desktop Services CAL - 1 User CAL – 3 year", 
    "productType": { 
        "id": "Software", 
        "displayName": "Software" 
    }, 
    "quantity": 1, 
    "unitType": "Licenses", 
    "hasPurchasableAddons": false, 
    "creationDate": "2021-09-14T16:44:14.1210743Z", 
    "effectiveStartDate": "2021-09-14T16:44:03.4609789Z", 
    "commitmentEndDate": "2024-09-13T00:00:00Z", 
    "cancellationAllowedUntilDate": "2021-10-14T23:59:00Z", 
    "status": "active", 
    "autoRenewEnabled": true, 
    "scheduledNextTermInstructions": { 
      "product": { 
         "productId":  "DG7GMGF0DVSV", 
         "skuId":  "000P", 
         "availabilityId":  "DG7GMGF0F3Q9", 
         "billingCycle":  "Annual", 
         "termDuration":  "P3Y" 
        }, 
      "quantity":  1 
     },  // original value = null 
    "isTrial": false, 
    "billingType": "license", 
    "billingCycle": "triennial", 
    "termDuration": "P3Y", 
    "renewalTermDuration": "", 
    "isMicrosoftProduct": true, 
    "partnerId": "", 
    "attentionNeeded": false, 
    "actionTaken": false, 
    "contractType": "subscription", 
    "links": { 
        "product": { 
            "uri": "/products/DG7GMGF0DVSV?country=US", 
            "method": "GET", 
            "headers": [] 
        }, 
        "sku": { 
            "uri": "/products/DG7GMGF0DVSV/skus/000P?country=US", 
            "method": "GET", 
            "headers": [] 
        }, 
        "availability": { 
            "uri": "/products/DG7GMGF0DVSV/skus/000P/availabilities/DG7GMGF0F3Q9?country=US", 
            "method": "GET", 
            "headers": [] 
        }, 
        "self": { 
            "uri": "/customers/1f53d7b3-cd04-43a3-a09f-e52f3eb3c205/subscriptions/d3b7c9a2-9a4b-40b2-b075-6e442909e3e7", 
            "method": "GET", 
            "headers": [] 
        } 
    }, 
    "publisherName": "Microsoft", 
    "orderId": "123456789101", 
    "attributes": { 
        "objectType": "Subscription" 
    } 
} 
```

## REST response

If successful, this method returns updated [Subscription](subscription-resources.md) resource properties in the response body.

### Response success and error codes

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Error Codes](error-codes.md).

### Response example

```http
{ 
    "id": "d3b7c9a2-9a4b-40b2-b075-6e442909e3e7", 
    "offerId": "DG7GMGF0DVSV:000P:DG7GMGF0F3Q9", 
    "offerName": "Windows Server Remote Desktop Services CAL - 1 User CAL – 3 year", 
    "friendlyName": "Windows Server Remote Desktop Services CAL - 1 User CAL – 3 year", 
    "productType": { 
        "id": "Software", 
        "displayName": "Software" 
    }, 
    "quantity": 1, 
    "unitType": "Licenses", 
    "hasPurchasableAddons": false, 
    "creationDate": "2021-09-14T16:44:14.1210743Z", 
    "effectiveStartDate": "2021-09-14T16:44:03.4609789Z", 
    "commitmentEndDate": "2024-09-13T00:00:00Z", 
    "cancellationAllowedUntilDate": "2021-10-14T23:59:00Z", 
    "status": "active", 
    "autoRenewEnabled": true, 
    "scheduledNextTermInstructions": { 
      "product": { 
         "productId":  "DG7GMGF0DVSV", 
         "skuId":  "000P", 
         "availabilityId":  "DG7GMGF0F3Q9", 
         "billingCycle":  "Annual", 
         "termDuration":  "P3Y" 
        }, 
      "quantity":  1 
     },  // original value = null 

    "isTrial": false, 
    "billingType": "license", 
    "billingCycle": "triennial", 
    "termDuration": "P3Y", 
    "renewalTermDuration": "", 
    "isMicrosoftProduct": true, 
    "partnerId": "", 
    "attentionNeeded": false, 
    "actionTaken": false, 
    "contractType": "subscription", 
    "links": { 
        "product": { 
            "uri": "/products/DG7GMGF0DVSV?country=US", 
            "method": "GET", 
            "headers": [] 
        }, 
        "sku": { 
            "uri": "/products/DG7GMGF0DVSV/skus/000P?country=US", 
            "method": "GET", 
            "headers": [] 
        }, 
        "availability": { 
            "uri": "/products/DG7GMGF0DVSV/skus/000P/availabilities/DG7GMGF0F3Q9?country=US", 
            "method": "GET", 
            "headers": [] 
        }, 
        "self": { 
            "uri": "/customers/1f53d7b3-cd04-43a3-a09f-e52f3eb3c205/subscriptions/d3b7c9a2-9a4b-40b2-b075-6e442909e3e7", 
            "method": "GET", 
            "headers": [] 
        } 
    }, 
    "publisherName": "Microsoft", 
    "orderId": "123456789101", 
    "attributes": { 
        "objectType": "Subscription" 
    } 
} 
```
