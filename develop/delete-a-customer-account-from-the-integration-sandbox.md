---
title: Delete a customer account from the integration sandbox
description: How to delete a customer account from the Testing in Production (Tip) integration sandbox.
ms.assetid: B95431F6-EA7F-4C21-835F-6D6C303B05A5
ms.date: 12/15/2017
ms.localizationpriority: medium
---

# Delete a customer account from the integration sandbox


**Applies To**

- Partner Center
- Partner Center operated by 21Vianet
- Partner Center for Microsoft Cloud Germany
- Partner Center for Microsoft Cloud for US Government

How to delete a customer account from the Testing in Production (Tip) integration sandbox.

>[!NOTE]
>Please be aware that deleting a customer account means that all resources associated with that customer tenant will be purged.

## <span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>Prerequisites


- Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.
- A customer ID (customer-tenant-id).
- All Azure Reserved Virtual Machine Instances and software purchase orders must be cancelled before deleting a customer from the Tip integration sandbox.

## <span id="C_"/><span id="c_"/>C#


To delete a customer from the Tip integration sandbox, pass your Tip account credentials to the [**CreatePartnerOperations**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) method to get an [**IPartner**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.ipartner) interface to partner operations. 

Next, ensure that all Azure Reserved Virtual Machine Instances and software purchase orders for that customer are cancelled. To do this, use the partner operations interface to retrieve the collection of entitlements by calling the [**Customers.ById()**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier to specify the customer, then the **Entitlements** property, and finally the **Get** or **GetAsync** method to retrieve the [**Entitlement**](entitlement-resources.md) collection.

For each [**Entitlement**](entitlement-resources.md) in the collection, use the [**entitlement.ReferenceOrder.Id**](entitlement-resources.md#referenceorder) to get a local copy of the corresponding [Order](order-resources.md#order) from the customer's collection of orders. Set the [**Order.Status**](order-resources.md#order) property to "Cancelled" and use the **Patch()** method to update the order. 

To ensure that all orders are cancelled, the following example uses a loop to poll each order until it's status is "Cancelled". When all orders are cancelled, call the **Delete** method for the customer.

``` csharp
// IPartnerCredentials tipAccountCredentials;
// Customer tenant Id to be deleted.
// string customerTenantId;

IPartner tipAccountPartnerOperations = PartnerService.Instance.CreatePartnerOperations(tipAccountCredentials);

// Get all entitlements whose order must be cancelled.
ResourceCollection<Entitlement> entitlements = tipAccountPartnerOperations.Customers.ById(customerTenantId).Entitlements.Get();

// Cancel all orders
foreach (var entitlement in entitlements)
{
    var order = tipAccountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(entitlement.ReferenceOrder.Id).Get();
    order.Status = "Cancelled";
    order = tipAccountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(order.Id).Patch(order);
}

// Keep polling until the status of all orders is "Cancelled".
bool proceed = true;
do
{
    // Check if all the orders were cancelled.
    foreach (var entitlement in entitlements)
    {
        var order = tipAccountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(entitlement.ReferenceOrder.Id).Get();
        if (!order.Status.Equals("Cancelled", StringComparison.OrdinalIgnoreCase))
        {
            proceed = false;
        }
    }

    // Wait for a few seconds.
    Thread.Sleep(5000);
}
while (proceed == false);

tipAccountPartnerOperations.Customers.ById(customerTenantId).Delete();
```

**Sample**: [Console test app](console-test-app.md). **Project**: Partner Center PartnerCenterSDK.FeaturesSamples **Class**: DeleteCustomerFromTipAccount.cs

## <span id="_Request"/><span id="_request"/><span id="_REQUEST"/> REST Request


**Request syntax**

| Method     | Request URI                                                                            |
|------------|----------------------------------------------------------------------------------------|
| **DELETE** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id} HTTP/1.1 |

 

**URI parameter**

Use the following query parameter to delete a customer.

| Name                   | Type     | Required | Description                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **customer-tenant-id** | **guid** | Y        | The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller. |

 

**Request headers**

- See [Partner Center REST headers](headers.md) for more information.

**Request body**

None.

**Request example**

```http
DELETE https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id> HTTP/1.1
Accept: application/json
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
Content-Length: 0
```

## <span id="_Response"/><span id="_response"/><span id="_RESPONSE"/> REST Response


If successful, this method returns an empty response.

**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center REST error codes](error-codes.md).

**Response example**

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
Date: Wed, 16 Mar 2016 00:43:02 GMT
```