---
title: Create a cart with add-ons
description: How to add an order with add-ons for a customer in a cart.
ms.date: 11/02/18
ms.localizationpriority: medium
---

# Create a cart with add-ons

**Applies To**

-   Partner Center

How to add an order with add-ons for a customer in a cart. For more information about what is currently available to sell, see [CSP agreements, price lists, and offers](https://msdn.microsoft.com/partner-center/csp-documents-and-learning-resources).

## <span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>Prerequisites

-   Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.
-   A customer identifier. If you do not have a customer's ID, you can look up the ID in Partner Center by choosing the customer from the customers list, selecting Account, then saving their Microsoft ID.

## <span id="Examples"></span><span id="examples"><span id="EXAMPLES"></span>Examples

### C# 

To create an order with add-ons for a customer, first instantiate a [**Cart**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.carts.cart) object. Next, create a list of [**CartLineItem**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.carts.cartlineitem) objects, and assign the list to the cart's [**LineItems**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.carts.cart.lineitems) property. Each cart line item contains a list of **AddOnItems**. 

Next, obtain an interface to cart operations by using [**IAggregatePartner**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.iaggregatepartner) to call the [**ICustomerCollection.ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer, and then retrieving the interface from the **Cart** property.

Finally, call the [**Create**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.carts.icartcollection.create) or [**CreateAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.carts.icartcollection.createasync) method to create the cart.

```csharp
// IAggregatePartner partnerOperations;
// string customerId;

var cart = new Cart()
    {
        LineItems = new List<CartLineItem>()
        {
            new CartLineItem()
            {
                Id = 0,
                CatalogItemId = “A_sample_Offer_ID_having_addon”,
                FriendlyName = "Myofferpurchase",
                Quantity = 3,
                BillingCycle = BillingCycleType.Monthly,
                AddonItems = new List<CartLineItem>
                {
                    new CartLineItem
                    {
                        Id = 1,
                        CatalogItemId = “A_sample_addon_item_ID”,
                        BillingCycle = BillingCycleType.Monthly,
                        Quantity = 2,
                    },
                    new CartLineItem
                    {
                        Id = 2,
                        CatalogItemId = “Another_sample_addon_item_ID”,
                        BillingCycle = BillingCycleType.Monthly,
                        Quantity = 3
                    }
                }
            }
        }
    };

var createdCart = partnerOperations.Customers.ById(customerId).Cart.Create(cart);
```

To append an add-on item to an existing base subscription, create a **Cart** with a new **CartLineItem** containing the parent subscription ID in the **ProvisioninContext** property, then call the **Create** or **CreateAsync** method.

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var cart = new Cart()
    {
        LineItems = new List<CartLineItem>()
        {
            new CartLineItem()
            {
                Id = 0,
                CatalogItemId = “A_sample_addon_item_ID”,
                ProvisioningContext = new Dictionary<string, string>
                {
                    {
                        "ParentSubscriptionId", “A_sample_existing_subscription_Id”
                    }
                },
                Quantity = 1,
                BillingCycle = BillingCycleType.Annual,
            }
        }
    };

var createdCart = partnerOperations.Customers.ById(selectedCustomerId).Carts.Create(cart);
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

| Property              | Type             | Required        | Description |
|-----------------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| id                    | string           | No              | A cart identifier that is supplied upon successful creation of the cart.                                  |
| creationTimeStamp     | DateTime         | No              | The date the cart was created, in date-time format. Applied upon successful creation of the cart.         |
| lastModifiedTimeStamp | DateTime         | No              | The date the cart was last updated, in date-time format. Applied upon successful creation of the cart.    |
| expirationTimeStamp   | DateTime         | No              | The date the cart will expire, in date-time format.  Applied upon successful creation of cart.            |
| lastModifiedUser      | string           | No              | The user who last updated the cart. Applied upon successful creation of cart.                             |
| lineItems             | Array of objects | Yes             | An Array of [CartLineItem](cart.md#cartlineitem) resources.                                             |

This table describes the [CartLineItem](cart.md#cartlineitem) properties in the request body.


| Property             | Type                             | Description                                                                                                                                           |
|----------------------|----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| id                   | string                           | A unique identifier for a cart line item. Applied upon successful creation of cart.                                                                   |
| catalogId            | string                           | The catalog item identifier.                                                                                                                          |
| friendlyName         | string                           | Optional. The friendly name for the item defined by the partner to help disambiguate.                                                                 |
| quantity             | int                              | The number of licenses or instances.                                                                                                                  |
| currencyCode         | string                           | The currency code.                                                                                                                                    |
| billingCycle         | Object                           | The type of billing cycle set for the current period.                                                                                                 |
| participants         | List of Object String pairs      | A collection of PartnerId on Record (MPNID) on the purchase.                                                                                          |
| provisioningContext  | Dictionary<string, string>       | A context used for provisioning of offer.                                                                                                             |
| orderGroup           | string                           | A group to indicate which items can be placed together.                                                                                               |
| addonItems           | List of **CartLineItem** objects | A collection of cart line items for addons that will be purchased towards the base subscription that results from the root cart line item's purchase. |
| error                | Object                           | Applied after cart is created in case of an error.                                                                                                    |

**Request example**

The following REST example show how to create a cart with add-on items for a new base subscription.

```http
POST https://api.partnercenter.microsoft.com/v1/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/carts HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: f931348a-6312-47d0-a8dd-31a386dedb8f
MS-CorrelationId: f73baf70-bbc3-43d0-8b29-dffa08ff9511

{
    "Id":null,
    "CreationTimestamp":null,
    "LastModifiedTimestamp":null,
    "ExpirationTimestamp":"0001-01-01T00:00:00",
    "LastModifiedUser":null,
    "LineItems": [
        {
            "Id":0,
            "CatalogItemId":"91FD106F-4B2C-4938-95AC-F54F74E9A239",
            "FriendlyName":"Myofferpurchase",
            "Quantity":3,
            "CurrencyCode":null,
            "BillingCycle":"monthly",
            "Participants":null,
            "ProvisioningContext":null,
            "OrderGroup":null,
            "AddonItems": [
                {
                    "Id":1,
                    "CatalogItemId":"C94271D8-B431-4A25-A3C5-A57737A1C909",
                    "FriendlyName":null,
                    "Quantity":2,
                    "CurrencyCode":null,
                    "BillingCycle":"monthly",
                    "Participants":null,
                    "ProvisioningContext":null,
                    "OrderGroup":null,
                    "AddonItems":null,
                    "Error":null
                },
                {
                    "Id":2,
                    "CatalogItemId":"43FCE491-76D1-4BCC-B709-8A288786DBAE",
                    "FriendlyName":null,
                    "Quantity":3,
                    "CurrencyCode":null,
                    "BillingCycle":"monthly",
                    "Participants":null,
                    "ProvisioningContext":null,
                    "OrderGroup":null,
                    "AddonItems":null,
                    "Error":null
                }
            ],
            "Error":null
        }
    ],
    "Attributes":
    {
        "ObjectType":"Cart"
    }
}
```

### REST Response

If successful, this method returns the populated [Cart](cart.md) resource in the response body.

**Response example**

```http
HTTP/1.1 201 Created
Content-Length: 958
Content-Type: application/json
MS-CorrelationId: f73baf70-bbc3-43d0-8b29-dffa08ff9511
MS-RequestId: f931348a-6312-47d0-a8dd-31a386dedb8f
X-Locale: en-US,en-US
Date: Thu, 01 Nov 2018 22:29:05 GMT

{
	"id":"dbe2f8d4-f21d-43e2-9356-cff6387c4ba1",
	"creationTimestamp":"2018-11-01T22:29:03.6900182Z",
	"lastModifiedTimestamp":"2018-11-01T22:29:03.6900182Z",
	"expirationTimestamp":"2018-11-01T22:44:05.0025799Z",
	"lastModifiedUser":"1824b7fc-2fac-4478-b177-   66823c40ab75",
	"status":"Active",
	"lineItems": [
		{
			"id":0,
			"catalogItemId":"91FD106F-4B2C-4938-95AC-F54F74E9A239",
			"friendlyName":"Myofferpurchase",
			"quantity":3,
			"currencyCode":"USD",
			"billingCycle":"monthly",
			"orderGroup":"OMS-0",
			"addonItems": [
				{
					"id":1,
					"catalogItemId":"C94271D8-B431-4A25-A3C5-A57737A1C909",
					"quantity":2,
					"currencyCode":"USD",
					"billingCycle":"monthly",
					"orderGroup":"OMS-0"
				},
				{
					"id":2,
					"catalogItemId":"43FCE491-76D1-4BCC-B709-8A288786DBAE",
					"quantity":3,
					"currencyCode":"USD",
					"billingCycle":"monthly",
					"orderGroup":"OMS-0"
				}
			]
		}
	],
	"links": {
		"self": {
			"uri":"/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/carts/dbe2f8d4-f21d-43e2-9356-cff6387c4ba1",
			"method":"GET",
			"headers":[
			]
		}
	},
	"attributes": {
		"objectType":"Cart"
	}
}
```

**Request example**

The following REST example show how to append add-ons to an existing base subscription.

```http
POST https://api.partnercenter.microsoft.com/v1/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/carts HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 512a777a-5427-452d-9637-18421387e435
MS-CorrelationId: 182474ba-7303-4d0f-870a-8c7fba5ccc4b

{
    "Id":null,
    "CreationTimestamp":null,
    "LastModifiedTimestamp":null,
    "ExpirationTimestamp":"0001-01-01T00:00:00",
    "LastModifiedUser":null,
    "LineItems": [
        {
            "Id":0,
            "CatalogItemId":"C94271D8-B431-4A25-A3C5-A57737A1C909",
            "FriendlyName":null,
            "Quantity":1,
            "CurrencyCode":null,
            "BillingCycle":"annual",
            "Participants":null,
            "ProvisioningContext":{"ParentSubscriptionId":"97555B61-7461-477A-A98C-9C76148783E4"},
            "OrderGroup":null,
            "AddonItems":null,
            "Error":null
        }
    ],
    "Attributes": {
        "ObjectType":"Cart"
    }
}
```

### REST Response

If successful, this method returns the populated [Cart](cart.md) resource in the response body.

**Response example**

```http
HTTP/1.1 201 Created
Content-Length: 707
Content-Type: application/json
MS-CorrelationId: 182474ba-7303-4d0f-870a-8c7fba5ccc4b
MS-RequestId: 512a777a-5427-452d-9637-18421387e435
X-Locale: en-US,en-US
Date: Thu, 01 Nov 2018 22:46:18 GMT

{
    "id":"4d927e27-93d1-448b-abe5-819b66ecca22",
    "creationTimestamp":"2018-11-01T22:46:16.2996364Z",
    "lastModifiedTimestamp":"2018-11-01T22:46:16.2996364Z",
    "expirationTimestamp":"2018-11-01T23:01:18.7543264Z",
    "lastModifiedUser":"1824b7fc-2fac-4478-b177-66823c40ab75",
    "status":"Active",
    "lineItems": [
        {
            "id":0,
            "catalogItemId":"C94271D8-B431-4A25-A3C5-A57737A1C909",
            "quantity":1,
            "currencyCode":"USD",
            "billingCycle":"annual",
            "provisioningContext": {
                "parentSubscriptionId":"97555B61-7461-477A-A98C-9C76148783E4"
            },
            "orderGroup":"OMS-0"
        }
    ],
    "links": {
        "self": {
            "uri":"/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/carts/4d927e27-93d1-448b-abe5-819b66ecca22",
            "method":"GET",
            "headers":[
            ]
        }
    },
    "attributes": {
        "objectType":"Cart"
    }
}
```

**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Error Codes](error-codes.md).
