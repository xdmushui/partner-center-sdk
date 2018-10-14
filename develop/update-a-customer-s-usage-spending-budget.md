---
title: Update a customer's usage spending budget
description: Update the spending budget allocated for a customer's usage.
ms.assetid: D7843FBF-81FC-4FA0-8396-6365E12FB01B
ms.date: 02/05/2018
ms.localizationpriority: medium
---

# Update a customer's usage spending budget


**Applies To**

-   Partner Center
-   Partner Center for Microsoft Cloud Germany
-   Partner Center for Microsoft Cloud for US Government

Update the [spending budget](customer-usage.md#customerusagesummary)
allocated for a customer's usage.

## <span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>Prerequisites


-   Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.
-   A customer ID (customer-tenant-id). If you do not have a customer's ID, you can look up the ID in Partner Center by choosing the
    customer from the customers list, selecting Account, then saving their Microsoft ID.

## <span id="C_"></span><span id="c_"></span>C#


To update a customer's usage spending budget, first create a new
[**SpendingBudget**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.usage.spendingbudget) object with the updated amount. Then use the
[**IAggregatePartner.Customers**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection) collection and call the [**ById()**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)
method with the specified customer's ID. Then access the [**UsageBudget**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomer.usagebudget)
property and pass the updated usage budget to the [**Patch()**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.usage.icustomerusagespendingbudget.patch) or
[**PatchAsync()**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.usage.icustomerusagespendingbudget.patchasync) method.

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

// Create a new spending budget with the udpated amount.
var newUsageBudget = new SpendingBudget()
{  
    Amount = 100
};

// Update the customer's usage budget.
var usageBudget = partnerOperations.Customers.ById(selectedCustomerId).UsageBudget.Patch(newUsageBudget);
```



## <span id="_Request"></span><span id="_request"></span><span id="_REQUEST"></span> REST Request


**Request syntax**

| Method    | Request URI                                                                                             |
|-----------|---------------------------------------------------------------------------------------------------------|
| **PATCH** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/usagebudget  HTTP/1.1 |   
 

**URI parameter**

Use the following query parameter to update the billing profile.

| Name                   | Type     | Required | Description                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **customer-tenant-id** | **guid** | Y        | The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller. |

 

**Request headers**

-   See [Headers](headers.md) for more information.


**Request body**

The full resource.


**Request example**

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/usagebudget HTTP/1.1
Authorization: Bearer <token>
Accept: application/json, text/plain, */*
MS-RequestId: 312b044d-dc41-4b37-c2d5-7d27322d9654
MS-CorrelationId: 7cb67bb7-4750-403d-cc2e-6bc44c52d52c
Content-Type: application/json;charset=utf-8
X-Locale: "en-US"

{
     "Amount": 100,
     "Attributes": {
          "ObjectType": "SpendingBudget"
     }
}
```



## <span id="_Response"></span><span id="_response"></span><span id="_RESPONSE"></span> REST Response

If successful, this method returns a user's spending budget with the updated amount.


**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Error Codes](error-codes.md).


**Response example**

```http
HTTP/1.1 200 OK
Content-Length: 12014
Content-Type: application/json
MS-CorrelationId: 7cb67bb7-4750-403d-cc2e-6bc44c52d52c
MS-RequestId: be82a8ba-4a53-49f7-8313-b033c058687e
Date: Tue, 10 Nov 2015 19:09:59 GMT

{
    {
        "amount": 100,
        "usageSpendingBudget": 100,
        "attributes":{
            "objectType":"SpendingBudget"
        }
    },
    "links":{
        "self":{
            "uri":"/v1/customers/<customer-tenant-id>/usagebudget",
            "method":"PATCH",
            "headers":[]
        }
    }
}
```

