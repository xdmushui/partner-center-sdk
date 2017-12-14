---
title: Create a new configuration policy for the specified customer
description: How to create a new configuration policy for the specified customer.
ms.assetid: 95649991-A950-4F43-87E8-3EB1E7D06FCD
ms.author: v-thpr
ms.date: 12/15/2017
ms.topic: article
ms.prod: partner-center
ms.technology: partner-center-sdk
---

# Create a new configuration policy for the specified customer


**Applies To**

-   Partner Center
-   Partner Center for Microsoft Cloud Germany

How to create a new configuration policy for the specified customer.

## <span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>Prerequisites


-   Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.
-   The customer identifier.

## <span id="C_"></span><span id="c_"></span>C#


To create a new configuration policy for the specified customer, instantiate a new [**ConfigurationPolicy**](https://review.docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.configurationpolicy) object as shown in the following code snippet. Then call the [**IAggregatePartner.Customers.ById**](https://review.docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer. Next, retrieve the [**ConfigurationPolicies**](https://review.docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomer.configurationpolicies) property to get an interface to configuration policy collection operations. Finally, call the [**Create**](https://review.docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) or [**CreateAsync**](https://review.docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync) method to create the configuration policy.

```
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var configurationPolicyToCreate = new ConfigurationPolicy
{
    Name = "Test Config Policy",
    Description = "This configuration policy is created by the SDK samples",
    PolicySettings = new List<PolicySettingsType>() { 
        PolicySettingsType.OobeUserNotLocalAdmin, 
        PolicySettingsType.SkipEula }
};

var createdConfigurationPolicy = 
    partnerOperations.Customers.ById(selectedCustomerId).ConfigurationPolicies.Create(configurationPolicyToCreate);
```

**Sample**: [Console test app](console-test-app.md). **Project**: Partner Center SDK Samples **Class**: CreateConfigurationPolicy.cs

## <span id="Request"></span><span id="request"></span><span id="REQUEST"></span>Request


**Request syntax**

| Method   | Request URI                                                                              |
|----------|------------------------------------------------------------------------------------------|
| **POST** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/policies HTTP/1.1 |

 

**URI parameter**

Use the following path parameters when creating the request.

| Name        | Type   | Required | Description                                           |
|-------------|--------|----------|-------------------------------------------------------|
| customer-id | string | Yes      | A GUID-formatted string that identifies the customer. |

 

**Request headers**

-   See [Partner Center REST headers](headers.md) for more information.

**Request body**

The request body must contain an object with the configuration policy information as described in the following table:

| Name           | Type             | Required | Description                      |
|----------------|------------------|----------|----------------------------------|
| name           | string           | Yes      | The friendly name of the policy. |
| category       | string           | Yes      | The policy category.             |
| description    | string           | No       | The policy description.          |
| policySettings | array of strings | Yes      | The policy settings.             |

 

**Request example**

```
POST https://api.partnercenter.microsoft.com//v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/policies HTTP/1.1
Authorization: Bearer <token> 
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Content-Length: 212
Content-Type: application/json
Host: api.partnercenter.microsoft.com

{
    "name": "Windows 10 Enterprise E5",
    "category": "o_o_b_e",
    "description": "test policy creation from API",
    "policySettings": ["oobe_user_not_local_admin", "skip_express_settings"]
}
```

## <span id="Response"></span><span id="response"></span><span id="RESPONSE"></span>Response


If successful, the response body contains the [ConfigurationPolicy](devicedeployment.md#configurationpolicy) resource for the new policy.

**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center REST error codes](error-codes.md).

**Response example**

```
HTTP/1.1 200 OK
Content-Length: 404
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 4beda413-74fc-4839-b74f-f580c353ab45
MS-RequestId: 0dfadf74-aa66-49ed-9a67-b3b78d9297cc
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 18:07:36 GMT

{
    "id": "40cdb858-edcc-44d7-9083-d6a36d43bd3f",
    "name": "Windows 10 Enterprise E5",
    "category": "o_o_b_e",
    "description": "test policy creation from API",
    "devicesAssigned": 0,
    "policySettings": ["oobe_user_not_local_admin", "skip_express_settings"],
    "createdDate": "2017-07-25T18:07:36",
    "lastModifiedDate": "2017-07-25T18:07:36",
    "attributes": {
        "objectType": "ConfigurationPolicy"
    }
}
```

 

 




