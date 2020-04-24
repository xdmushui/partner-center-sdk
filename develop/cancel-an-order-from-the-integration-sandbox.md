---
title: Cancel an order from the integration sandbox
description: Cancel orders from integration sandbox accounts.
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice:  partnercenter-sdk
ms.localizationpriority: medium
---

# Cancel an order from the integration sandbox

**Applies to:**

- Partner Center
- Partner Center operated by 21Vianet
- Partner Center for Microsoft Cloud Germany
- Partner Center for Microsoft Cloud for US Government

How to cancel reserved instance, software, and commercial marketplace Software as a Service (SaaS) subscription orders from integration sandbox accounts.

>[!NOTE]
>Please be aware that the cancellations of reserved instance, software, or commercial marketplace SaaS subscription orders are only possible from integration sandbox accounts. To cancel production orders please contact Partner Center support.

## Prerequisites

- Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.
- An integration sandbox partner account with a customer having active reserved instance / software / third-party SaaS subscription orders.

## C\#

To cancel an order from the integration sandbox, pass your account credentials to the [**`CreatePartnerOperations`**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) method to get an [**`IPartner`**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.ipartner) interface to get partner operations.

To select a particular [Order](order-resources.md#order), use the partner operations and call [**`Customers.ById()`**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier to specify the customer, followed by **`Orders.ById()`** with order identifier to specify the order and finally **`Get`** or **`GetAsync`** method to retrieve it.

Set the [**`Order.Status`**](order-resources.md#order) property to `cancelled` and use the **`Patch()`** method to update the order.

``` csharp
// IPartnerCredentials tipAccountCredentials;
// Customer tenant Id to be deleted.
// string customerTenantId;

IPartner tipAccountPartnerOperations = PartnerService.Instance.CreatePartnerOperations(tipAccountCredentials);

// Cancel order
var order = tipAccountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(orderId).Get();
order.Status = "cancelled";
order = tipAccountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(orderId).Patch(order);

```

## REST request

### Request syntax

| Method     | Request URI                                                                            |
|------------|----------------------------------------------------------------------------------------|
| **PATCH** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{order-id} HTTP/1.1 |

### URI parameter

Use the following query parameter to delete a customer.

| Name                   | Type     | Required | Description                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **customer-tenant-id** | **guid** | Y        | The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller. |
| **order-id** | **string** | Y        | The value is a string denoting the order IDs that need to be canceled. |

### Request headers

For more information, see [Partner Center REST headers](headers.md).

### Request body

```http
{
    "id": "UKXASSO1dezh3HdxClHxSp5UEFXGbAnt1",
    "status": "cancelled",
}
```

### Request example

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/orders/<order-id> HTTP/1.1
Accept: application/json
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd

{
    "id": "UKXASSO1dezh3HdxClHxSp5UEFXGbAnt1",
    "status": "cancelled",
}
```

## REST response

If successful, this method returns the canceled order.

### Response success and error codes

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center REST error codes](error-codes.md).

### Response example

```http
HTTP/1.1 200 OK
Content-Length: 866
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5

{
    "id": "UKXASSO1dezh3HdxClHxSp5UEFXGbAnt1",
    "alternateId": "11fc4bdfd47a",
    "referenceCustomerId": "bd59b416-37f9-4d8f-8df3-5750111fc615",
    "billingCycle": "one_time",
    "currencyCode": "USD",
    "currencySymbol": "$",
    "lineItems": [
        {
            "lineItemNumber": 0,
            "offerId": "DG7GMGF0DWT0:0001:DG7GMGF0DSQR",
            "termDuration": "",
            "transactionType": "New",
            "friendlyName": "Microsoft Identity Manager 2016 - 1 User CAL",
            "quantity": 1,
            "links": {
                "product": {
                    "uri": "/products/DG7GMGF0DWT0?country=US",
                    "method": "GET",
                    "headers": []
                },
                "sku": {
                    "uri": "/products/DG7GMGF0DWT0/skus/0001?country=US",
                    "method": "GET",
                    "headers": []
                },
                "availability": {
                    "uri": "/products/DG7GMGF0DWT0/skus/0001/availabilities/DG7GMGF0DSQR?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "creationDate": "2019-02-21T17:56:21.1335741Z",
    "status": "cancelled",
    "transactionType": "UserPurchase",
    "attributes": {
        "objectType": "Order"
    }
}
```
