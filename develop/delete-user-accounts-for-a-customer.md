---
title: Delete a user account for a customer
description: How to delete an existing user account for a customer.
ms.assetid: 12097809-A62D-4929-9F1D-08676784BA39
ms.author: mhopkins
ms.date: 12/15/2017
ms.topic: article
ms.prod: partner-center
ms.technology: partner-center-sdk
ms.localizationpriority: medium
---

# Delete a user account for a customer


**Applies To**

-   Partner Center

How to delete an existing user account for a customer.

## <span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>Prerequisites


-   Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with App+User credentials only.
-   A customer ID (customer-tenant-id). If you do not have a customer's ID, you can look up the ID in Partner Center by choosing the customer from the customers list, selecting Account, then saving their Microsoft ID.
-   A user ID. If you do not have the user ID, see [Get a list of all user accounts for a customer](get-a-list-of-all-user-accounts-for-a-customer.md).

## <span id="What_happens_when_you_delete_a_user_account_"></span><span id="what_happens_when_you_delete_a_user_account_"></span><span id="WHAT_HAPPENS_WHEN_YOU_DELETE_A_USER_ACCOUNT_"></span>What happens when you delete a user account?


The user state is set to "inactive" when you delete a user account. It remains that way for thirty days, after which the user account and its associated data are purged and made unrecoverable. If you want to restore a deleted user account within the thirty day window, see [Restore a deleted user for a customer](restore-a-user-for-a-customer.md). Note that once deleted and marked "inactive" the user account is no longer returned as a member of the user collection (for example, using [Get a list of all user accounts for a customer](get-a-list-of-all-user-accounts-for-a-customer.md)).

## <span id="C_"></span><span id="c_"></span>C#


To delete an existing customer user account, use the [**IAggregatePartner.Customers.ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer. Then call the [**Users.ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method to identify the user. Finally, call the [**Delete**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.delete) method to delete the user and set the user state to inactive.

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string customerUserIdToDelete;

partnerOperations.Customers.ById(selectedCustomerId).Users.ById(customerUserIdToDelete).Delete();
```

**Sample**: [Console test app](console-test-app.md). **Project**: Partner Center SDK Samples **Class**: DeleteCustomerUser.cs

## <span id="REST_Request"></span><span id="rest_request"></span><span id="REST_REQUEST"></span>REST Request


**Request syntax**

| Method     | Request URI                                                                                            |
|------------|--------------------------------------------------------------------------------------------------------|
| **DELETE** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users/{user-id} HTTP/1.1 |

 

**URI parameter**

Use the following query parameter to identify the customer and user.

| Name                   | Type     | Required | Description                                                                                                               |
|------------------------|----------|----------|---------------------------------------------------------------------------------------------------------------------------|
| **customer-tenant-id** | **guid** | Y        | The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer. |
| **user-id**            | **guid** | Y        | The value is a GUID formatted **user-id** that belongs to a single user account.                                          |

 

**Request headers**

-   See [Partner Center REST Headers](headers.md) for more information.

**Request body**

None.

**Request example**

```http
DELETE https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users/a45f1416-3300-4f65-9e8d-f123b397a4ea HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: f113b126-ec13-4baa-ab4d-67c245244971
MS-CorrelationId: 709c0b80-016c-4662-b29f-697fdf03e87a
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Content-Length: 0
```

## <span id="REST_Response"></span><span id="rest_response"></span><span id="REST_RESPONSE"></span>REST Response


If successful, this method returns **204 No Content**.

**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center REST Error Codes](error-codes.md).

**Response example**

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 709c0b80-016c-4662-b29f-697fdf03e87a
MS-RequestId: f113b126-ec13-4baa-ab4d-67c245244971
MS-CV: 90KUJA7HKEaG8wHu.0
MS-ServerId: 101112616
Date: Tue, 24 Jan 2017 23:27:18 GMT
```