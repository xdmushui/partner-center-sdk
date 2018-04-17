---
title: Checkout a cart
description: How to checkout an order for a customer in a cart.
ms.assetid: 
ms.author: v-thpr
ms.date: 03/19/18
ms.topic: article
ms.prod: partner-center
ms.technology: partner-center-sdk
---

# Checkout a cart

[This information relates to pre-released product which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.] 

**Applies To**

-   Partner Center


How to checkout an order for a customer in a cart. 

## <span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>Prerequisites


-   Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.
-   A customer identifier. If you do not have a customer's ID, you can look up the ID in Partner Center by choosing the customer from the customers list, selecting Account, then saving their Microsoft ID.
-   A Cart ID for an existing cart.


## <span id="C_"></span><span id="c_"></span>C#


To Checkout an order for a customer, get the cart using the **Get()** method by passing the customer and cart ID’s using the **ById()** function. 

Finally, call the **Create** or **CreateAsync()** method to create the order.


```CSharp
IAggregatePartner partnerOperations;
string customerId;
string cartId;

var cart = partnerOperations.Customers.ById(customerId).Cart.ById(cartId).Checkout();
```

## <span id="REST_Request"></span><span id="rest_request"></span><span id="REST_REQUEST"></span>REST Request


**Request syntax**

| Method   | Request URI                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **POST** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/carts/{cart-id}/checkout HTTP/1.1              |

 

**URI parameters**

Use the following path parameters to identify the customer and specify the cart to be checked out.

| Name            | Type     | Required | Description                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| **customer-id** | string   | Yes      | A GUID formatted customer-id that identifies the customer.             |
| **cart-id**     | string   | Yes      | A GUID formatted cart-id that identifies the cart.                     |

 

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
| lineItems             | Array of objects | Yes             | An Array of [CartLineItem](cart.md#cartlineitem) resources.                                               |


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
POST /v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/carts/65faf57b-0205-47ee-92b3-08dcf233ea73/checkout HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4fa6dad6-a89f-4875-8247-8294a10ae1cf
MS-CorrelationId: 0e93c70c-977a-4a88-9580-7cf084c73286
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Content-Type: application/json
Host: api.partnercenter.microsoft-ppe.com
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
                "FriendlyName":"My offer purchase",
                "Quantity":3,
                "CurrencyCode":"USD",
                "BillingCycle":"one_time",
                "Participants":null,
                "ProvisioningContext":null,
                "OrderGroup":"0",
                "PurchaseSystem":null,
                "AudienceClaimHeader":null,
                "TargetId":null,
                "Error":null
            }
        ],
        "Links":{  
            "Self":{  
                "Uri":"/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/carts/b4c8fdea-cbe4-4d17-9576-13fcacbf9605",
                "Method":"GET",
                "Headers":[]
            }
        },
        "Attributes":{  
            "ObjectType":"Cart"
        }
    }
}
```

## <span id="Response"></span><span id="response"></span><span id="RESPONSE"></span>REST Response


If successful, the response body contains the populated **CartCheckoutResult** resource.

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
    "orders":[  
        {  
            "id":"VulAvcXKPvZqsyAAaahiT7Ii0QEJuReH1",
            "referenceCustomerId":"d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d",
            "billingCycle":"one_time",
            "currencyCode":"USD",
            "lineItems":[  
                {  
                    "lineItemNumber":0,
                    "offerId":"DG7GMGF0DWTL:0001:DG7GMGF0DSJB",
                    "friendlyName":"Office Professional Plus 2016My offer purchase",
                    "quantity":2,
                    "links":{  
                    "sku":{  
                            "uri":"/products/DG7GMGF0DWTL/skus/0001?country=US",
                            "method":"GET",
                            "headers":[]
                        }
                    }
                }
            ],
            "creationDate":"2018-03-15T17:10:51.2712905Z",
            "status":"completed",
            "links":{  
                "provisioningStatus":{  
                    "uri":"/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/orders/VulAvcXKPvZqsyAAaahiT7Ii0QEJuReH1/provisioningstatus",
                    "method":"GET",
                    "headers":[]
                },
                "self":{  
                    "uri":"/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/orders/VulAvcXKPvZqsyAAaahiT7Ii0QEJuReH1",
                    "method":"GET",
                    "headers":[]
                }
            },
            "attributes":{  
                "objectType":"Order"
            }
        }
    ],
    "attributes":{  
        "objectType":"CartCheckoutResult"
    }
}
```

 

 




