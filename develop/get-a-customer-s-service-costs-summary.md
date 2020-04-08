---
title: Get a customer's service costs summary
description: Gets a customer's service costs for the specified billing period.
ms.assetid: 99B250F7-6C29-4BC3-8427-0DF178D7BE68
ms.date: 06/10/2019
ms.service: partner-dashboard
ms.subservice:  partnercenter-sdk
ms.localizationpriority: medium
---

# Get a customer's service costs summary

Applies to:

- Partner Center

Gets a customer's service costs for the specified billing period.

## Prerequisites

- Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with App+User credentials.
- A customer identifier.
- A billing period indicator (**mostrecent**).

## C\#

To retrieve a service costs summary for the specified customer:

1. Call the [**IAggregatePartner.Customers.ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.
2. Use the [**ServiceCosts**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomer.servicecosts) property to get an interface to customer service costs collection operations.
3. Call the [**ByBillingPeriod**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.icustomerservicecostscollection.bybillingperiod) method with a member of the [**ServiceCostsBillingPeriod**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.servicecosts.servicecostsbillingperiod) enumeration to return an [**IServiceCostsCollection**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostscollection).
4. Use the [**IServiceCostsCollection.Summary.Get**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostsummary.get) or [**GetAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostsummary.getasync) method to get the customer's service costs summary.

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var serviceCostsSummary = partnerOperations.Customers.ById(selectedCustomerId).ServiceCosts.ByBillingPeriod(ServiceCostsBillingPeriod.MostRecent).Summary.Get();
```

## REST request

### Request syntax

| Method  | Request URI                                                                                                   |
|---------|---------------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/servicecosts/{billing-period} HTTP/1.1 |

#### URI parameters

Use the following path parameters to identify the customer and the billing period.

| Name           | Type   | Required | Description                                                                                                                      |
|----------------|--------|----------|----------------------------------------------------------------------------------------------------------------------------------|
| customer-id    | guid   | Yes      | A GUID formatted customer ID that identifies the customer.                                                                       |
| billing-period | string | Yes      | An indicator that represents the billing period. The only supported value is MostRecent. The case of the string does not matter. |

### Request headers

See [Partner Center REST headers](headers.md) for more information.

### Request body

None.

### Request example

```http
GET https://api.partnercenter.microsoft.com/v1/customers/65726577-c208-40fd-9735-8c85ac9cac68/servicecosts/mostrecent HTTP/1.1
Authorization: Bearer <authorization token>
Accept: application/json
MS-RequestId: e6a3b6b2-230a-4813-999d-57f883b60d38
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## REST response

If successful, the response body contains a [ServiceCostsSummary](service-costs-resources.md) resource that provides information about the service costs.

### Response success and error codes

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center REST error codes](error-codes.md).

### Response example

```http
HTTP/1.1 200 OK
Content-Length: 766
Content-Type: application/json; charset=utf-8
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
MS-RequestId: e6a3b6b2-230a-4813-999d-57f883b60d38
MS-CV: gPPoyNX1X0asAAcw.0
MS-ServerId: 101112202
Date: Fri, 02 Dec 2016 18: 54: 38 GMT

{
    "billingStartDate": "2015-12-12T00:00:00Z",
    "billingEndDate": "2016-01-11T00:00:00Z",
    "pretaxTotal": 17.22,
    "tax": 0.0,
    "afterTaxTotal": 17.22,
    "currencySymbol": "$",
    "customerId": "ae1d5b32-f9ff-4252-b2bf-40e21937a51a",
    "details":
     [
        {
            "invoiceType": "Recurring",
            "summary": {
                "billingStartDate": "2015-12-12T00:00:00Z",
                "billingEndDate": "2016-01-11T00:00:00Z",
                "pretaxTotal": 17.22,
                "tax": 0.0,
                "afterTaxTotal": 17.22,
                "currencyCode": "USD",
                "currencySymbol": "$",
                "customerId": "ae1d5b32-f9ff-4252-b2bf-40e21937a51a",
                "links": {},
                "attributes": {
                    "objectType": "ServiceCostsSummary"
                }
            }
        },
        {
            "invoiceType": "OneTime",
            "summary": {
                "billingStartDate": "2019-04-01T00:00:00Z",
                "billingEndDate": "2019-04-30T23:59:59.9999999Z",
                "pretaxTotal": 2,
                "tax": 0.2,
                "afterTaxTotal": 2.2,
                "currencyCode": "USD",
                "currencySymbol": "$",
                "customerId": "ae1d5b32-f9ff-4252-b2bf-40e21937a51a",
                "links": {},
                "attributes": {
                    "objectType": "ServiceCostsSummary"
                }
            }
        }
    ],
    "links": {
        "serviceCostLineItems": {
            "uri": "/customers/ae1d5b32-f9ff-4252-b2bf-40e21937a51a/servicecosts/MostRecent/lineitems",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/customers/ae1d5b32-f9ff-4252-b2bf-40e21937a51a/servicecosts/MostRecent",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "ServiceCostsSummary"
    }
}
```
