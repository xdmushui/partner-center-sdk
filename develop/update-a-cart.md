---
title: Update a cart
description: How to update an order for a customer in a cart.
ms.date: 09/06/2021
ms.service: partner-dashboard
ms.subservice:  partnercenter-sdk
---

# Update a cart

How to update an order for a customer in a cart.

## Prerequisites

- Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.

- A customer ID (`customer-tenant-id`). If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard). Select **CSP** from the Partner Center menu, followed by **Customers**. Select the customer from the customer list, then select **Account**. On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section. The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).

- A Cart ID for an existing cart.

## C\#

To update an order for a customer, get the cart using the **Get()** method by passing the customer and cart IDs using the **ById()** function. Make the necessary changes to the cart. Now call the **Put** method by using customer and cart IDs using the **ById()** method.

Finally, call the **Put()** or **PutAsync()** method to create the order.

``` csharp
IAggregatePartner partnerOperations;
string customerId;
string cartId;

var cart = partnerOperations.Customers.ById(customerId).Cart.ById(cartId).Get();

cart.LineItems.ToArray()[0].Quantity++;

var updatedCart = partnerOperations.Customers.ById(customerId).Cart.ById(cartId).Put(cart);
```

To complete attestation and include additional resellers, see the following sample.

### API Sample - Check out cart

``` csharp
{
    "orders": [
        {
            "id": "f76c6b7f449d",
            "alternateId": "f76c6b7f449d",
            "referenceCustomerId": "f81d98dd-c2f4-499e-a194-5619e260344e",
            "billingCycle": "monthly",
            "currencyCode": "USD",
            "currencySymbol": "$",
            "lineItems": [
                {
                    "lineItemNumber": 0,
                    "offerId": "CFQ7TTC0LH0Z:0001:CFQ7TTC0K18P",
                    "subscriptionId": "ebc0beef-7ffb-4044-c074-16f324432139",
                    "termDuration": "P1M",
                    "transactionType": "New",
                    "friendlyName": "AI Builder Capacity add-on",
                    "quantity": 1,
                    "links": {
                        "product": {
                            "uri": "/products/CFQ7TTC0LH0Z?country=US",
                            "method": "GET",
                            "headers": []
                        },
                        "sku": {
                            "uri": "/products/CFQ7TTC0LH0Z/skus/0001?country=US",
                            "method": "GET",
                            "headers": []
                        },
                        "availability": {
                            "uri": "/products/CFQ7TTC0LH0Z/skus/0001/availabilities/CFQ7TTC0K18P?country=US",
                            "method": "GET",
                            "headers": []
                        }
                    }
                },
                {
                    "lineItemNumber": 1,
                    "offerId": "CFQ7TTC0LFLS:0002:CFQ7TTC0KDLJ",
                    "subscriptionId": "261bac40-7d88-4327-dfa3-dacd09222d62",
                    "termDuration": "P1Y",
                    "transactionType": "New",
                    "friendlyName": "Azure Active Directory Premium P1",
                    "quantity": 2,
                    "partnerIdOnRecord": "517285",
                    "additionalPartnerIdsOnRecord": 
                        "5357564",
                        "5357563"
                    ],
                 
   "links": {
                        "product": {
                            "uri": "/products/CFQ7TTC0LFLS?country=US",
                            "method": "GET",
                            "headers": []
                        },
                        "sku": {
                            "uri": "/products/CFQ7TTC0LFLS/skus/0002?country=US",
                            "method": "GET",
                            "headers": []
                        },
                        "availability": {
                            "uri": "/products/CFQ7TTC0LFLS/skus/0002/availabilities/CFQ7TTC0KDLJ?country=US",
                            "method": "GET",
                            "headers": []
                        }
                    }
                }
            ],
            "creationDate": "2021-08-18T07:52:23.1921872Z",
            "status": "pending",
            "transactionType": "UserPurchase",
            "links": {
                "self": {
                    "uri": "/customers/f81d98dd-c2f4-499e-a194-5619e260344e/orders/f76c6b7f449d",
                    "method": "GET",
                    "headers": []
                },
                "provisioningStatus": {
                    "uri": "/customers/f81d98dd-c2f4-499e-a194-5619e260344e/orders/f76c6b7f449d/provisioningstatus",
                    "method": "GET",
                    "headers": []
                },
                "patchOperation": {
                    "uri": "/customers/f81d98dd-c2f4-499e-a194-5619e260344e/orders/f76c6b7f449d",
                    "method": "PATCH",
                    "headers": []
                }
            },
            "client": {},
            "attributes": {
                "objectType": "Order"
            }
        }
    ],
    "attributes": {
        "objectType": "CartCheckoutResult"
    }
}

```

## REST request

### Request syntax

| Method  | Request URI                                                                                                 |
|---------|-------------------------------------------------------------------------------------------------------------|
| **PUT** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/carts/{cart-id} HTTP/1.1              |

### URI parameters

Use the following path parameters to identify the customer, and specify the cart to be updated.

| Name            | Type     | Required | Description                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| **customer-id** | string   | Yes      | A GUID formatted customer-id that identifies the customer.             |
| **cart-id**     | string   | Yes      | A GUID formatted cart-id that identifies the cart.                     |

### Request headers

For more information, see [Partner Center REST headers](headers.md).

### Request body

This table describes the [Cart](cart-resources.md) properties in the request body.

| Property              | Type             | Required        | Description                                                                                               |
|-----------------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| id                    | string           | No              | A cart identifier that is supplied upon successful creation of the cart.                                  |
| creationTimeStamp     | DateTime         | No              | The date the cart was created, in date-time format. Applied upon successful creation of the cart.        |
| lastModifiedTimeStamp | DateTime         | No              | The date the cart was last updated, in date-time format. Applied upon successful creation of the cart.    |
| expirationTimeStamp   | DateTime         | No              | The date the cart will expire, in date-time format.  Applied upon successful creation of cart.            |
| lastModifiedUser      | string           | No              | The user who last updated the cart. Applied upon successful creation of cart.                             |
| lineItems             | Array of objects | Yes             | An Array of [CartLineItem](cart-resources.md#cartlineitem) resources.                                               |

This table describes the [CartLineItem](cart-resources.md#cartlineitem) properties in the request body.

| Property             | Type                        | Required     | Description                                                                                        |
|----------------------|-----------------------------|--------------|----------------------------------------------------------------------------------------------------|
| id                   | string                      | No           | A Unique identifier for a cart line item. Applied upon successful creation of cart.                |
| catalogId            | string                      | Yes          | The catalog item identifier.                                                                       |
| friendlyName         | string                      | No           | Optional. The friendly name for the item defined by the partner to help disambiguate.              |
| quantity             | int                         | Yes          | The number of licenses or instances.     |
| currencyCode         | string                      | No           | The currency code.                                                                                 |
| billingCycle         | Object                      | Yes          | The type of billing cycle set for the current period.                                              |
| participants         | List of Object String pairs | No           | A collection of participants on the purchase.                                                      |
| provisioningContext  | Dictionary<string, string>  | No           | A context used for provisioning of offer.                                                          |
| orderGroup           | string                      | No           | A group to indicate which items can be placed together.                                            |
| error                | Object                      | No           | Applied after cart is created in case of an error.                                                 |
| AdditionalPartnerIdsOnRecord | String | No | When an indirect provider places an order on behalf of an indirect reseller, populate this field with the MPN ID of the **Additional indirect reseller only** (never the ID of the indirect provider). Incentives are not applicable for these additional resellers. Only a maximum of 5 Indirect Resellers can be entered. This is only applicable partners transacting within EU / EFTA countries.  |

### Request example

```http
PUT /v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/carts/65faf57b-0205-47ee-92b3-08dcf233ea73/ HTTP/1.1
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
    {
        "Id":"b4c8fdea-cbe4-4d17-9576-13fcacbf9605",
        "CreationTimestamp":"2018-03-15T17:15:02.3840528Z",
        "LastModifiedTimestamp":"2018-03-15T17:15:02.3840528Z",
        "ExpirationTimestamp":"0001-01-01T00:00:00",
        "LastModifiedUser":"2713ccd7-ea3b-470a-9cfb-451d5d0482cc",
        "LineItems":[
            {
                "Id":0,
                "CatalogItemId":"DG7GMGF0DWTL:0001:DG7GMGF0DSJB",
                "FriendlyName":"A_sample_Azure_RI",
                "Quantity":2,
                "BillingCycle":"one_time",
                "ProvisioningContext": {
                    "SubscriptionId": "3D5ECED6-1151-44C7-AEE6-70A4BB725666",
                    "Scope": "shared",
                    "Duration": "1Year"
                }
            }
        ],
    }
}
```

## REST response

If successful, this method returns the populated [Cart](cart-resources.md) resource in the response body.

### Response success and error codes

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Error Codes](error-codes.md).

### Response example

```http
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
            "friendlyName": "A_sample_Azure_RI",
            "quantity": 2,
            "currencyCode": "USD",
            "billingCycle": "one_time",
            "ProvisioningContext": {
                "subscriptionId": "3D5ECED6-1151-44C7-AEE6-70A4BB725666",
                "scope": "shared",
                "duration": "1Year"
            }
            "orderGroup": "0"
        }
    ],
    "links": {
        "self": {
            "uri": "/v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/carts/b4c8fdea-cbe4-4d17-9576-13fcacbf9605/",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Cart"
    }
}
```
