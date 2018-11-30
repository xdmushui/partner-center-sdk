---
title: Create an order
description: How to create an order for a customer.
ms.assetid: FE4949FA-7C4D-462D-8F32-FAADCF166875
ms.date: 11/29/2018
ms.localizationpriority: medium
---

# Create an order


**Applies To**

-   Partner Center
-   Partner Center operated by 21Vianet
-   Partner Center for Microsoft Cloud for US Government

**Creating an Order for Azure Reserved VM Instance products applies only to**

-   Partner Center

How to create an order for a customer. For more information about what is currently available to sell, see [CSP agreements, price lists, and offers](https://msdn.microsoft.com/partner-center/csp-documents-and-learning-resources).

## <span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>Prerequisites


-   Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.
-   A customer identifier.
-   An offer identifier.

## <span id="C_"></span><span id="c_"></span>C#


To create an order for a customer, first instantiate an [**Order**](orders.md) object and set the **ReferenceCustomerID** property to the customer ID to record the customer. Next, create a list of [**OrderLineItem**](orders.md#orderlineitem) objects, and assign the list to the order's **LineItems** property. Each order line item contains the purchase information for one offer. You must have at least one order line item.

Next, obtain an interface to order operations by calling the [**IAggregatePartner.Customers.ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer, and then retrieving the interface from the [**Orders**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) property.

Finally, call the [**Create**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.create) or [**CreateAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.createasync) method and pass in the [**Order**](orders.md) object.

``` csharp
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
            Quantity = 1,
            ProvisioningContext = new Dictionary<string, string>
            {
                { "subscriptionId", "5198C069-3DAA-403A-8660-5BE11BFD12EE" },
                { "scope", "shared" },
                { "duration", "3Years" }            
            }	
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

| Name        | Type   | Required | Description                                                |
|-------------|--------|----------|------------------------------------------------------------|
| customer-id | string | Yes      | A GUID formatted customer-id that identifies the customer. |

 

**Request headers**

-   See [Partner Center REST headers](headers.md) for more information.

**Request body**

This table describes the [Order](orders.md) properties in the request body.

## <span id="Order"></span><span id="order"></span><span id="ORDER"></span>Order


| Property             | Type                        | Required                        | Description                                                                   |
|----------------------|-----------------------------|---------------------------------|-------------------------------------------------------------------------------|
| id                   | string                      | No                              | An order identifier that is supplied upon successful creation of the order.   |
| referenceCustomerId  | string                      | No                              | The customer identifier. |
| billingCycle         | string                      | No                              | Indicates the frequency with which the partner is billed for this order. Supported values are the member names found in [BillingCycleType](products.md#billingcycletype). The default is "Monthly" or "OneTime" at order creation. This field is applied upon successful creation of the order. |
| lineItems            | array of [OrderLineItem](orders.md#orderlineitem) resources | Yes      | An itemized list of the offers the customer is purchasing including the quantity.        |
| currencyCode         | string                      | No                              | Read-only. The currency used when placing the order. Applied upon successful creation of the order.           |
| creationDate         | datetime                    | No                              | Read-only. The date the order was created, in date-time format. Applied upon successful creation of the order.                                   |
| status               | string                      | No                              | Read-only. The status of the order.  Supported values are the member names found in [OrderStatus](orders.md#orderstatus).        |
| links                | [OrderLinks](utility-resources.md#resourcelinks)              | No                              | The resource links corresponding to the Order. |
| attributes           | [ResourceAttributes](utility-resources.md#resourceattributes) | No                              | The metadata attributes corresponding to the Order. | 



This table describes the [OrderLineItem](orders.md#orderlineitem) properties in the request body.

>[!NOTE]
>The partnerIdOnRecord should only be provided when an indirect provider places an order on behalf of an indirect reseller. It's used to store the Microsoft Partner Network ID of the indirect reseller only (never the ID of the indirect provider).

 

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
| provisioningContext  | Dictionary<string, string>                | No       |  Information required for provisioning for some items in the catalog. The provisioningVariables property in a SKU indicates which properties are required for specific items in the catalog.                  |
| links                | [OrderLineItemLinks](orders.md#orderlineitemlinks) | No       |  Read-only. The resource links corresponding to the Order line item.  |
| attributes           | [ResourceAttributes](utility-resources.md#resourceattributes) | No       | The metadata attributes corresponding to the OrderLineItem. | 
 

**Request example**

```http
POST https://api.partnercenter.microsoft.com/v1/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders HTTP/1.1
Authorization: Bearer <token>
Host: api.partnercenter.microsoft.com
Content-Length: 691
Content-Type: application/json

{
  "BillingCycle": "one_time",
  "CurrencyCode": "USD",
  "LineItems": [
    {
      "LineItemNumber": 0,
      "ProvisioningContext": {
        "subscriptionId": "3D5ECED6-1151-44C7-AEE6-70A4BB725666",
        "scope": "shared",
        "duration": "1Year"
      },
      "OfferId": "DZH318Z0BQ4B:0047:DZH318Z0DSM8",
      "FriendlyName": "A_sample_Azure_RI",
      "Quantity": 1
    }
  ]
}
```

## <span id="Response"></span><span id="response"></span><span id="RESPONSE"></span>Response


If successful, the method returns an [Order](orders.md) resource in the response body.

**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center error codes](error-codes.md).

This method returns the following error codes:

| HTTP Status Code     | Error code   | Description                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| 400                  | 2093         | Inventory is not available for the catalog item selected.                                                 |
| 400                  | 2094         | Subscription is not a valid Azure subscription. Only applicable for Azure Reserved VM Instance purchase.     |
| 400                  | 2095         | Subscription is not enabled for an Azure Reserved VM Instance purchase.                                                                                                

**Response example**

```http
HTTP/1.1 201 Created
Content-Length: 788
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b593cbb7-b358-4b31-81fc-e60b9c277a7f
MS-RequestId: 025f4c19-217f-49d6-a056-391902c62fb3
Date: Thu, 15 Mar 2018 22:30:02 GMT

{
  "id": "Cs_jyTxubLpvdJXdo8xcQZN6I2RsLrgZ1",
  "referenceCustomerId": "b0d70a69-4c42-4b27-b17b-91a835d8686a",
  "billingCycle": "one_time",
  "currencyCode": "USD",
  "lineItems": [
    {
        "lineItemNumber": 0,
        "offerId": "84A03D81-6B37-4D66-8D4A-FAEA24541538",
        "friendlyName": "A_sample_Azure_RI",
        "quantity": 1,
        "links": {
            "sku": {
                "uri": "/products/DZH318Z0BQ4B/skus/0047?country=US",
                "method": "GET",
                "headers": []
            }
        }
    ],
    "creationDate": "2018-03-15T22:30:02.085152Z",
    "status": "pending",
    "links": {
        "provisioningStatus": {
            "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/Cs_jyTxubLpvdJXdo8xcQZN6I2RsLrgZ1/provisioningstatus",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/Cs_jyTxubLpvdJXdo8xcQZN6I2RsLrgZ1",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Order"
    }
}
```

 

 




