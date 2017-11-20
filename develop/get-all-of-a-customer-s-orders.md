---
title: Get a customer's orders
description: Gets all of a customer's orders.
MSHAttr:
- 'PreferredSiteName:MSDN'
- 'PreferredLib:/library/PartnerCenter'
ms.assetid: DF1E52F6-1A3D-4B26-8BCC-6E429410C662
---

# Get a customer's orders


**Applies To**

-   Partner Center
-   Partner Center operated by 21Vianet
-   Partner Center for Microsoft Cloud Germany
-   Partner Center for Microsoft Cloud for US Government

Gets all of a customer's orders.

## <span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>Prerequisites


-   Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with App+User credentials only.
-   A customer ID (customer-tenant-id). If you do not have a customer's ID, you can look up the ID in Partner Center by choosing the customer from the customers list, selecting Account, then saving their Microsoft ID.

## <span id="C_"></span><span id="c_"></span>C#


To obtain a list of all of a customer's orders, use your [**IAggregatePartner.Customers**](https://review.docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection and call the [**ById()**](https://review.docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollectionoperations.byid) method. Then call the [**Orders**](https://review.docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomeroperations.orders) property, followed by the [**Get()**](https://review.docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitygetoperations.get) or [**GetAsync()**](https://review.docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitygetoperations.getasync) methods.

```CSharp
// IAggregatePartner partnerOperations;
// var selectedCustomerID as String;

var orders = partnerOperations.Customers.ById(selectedCustomerId).Orders.Get();
```

**Sample**: [Console test app](console-test-app.md). **Project**: PartnerSDK.FeatureSamples **Class**: GetOrders.cs

## <span id="REST_Request"></span><span id="rest_request"></span><span id="REST_REQUEST"></span>REST Request


**Request syntax**

| Method  | Request URI                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders HTTP/1.1 |

 

**URI parameter**

Use the following query parameter to get all orders.

| Name                   | Type     | Required | Description                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **customer-tenant-id** | **guid** | Y        | The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller. |

 

**Request headers**

-   See [Headers](headers.md) for more information.

**Request body**

None.

**Request example**

```
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/orders HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
```

## <span id="REST_Response"></span><span id="rest_response"></span><span id="REST_RESPONSE"></span>REST Response


If successful, this method returns a collection of [Order](orders.md) resources in the response body.

**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Error Codes](error-codes.md).

**Response example**

```
HTTP/1.1 200 OK
Content-Length: 31942
Content-Type: application/json
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
Date: Mon, 23 Nov 2015 22:00:25 GMT

{
    "totalCount": 24,
    "items": [{
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
        "creationDate": "2015-10-08T10: 42: 36.54-07: 00",
        "attributes": {
            "etag": "<etag>",
            "objectType": "Order"
        }
    },
    {
        "id": "b8fe2ddb-6e85-4f8b-a5ba-06c20ce6d6c5",
        "referenceCustomerId": "<customer-tenant-id>",
        "lineItems": [{
            "lineItemNumber": 0,
            "offerId": "4271AA57-4129-477E-BA88-0A276D4A1619",
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
        "creationDate": "2015-10-09T21: 53: 18.83-07: 00",
        "attributes": {
            "etag": "<etag>",
            "objectType": "Order"
        }
    }
```

 

 




