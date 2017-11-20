---
title: Delete a configuration policy for the specified customer
description: How to delete a configuration policy for the specified customer and policy identifier.
MSHAttr:
- 'PreferredSiteName:MSDN'
- 'PreferredLib:/library/PartnerCenter'
ms.assetid: DEFEC12E-3EA0-401B-B612-ACD1D71DB415
---

# Delete a configuration policy for the specified customer


**Applies To**

-   Partner Center
-   Partner Center for Microsoft Cloud Germany

How to delete a configuration policy for the specified customer and policy identifier.

## <span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>Prerequisites


-   Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.
-   The customer identifier.
-   The policy identifier.

## <span id="C_"></span><span id="c_"></span>C#


To delete a configuration policy for the specified customer, first call the [**IAggregatePartner.Customers.ById**](https://review.docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer. Next, call the [**ConfigurationPolicies.ById**](https://review.docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) method with the policy ID to retrieve an interface to configuration policy operations for the specified policy. Finally, call the [**Delete**](https://review.docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.delete) or [**DeleteAsync**](https://review.docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.deleteasync) method to delete the configuration policy.

```
IAggregatePartner partnerOperations;
string selectedCustomerId; 
string selectedPolicyId;
           
partnerOperations.Customers.ById(selectedCustomerId).ConfigurationPolicies.ById(selectedPolicyId).Delete();
```

**Sample**: [Console test app](console-test-app.md). **Project**: Partner Center SDK Samples **Class**: DeleteConfigurationPolicy.cs

## <span id="Request"></span><span id="request"></span><span id="REQUEST"></span>Request


**Request syntax**

| Method     | Request URI                                                                                          |
|------------|------------------------------------------------------------------------------------------------------|
| **DELETE** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/policies/{policy-id} HTTP/1.1 |

 

**URI parameter**

Use the following path parameters when creating the request.

| Name        | Type   | Required | Description                                                   |
|-------------|--------|----------|---------------------------------------------------------------|
| customer-id | string | Yes      | A GUID-formatted string that identifies the customer.         |
| policy-id   | string | Yes      | A GUID-formatted string that identifies the policy to delete. |

 

**Request headers**

-   See [Partner Center REST headers](headers.md) for more information.

**Request body**

None

**Request example**

```
DELETE https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/policies/56edf752-ee77-4fd8-b7f5-df1f74a3a9ac HTTP/1.1
Authorization: Bearer <token> 
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Content-Length: 0
Content-Type: application/json
Host: api.partnercenter.microsoft.com
```

## <span id="Response"></span><span id="response"></span><span id="RESPONSE"></span>Response


If successful, the response returns a 204 No Content status code.

**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center REST error codes](error-codes.md).

**Response example**

```
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: cee5caf4-c322-4baa-b1d7-e94afb9891a4
MS-RequestId: 76b6f317-1da1-4b61-a6fd-9952439a2c46
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 18:10:41 GMT
```

 

 




