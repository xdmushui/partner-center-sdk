---
title: Update a customer's usage spending budget
description: Update the spending budget allocated for a customer's usage.
MSHAttr:
- 'PreferredSiteName:MSDN'
- 'PreferredLib:/library/PartnerCenter'
ms.assetid: D7843FBF-81FC-4FA0-8396-6365E12FB01B
---

# Update a customer's usage spending budget


<span class="sidebar_heading" style="font-weight: bold;">Applies
To</span>

-   Partner Center
-   Partner Center for Microsoft Cloud Germany
-   Partner Center for Microsoft Cloud for US Government

\[Some information relates to pre-released product which may be
substantially modified before it's commercially released. Microsoft
makes no warranties, express or implied, with respect to the information
provided here.\]

Update the [spending budget](customer-usage.md#customerusagesummary)
allocated for a customer's usage.

## <span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>Prerequisites


-   Credentials as described in [Partner Center
    authentication](partner-center-authentication.md). This scenario
    supports authentication with both standalone App and App+User
    credentials.
-   A customer ID (customer-tenant-id). If you do not have a customer's
    ID, you can look up the ID in Partner Center by choosing the
    customer from the customers list, selecting Account, then saving
    their Microsoft ID.

## <span id="C_"></span><span id="c_"></span>C#


To update a customer's usage spending budget, first create a new
**SpendingBudget** object with the updated amount. Then use the
**IAggregatePartner.Customers** collection and call the **ById()**
method with the specified customer's ID. Then access the **UsageBudget**
property and pass the updated usage budget to the **Patch()** or
**PatchAsync()** method.

```CSharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

// Create a new spending budget with the udpated amount.
var newUsageBudget = new SpendingBudget()
{  
    Amount = 100
};

// Update the customer&#39;s usage budget.
## var usageBudget = partnerOperations.Customers.ById(selectedCustomerId).UsageBudget.Patch(newUsageBudget);
PATCH https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/usagebudget HTTP/1.1
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
## }
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
            "uri":"/v1/customers/{customer-tenant-id}/usagebudget",
            "method":"PATCH",
            "headers":[]
        }
    }
}


