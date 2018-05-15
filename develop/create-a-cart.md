---
title: Create a cart
description: How to add an order for a customer in a cart.
ms.assetid: 
ms.author: v-thpr
ms.date: 03/19/18
ms.topic: article
ms.prod: partner-center
ms.technology: partner-center-sdk
---

# Create a cart


**Applies To**

-   Partner Center


How to add an order for a customer in a cart. For more information about what is currently available to sell, see [CSP agreements, price lists, and offers](https://msdn.microsoft.com/partner-center/csp-documents-and-learning-resources).

## <span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>Prerequisites


-   Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.
-   A customer identifier. If you do not have a customer's ID, you can look up the ID in Partner Center by choosing the customer from the customers list, selecting Account, then saving their Microsoft ID.


## <span id="C_"></span><span id="c_"></span>C#


To create an order for a customer, first instantiate a Cart object. Next, create a list of **CartLineItem** objects, and assign the list to the Cart's LineItems property. Each cart line item contains the purchase information for one Product. You must have at least one cart line item. 

Next, obtain an interface to cart operations by calling the **IAggregatePartner.Customers.ById** method with the customer ID to identify the customer, and then retrieving the interface from the **Cart** property.

Finally, call the **Create** or **CreateAsync** method to create the order.


```CSharp
IAggregatePartner partnerOperations;
string customerId;
string catalogItemId;
string subscriptionId;

var cart = new Cart()
{
    LineItems = new List<CartLineItem>()
    {
        catalogItemId = catalogItemId,
        FriendlyName = "A_sample_Azure_RI",
        Quantity = 5,
        BillingCycle = BillingCycleType.OneTime,
        ProvisioningContext = new Dictionary<string, string>
        {
            { "subscriptionId", subscriptionId },
            { "scope", "shared" },
            { "duration", "3Years" }            
        }   
    }
};

var createdCart = partnerOperations.Customers.ById(customerId).Cart.Create(cart);
```

## <span id="REST_Request"></span><span id="rest_request"></span><span id="REST_REQUEST"></span>REST Request


**Request syntax**

| Method   | Request URI                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **POST** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/carts HTTP/1.1                        |

 

**URI parameter**

Use the following path parameter to identify the customer.

| Name            | Type     | Required | Description                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| **customer-id** | string   | Yes      | A GUID formatted customer-id that identifies the customer.             |

 

**Request headers**

-   See [Partner Center REST headers](headers.md) for more information.

**Request body**

This table describes the [Cart](cart.md) properties in the request body.

| Property              | Type             | Required        | Description                                                                                               |
|-----------------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| id                    | string           | No              | A cart identifier that is supplied upon successful creation of the cart.                                  |
| creationTimeStamp     | DateTime         | No              | The date the cart was created, in date-time format. Applied upon successful creation of the cart.         |
| lastModifiedTimeStamp | DateTime         | No              | The date the cart was last updated, in date-time format. Applied upon successful creation of the cart.    |
| expirationTimeStamp   | DateTime         | No              | The date the cart will expire, in date-time format.  Applied upon successful creation of cart.            |
| lastModifiedUser      | string           | No              | The user who last updated the cart. Applied upon successful creation of cart.                             |
| lineItems             | Array of objects | Yes             | An Array of [CartLineItem](cart.md#cartlineitem) resources.                                             |


This table describes the [CartLineItem](cart.md#cartlineitem) properties in the request body.

| Property             | Type                        | Required     | Description                                                                                        |
|----------------------|-----------------------------|--------------|----------------------------------------------------------------------------------------------------|
| id                   | string                      | No           | A Unique identifier for a cart line item. Applied upon successful creation of cart.                |
| catalogId            | string                      | Yes          | The catalog item identifier.                                                                       |
| friendlyName         | string                      | No           | Optional. The friendly name for the item defined by the partner to help disambiguate.              |
| quantity             | int                         | Yes          | The number of licenses for a license-based subscription or instances for an Azure reservation.     |
| currencyCode         | string                      | No           | The currency code.                                                                                 |
| billingCycle         | Object                      | Yes          | The type of billing cycle set for the current period.                                              |
| participants         | List of Object String pairs | No           | A collection of participants on the purchase.                                                      |
| provisioningContext  | Dictionary<string, string>  | No           | A context used for provisioning of offer.                                                          |
| orderGroup           | string                      | No           | A group to indicate which items can be placed together.                                            |
| error                | Object                      | No           | Applied after cart is created in case of an error.                                                 |


**Request example**

```
POST /v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/carts HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4fa6dad6-a89f-4875-8247-8294a10ae1cf
MS-CorrelationId: 0e93c70c-977a-4a88-9580-7cf084c73286
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Content-Type: application/json
Host: api.partnercenter.microsoft.com 
Content-Length: 496
Expect: 100-continue

{  
   "LineItems": [  
        {  
            "Id":0,
            "CatalogItemId": "DG7GMGF0DWTL:0001:DG7GMGF0DSJB",
            "FriendlyName": "A_sample_Azure_RI",
            "Quantity": 2,
            "BillingCycle": "one_time",
            "ProvisioningContext": {
                "subscriptionId": "3D5ECED6-1151-44C7-AEE6-70A4BB725666",
                "scope": "shared",
                "duration": "1Year"
            }
        }
    ],
    "Attributes": {  
        "ObjectType": "Cart"
    }
}
```

## <span id="Response"></span><span id="response"></span><span id="RESPONSE"></span>REST Response


If successful, this method returns the populated [Cart](cart.md) resource in the response body.

**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Error Codes](error-codes.md).

**Response example**

```
HTTP/1.1 201 Created
Content-Length: 764
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 0e93c70c-977a-4a88-9580-7cf084c73286
MS-RequestId: 4fa6dad6-a89f-4875-8247-8294a10ae1cf
X-Locale: en-US,en-US
MS-CV: sF/wRa2ih0CzbABc.0
MS-ServerId: 000001
Date: Thu, 15 Mar 2018 17:15:01 GMT
{
    "id": "b4c8fdea-cbe4-4d17-9576-13fcacbf9605",
    "creationTimestamp": "2018-03-15T17:15:02.3840528Z",
    "lastModifiedTimestamp": "2018-03-15T17:15:02.3840528Z",
    "lastModifiedUser": "2713ccd7-ea3b-470a-9cfb-451d5d0482cc",
    "lineItems": [
        {
            "id": 0,
            "catalogItemId": "DG7GMGF0DWTL:0001:DG7GMGF0DSJB",
            "friendlyName": "My offer purchase",
            "quantity": 2,
            "currencyCode": "USD",
            "billingCycle": "one_time",
            "provisioningContext": {
                "subscriptionId": "3D5ECED6-1151-44C7-AEE6-70A4BB725666",
                "scope": "shared",
                "duration": "1Year"
            },
            "orderGroup": "0"
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/carts/b4c8fdea-cbe4-4d17-9576-13fcacbf9605",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Cart"
    }
}
```

 

 




