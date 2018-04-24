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

>[!IMPORTANT]   
>This information relates to pre-released product which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here. 

**Applies To**

-   Partner Center
-   Partner Center operated by 21Vianet
-   Partner Center for Microsoft Cloud Germany
-   Partner Center for Microsoft Cloud for US Government

Gets an [Order](orders.md) resource that matches the customer and order ID.

## <span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>Prerequisites


-   Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.
-   A customer ID (customer-tenant-id). If you do not have a customer's ID, you can look up the ID in Partner Center by choosing the customer from the customers list, selecting Account, then saving their Microsoft ID.
-   An order ID.

## <span id="C_"></span><span id="c_"></span>C#


To get a customer's order by ID, use your **IAggregatePartner.Customers** collection and call the **ById()** method. Then call the [**Orders**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) property, followed by the [**ByID()**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid) method once more. Finish by calling [**Get()**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.orders.iorder.get) or [**GetAsync()**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.orders.iorder.getasync).

```CSharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string selectedOrderId;

var order = partnerOperations.Customers.ById(selectedCustomerId).Orders.ById(selectedOrderId).Get();
```

**Sample**: [Console test app](console-test-app.md). **Project**: PartnerSDK.FeatureSample **Class**: GetOrder.cs

## <span id="REST_Request"></span><span id="rest_request"></span><span id="REST_REQUEST"></span>REST Request


**Request syntax**

| Method  | Request URI                                                                                                  |
|---------|--------------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{id-for-order} HTTP/1.1  |

 

**URI parameter**

This table lists the required query parameters to get an order by ID.

| Name                   | Type     | Required | Description                                            |
|------------------------|----------|----------|--------------------------------------------------------|
| customer-tenant-id     | string   | Yes      | A GUID formatted string corresponding to the customer. |
| id-for-order           | string   | Yes      | A string corresponding to the order ID.                |

 

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


If successful, this method returns an [Order](orders.md) resource in the response body.

**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Error Codes](error-codes.md).

**Response example**

```
HTTP/1.1 200 OK
Content-Length: 823
Content-Type: application/json
MS-RequestId: 0e5fc923-8e3c-4560-9100-ce7283c3e081
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
Date: Thu, 15 Mar 2018 22:05:30 GMT

{
    "id": "YxH1q4KScfvfkJQjgRI8QY1DznnUWZTH1",
    "referenceCustomerId": "b0d70a69-4c42-4b27-b17b-91a835d8686a",
    "billingCycle": "one_time",
    "currencyCode": "USD",
    "lineItems": [
    {
        "lineItemNumber": 0,
        "offerId": "DZH318Z0BQ4Z:002L:DZH318Z0CMNP",
        "friendlyName": "Reserved_VM_Instance_Standard_NC12_AU_East_1_Year",
        "quantity": 1,
        "links": {
            "sku": {
                "uri": "/products/DZH318Z0BQ4Z/skus/002L?country=US",
                "method": "GET",
                "headers": []
            }
        }
    }
    ],
    "creationDate": "2018-03-13T22:49:54.3396949Z",
    "status": "completed",
    "links": {
        "provisioningStatus": {
            "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/YxH1q4KScfvfkJQjgRI8QY1DznnUWZTH1/provisioningstatus",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/YxH1q4KScfvfkJQjgRI8QY1DznnUWZTH1",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Order"
    }
}
```

 

 




