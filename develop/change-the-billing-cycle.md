---
title: Change the billing cycle
description: Updates a subscription from monthly to annual billing or from annual to monthly billing.
ms.date: 11/14/2018
ms.localizationpriority: medium
---

# Change the billing cycle

**Applies To**

- Partner Center
- Partner Center operated by 21Vianet
- Partner Center for Microsoft Cloud Germany
- Partner Center for Microsoft Cloud for US Government

Updates an [Order](orders.md) from monthly to annual billing or from annual to monthly billing.

In the Partner Center dashboard, this operation can be performed by navigating to a customer's subscription details page. Once there, you will see an option defining the current billing cycle for the subscription with the ability to change and submit it.  

**Out of Scope**  

- Changing the billing cycle for trials
- Changing the billing cycles for any non-annual term offers (monthly, 6-year) & Azure subscriptions
- Changing the billing cycles for inactive subscriptions
- Changing billing cycles for Microsoft online services license-based subscriptions

## <span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>Prerequisites

- Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.
- A customer ID (customer-tenant-id). If you do not have a customer's ID, you can look up the ID in Partner Center by choosing the customer from the customers list, selecting Account, then saving their Microsoft ID.
- An order ID.

## <span id="C_"/><span id="c_"/>C#

To change the frequency of the billing cycle, update the [**Order.BillingCycle**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.orders.order.billingcycle?view=partnercenter-dotnet-latest#Microsoft_Store_PartnerCenter_Models_Orders_Order_BillingCycle) property.

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string offerId;
// string orderId; 

var order = new Order()
{
    ReferenceCustomerId = customerId,
    BillingCycle = BillingCycleType.Annual,
    LineItems = new List<OrderLineItem>()
    {
        new OrderLineItem()
        {
            LineItemNumber = 0,
            OfferId = offerId,
            SubscriptionId = null,
            ParentSubscriptionId = "1C2B75C1-74A5-472A-A729-7F8CEFC477F9",
            Quantity = 1
        }
    }
};

var createdOrder = partnerOperations.Customers.ById(customerId).Orders.ById(orderId).Patch(order);
```

## <span id="REST_Request"/><span id="rest_request"/><span id="REST_REQUEST"/>REST Request

**Request syntax**

| Method    | Request URI                                                                                             |
|-----------|---------------------------------------------------------------------------------------------------------|
| **PATCH** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{order-id} HTTP/1.1 |

**URI parameter**

This table lists the required query parameter to change the quantity of the subscription.

| Name                   | Type | Required | Description                                                          |  
|------------------------|------|----------|----------------------------------------------------------------------|  
| **customer-tenant-id** | GUID |    Y     | A GUID formatted **customer-tenant-id** that identifies the customer |  
| **order-id**           | GUID |    Y     | The order identifier                                                 |  

**Request headers**

- See [Headers](headers.md) for more information.

**Request body**

The following tables describe the properties in the request body.

## <span id="order"/><span id="ORDER"/>Order

| Property           | Type             | Required | Description                                                                |
|--------------------|------------------|----------|----------------------------------------------------------------------------|
| Id                 | string           |    N     | An order identifier that is supplied upon successful creation of the order |
|ReferenceCustomerId | string           |    Y     | The customer identifier                                                    |
| BillingCycle       | string           |    Y     | Indicates the frequency with which the partner is billed for this order. Supported values are the member names found in [BillingCycleType](products.md#billingcycletype). |
| LineItems          | array of objects |    Y     | An array of [OrderLineItem](#orderlineitem) resources                      |
| CreationDate       | datetime         |    N     | The date the order was created, in date-time format                        |
| Attributes         | Object           |    N     | Contains "ObjectType": "OrderLineItem"                                     |

## <span id="orderLineItem"/><span id="orderlineitem"/><span id="ORDERLINEITEM"/>OrderLineItem

| Property             | Type   | Required | Description                                                                        |
|----------------------|--------|----------|------------------------------------------------------------------------------------|
| LineItemNumber       | number |    Y     | The line item number, starting with 0                                              |
| OfferId              | string |    Y     | The ID of the offer                                                                |
| SubscriptionId       | string |    N     | The ID of the subscription                                                         |
| ParentSubscriptionId | string |    Y     | The ID of the parent subscription in an add-on offer. Applies to PATCH only        |
| FriendlyName         | string |    N     | The friendly name for the subscription defined by the partner to help disambiguate |
| Quantity             | number |    Y     | The number of licenses or instances                                                |
| PartnerIdOnRecord    | string |    N     | The MPN ID of the partner of record                                                |
| Attributes           | Object |    N     | Contains "ObjectType": "OrderLineItem"                                             |

**Request example**

Update to annual billing

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/orders/CF3B0E37-BE0B-4CDD-B584-D1A97D98A922 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 17a2658e-d2cc-439b-a2f0-2aefd9344fbc
MS-CorrelationId: 60efdd24-17ef-4080-9b02-4fc315f916ff
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 414
Expect: 100-continue

{
    "Id": null,
    "ReferenceCustomerId": "4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04",
    "BillingCycle" : "Annual",
    "LineItems": [{
            "LineItemNumber": 0,
            "OfferId": "2828BE95-46BA-4F91-B2FD-0BEF192ECF60",
            "SubscriptionId": null,
            "ParentSubscriptionId": "1C2B75C1-74A5-472A-A729-7F8CEFC477F9",
            "FriendlyName": "Some friendly name",
            "Quantity": 2,
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

## <span id="REST_Response"/><span id="rest_response"/><span id="REST_RESPONSE"/>REST Response

If successful, this method returns the updated subscription order in the response body.

**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Error Codes](error-codes.md).

**Response example**

```http
HTTP/1.1 200 OK
Content-Length: 1135
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 60efdd24-17ef-4080-9b02-4fc315f916ff
MS-RequestId: 17a2658e-d2cc-439b-a2f0-2aefd9344fbc
MS-CV: WtFy3zI8V0u2lnT9.0
MS-ServerId: 020021921
Date: Wed, 25 Jan 2017 23:01:08 GMT

{
    "id": "cf3b0e37-be0b-4cdd-b584-d1a97d98a922",
    "referenceCustomerId": "4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04",
    "billingCycle": "Annual",
    "lineItems": [{
            "lineItemNumber": 0,
            "offerId": "195416C1-3447-423A-B37B-EE59A99A19C4",
            "subscriptionId": "1C2B75C1-74A5-472A-A729-7F8CEFC477F9",
            "friendlyName": "new offer purchase",
            "quantity": 5,
            "links": {
                "subscription": {
                    "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/subscriptions/1C2B75C1-74A5-472A-A729-7F8CEFC477F9",
                    "method": "GET",
                    "headers": []
                }
            }
        },
        {
            "lineItemNumber": 1,
            "offerId": "2828BE95-46BA-4F91-B2FD-0BEF192ECF60",
            "subscriptionId": "968BA1CF-C146-4ADF-A300-308DCF718EEE",
            "friendlyName": "Some friendly name",
            "quantity": 2,
            "links": {
                "subscription": {
                    "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/subscriptions/968BA1CF-C146-4ADF-A300-308DCF718EEE",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "creationDate": "2017-01-25T14:53:12.093-08:00",
    "links": {
        "self": {
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/orders/cf3b0e37-be0b-4cdd-b584-d1a97d98a922",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "etag": "eyJpZCI6ImNmM2IwZTM3LWJlMGItNGNkZC1iNTg0LWQxYTk3ZDk4YTkyMiIsInZlcnNpb24iOjJ9",
        "objectType": "Order"
    }
}
```