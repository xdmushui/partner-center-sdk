---
title: Get an order by ID
description: Gets a Order resource that matches the customer and order ID.
ms.assetid: 5E4160AB-6B73-4CA1-903D-7257927CA754
ms.author: v-thpr
ms.date: 12/15/2017
ms.topic: article
ms.prod: partner-center
ms.technology: partner-center-sdk
---

# Get an order by ID


**Applies To**

-   Partner Center
-   Partner Center operated by 21Vianet
-   Partner Center for Microsoft Cloud Germany
-   Partner Center for Microsoft Cloud for US Government

Gets a [Order](orders.md) resource that matches the customer and order ID.

## <span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>Prerequisites


-   Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.
-   A customer ID (customer-tenant-id). If you do not have a customer's ID, you can look up the ID in Partner Center by choosing the customer from the customers list, selecting Account, then saving their Microsoft ID.
-   An order ID.

## <span id="C_"></span><span id="c_"></span>C#


To get a customer's order by ID, use your **IAggregatePartner.Customers** collection and call the **ById()** method. Then call the [**Orders**](https://review.docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomeroperations.orders) property, followed by the [**ByID()**](https://review.docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.orders.iordercollectionoperations.byid) method once more. Finish by calling [**Get()**](https://review.docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitygetoperations.get) or [**GetAsync()**](https://review.docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitygetoperations.getasync).

```CSharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string selectedOrderId;

var order = partnerOperations.Customers.ById(selectedCustomerId).Orders.ById(selectedOrder.Id).Get();
```

**Sample**: [Console test app](console-test-app.md). **Project**: PartnerSDK.FeatureSample **Class**: GetOrder.cs

## <span id="REST_Request"></span><span id="rest_request"></span><span id="REST_REQUEST"></span>REST Request


**Request syntax**

| Method  | Request URI                                                                                                  |
|---------|--------------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{id-for-order} HTTP/1.1 |

 

**URI parameter**

This table lists the required query parameter to get an order by ID.

| Name                   | Type     | Required | Description                           |
|------------------------|----------|----------|---------------------------------------|
| **customer-tenant-id** | **guid** | Y        | A GUID corresponding to the customer. |
| **id-for-order**       | **guid** | Y        | A GUID corresponding to the order.    |

 

**Request headers**

-   See [Headers](headers.md) for more information.

**Request body**

None.

**Request example**

```
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/orders/<id-for-order> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 0e5fc923-8e3c-4560-9100-ce7283c3e081
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
Connection: Keep-Alive
```

## <span id="Response"></span><span id="response"></span><span id="RESPONSE"></span>Response


If successful, this method returns a [Order](orders.md) resource in the response body.

**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Error Codes](error-codes.md).

**Response example**

```
HTTP/1.1 200 OK
Content-Length: 1252
Content-Type: application/json
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
MS-RequestId: 0e5fc923-8e3c-4560-9100-ce7283c3e081
Date: Mon, 23 Nov 2015 22:02:59 GMT

{
    "id": "d6595733-265f-4918-a62e-026e64bc8384",
    "referenceCustomerId": "<customer-tenant-id>",
    "lineItems": [{
        "lineItemNumber": 0,
        "offerId": "031C9E47-4802-4248-838E-778FB1D2CC05",
        "friendlyName": "nickname",
        "quantity": 1,
        "links": {
            "subscription": {
                "uri": "/subscriptions?key=<key>",
                "method": "GET",
                "headers": []
            }
        }
    }],
    "status": "none",
    "creationDate": "2015-10-08T10:42:36.54-07:00",
    "attributes": {
        "etag": "<etag>",
        "objectType": "Order"
    }
}
```

 

 




