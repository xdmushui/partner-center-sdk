---
title: Create an order
description: How to create an order for a customer.
MSHAttr:
- 'PreferredSiteName:MSDN'
- 'PreferredLib:/library/PartnerCenter'
ms.assetid: FE4949FA-7C4D-462D-8F32-FAADCF166875
---

# Create an order


**Applies To**

-   Partner Center
-   Partner Center operated by 21Vianet
-   Partner Center for Microsoft Cloud Germany
-   Partner Center for Microsoft Cloud for US Government

How to create an order for a customer. For more information about what is currently available to sell, see [CSP agreements, price lists, and offers](pc_cloud_sltn_provider.csp_documents_and_learning_resources).

## <span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>Prerequisites


-   Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.
-   A customer identifier.
-   An offer identifier.

## <span id="C_"></span><span id="c_"></span>C#


To create an order for a customer, first instantiate an [**Order**](pc_sdk_models_orders.order) object and set the [**ReferenceCustomerID**](pc_sdk_models_orders.order_referencecustomerid) property to the customer ID to record the customer. Next, create a list of [**OrderLineItem**](pc_sdk_models_orders.orderlineitem) objects, and assign the list to the order's [**LineItems**](pc_sdk_models_orders.order_lineitems) property. Each order line item contains the purchase information for one offer. You must have at least one order line item.

Next, obtain an interface to order operations by calling the [**IAggregatePartner.Customers.ById**](pc_sdk_cust.icustomercollection_byid) method with the customer ID to identify the customer, and then retrieving the interface from the [**Orders**](pc_sdk_cust.icustomer_orders) property.

Finally, call the [**Create**](pc_sdk_orders.iordercollection_create) or [**CreateAsync**](pc_sdk_orders.iordercollection_createasync) method to create the order.

```
IAggregatePartner partnerOperations;
string customerId;
string offerId;

var order = new Order()
{
    ReferenceCustomerId = customerId,
    LineItems = new List<OrderLineItem>()
    {
        new OrderLineItem()
        {
            OfferId = offerId,
            FriendlyName = "new offer purchase",
            Quantity = 5
        }
    }
};

var createdOrder = partnerOperations.Customers.ById(customerId).Orders.Create(order);
```

**Sample**: [Console test app](console-test-app.md). **Project**: Partner Center SDK Samples **Class**: CreateOrder.cs

## <span id="Request"></span><span id="request"></span><span id="REQUEST"></span>Request


**Request syntax**

| Method   | Request URI                                                                            |
|----------|----------------------------------------------------------------------------------------|
| **POST** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/orders HTTP/1.1 |

 

**URI parameters**

Use the following path parameter to identify the customer.

| Name        | Type | Required | Description                                                |
|-------------|------|----------|------------------------------------------------------------|
| customer-id | guid | Yes      | A GUID formatted customer-id that identifies the customer. |

 

**Request headers**

-   See [Partner Center REST headers](headers.md) for more information.

**Request body**

This table describes the **Order** properties in the request body.

## <span id="Order"></span><span id="order"></span><span id="ORDER"></span>Order


<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>Name</th>
<th>Type</th>
<th>Required</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>id</td>
<td>string</td>
<td>No</td>
<td>An order identifier that is supplied upon successful creation of the order.</td>
</tr>
<tr class="even">
<td>referenceCustomerId</td>
<td>string</td>
<td>Yes</td>
<td>The customer identifier.</td>
</tr>
<tr class="odd">
<td>billingCycle</td>
<td>string</td>
<td>No</td>
<td>The frequency with which the partner is billed for this order. The default is &quot;Monthly&quot; and is applied upon successful creation of the order. Supported values are the member names found in [<strong>BillingCycleType</strong>](pc_sdk_models_offers.billingcycletype).
<div class="alert">
<strong>Note</strong>  The annual billing feature is not yet generally available. Support for annual billing is coming soon.
</div>
<div>
 
</div></td>
</tr>
<tr class="even">
<td>lineItems</td>
<td>array of objects</td>
<td>Yes</td>
<td>An array of [OrderLineItem](#orderlineitem) resources.</td>
</tr>
<tr class="odd">
<td>creationDate</td>
<td>string</td>
<td>No</td>
<td>The date the order was created, in date-time format. Applied upon successful creation of the order.</td>
</tr>
<tr class="even">
<td>attributes</td>
<td>object</td>
<td>No</td>
<td>Contains &quot;ObjectType&quot;: &quot;Order&quot;.</td>
</tr>
</tbody>
</table>

 

This table describes the **OrderLineItem** properties in the request body.

**Note**  The partnerIdOnRecord should only be provided when an indirect provider places an order on behalf of an indirect reseller. It's used to store the Microsoft Partner Network ID of the indirect reseller only (never the ID of the indirect provider).

 

## <span id="orderLineItem"></span><span id="orderlineitem"></span><span id="ORDERLINEITEM"></span>OrderLineItem


| Name                 | Type   | Required | Description                                                                                                                                                                                                                                |
|----------------------|--------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| lineItemNumber       | int    | Yes      | Each line item in the collection gets a unique line number, counting up from 0 to count-1.                                                                                                                                                 |
| offerId              | string | Yes      | The offer identifier.                                                                                                                                                                                                                      |
| subscriptionId       | string | No       | The subscription identifier.                                                                                                                                                                                                               |
| parentSubscriptionId | string | No       | Optional. The ID of the parent subscription in an add-on offer. Applies to PATCH only.                                                                                                                                                     |
| friendlyName         | string | No       | Optional. The friendly name for the subscription defined by the partner to help disambiguate.                                                                                                                                              |
| quantity             | int    | Yes      | The number of licenses for a license-based subscription.                                                                                                                                                                                   |
| partnerIdOnRecord    | string | No       | When an indirect provider places an order on behalf of an indirect reseller, populate this field with the MPN ID of the **indirect reseller only** (never the ID of the indirect provider). This ensures proper accounting for incentives. |
| attributes           | object | No       | Contains "ObjectType":"OrderLineItem".                                                                                                                                                                                                     |

 

**Request example**

```
POST https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/orders HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 57870501-203b-468e-8a63-078a3826d8ec
MS-CorrelationId: 9c272436-538d-4dd4-a421-c811e004784c
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 405
Expect: 100-continue
Connection: Keep-Alive

{
    "Id": null,
    "ReferenceCustomerId": "4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04",
    "BillingCycle": "unknown",
    "LineItems": [{
            "LineItemNumber": 0,
            "OfferId": "84A03D81-6B37-4D66-8D4A-FAEA24541538",
            "SubscriptionId": null,
            "ParentSubscriptionId": null,
            "FriendlyName": "new offer purchase",
            "Quantity": 5,
            "PartnerIdOnRecord": null,
            "Attributes": {
                "ObjectType": "OrderLineItem"
            }
        }
    ],
    "CreationDate": null,
    "Attributes": {
        "ObjectType": "Order"
    }
}
```

## <span id="Response"></span><span id="response"></span><span id="RESPONSE"></span>Response


If successful, the response body contains the populated [Order](orders.md) resource

**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center error codes](error-codes.md).

**Response example**

```
HTTP/1.1 201 Created
Content-Length: 801
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9c272436-538d-4dd4-a421-c811e004784c
MS-RequestId: 57870501-203b-468e-8a63-078a3826d8ec
MS-CV: VcfS+fqdQUW8Nap6.0
MS-ServerId: 030020525
Date: Thu, 30 Mar 2017 17:43:08 GMT

﻿ {
    "id": "074bd849-9106-405c-9923-fa061839d487",
    "referenceCustomerId": "4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04",
    "billingCycle": "monthly",
    "lineItems": [{
            "lineItemNumber": 0,
            "offerId": "84A03D81-6B37-4D66-8D4A-FAEA24541538",
            "subscriptionId": "1DA3295E-C59A-476C-A7E7-D7E981FE79BE",
            "friendlyName": "new offer purchase",
            "quantity": 5,
            "links": {
                "subscription": {
                    "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/subscriptions/1DA3295E-C59A-476C-A7E7-D7E981FE79BE",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "creationDate": "2017-03-30T10:43:07.157-07:00",
    "links": {
        "self": {
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/orders/074bd849-9106-405c-9923-fa061839d487",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "etag": "eyJpZCI6IjA3NGJkODQ5LTkxMDYtNDA1Yy05OTIzLWZhMDYxODM5ZDQ4NyIsInZlcnNpb24iOjF9",
        "objectType": "Order"
    }
}
```

 

 




