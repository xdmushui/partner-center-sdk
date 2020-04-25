---
title: Restore a deleted user for a customer
description: How to restore a deleted User by customer ID and user ID.
ms.assetid: A48A4718-6EAF-4FC8-8B44-F3FDCA2B3298
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice:  partnercenter-sdk
ms.localizationpriority: medium
---

# Restore a deleted user for a customer

**Applies To**

- Partner Center

How to restore a deleted **User** by customer ID and user ID.

## Prerequisites

- Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with App+User credentials only.

- A customer ID (`customer-tenant-id`). If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard). Select **CSP** from the Partner Center menu, followed by **Customers**. Select the customer from the customer list, then select **Account**. On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section. The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).

- The user ID. If you do not have the user ID, see [View deleted users for a customer](view-a-deleted-user.md).

## When can you restore a deleted user account?

The user state is set to "inactive" when you delete a user account. It remains that way for thirty days, after which the user account and its associated data are purged and made unrecoverable. You can only restore a deleted user account during this thirty-day window. Once deleted and marked "inactive" the user account is no longer returned as a member of the user collection (for example, using [Get a list of all user accounts for a customer](get-a-list-of-all-user-accounts-for-a-customer.md)).

## C\#

To restore a user, create a new instance of the [**CustomerUser**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.users.customeruser) class, and set the value of the [**User.State**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.users.user.state) property to [**UserState.Active**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.users.userstate).

You restore a deleted user by setting the user's state to active. You do not have to repopulate the remaining fields in the user resource. Those values will automatically be restored from the deleted, inactive user resource. 
Next, use the [**IAggregatePartner.Customers.ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer, and the [**Users.ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method to identify the user.

Finally, call the [**Patch**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.patch) method and pass the **CustomerUser** instance to send the request to restore the user.

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string selectedCustomerUserId;

var updatedCustomerUser = new CustomerUser()
{
    State = UserState.Active
};

// Restore customer user information.
var restoredCustomerUserInfo = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).Patch(updatedCustomerUser);
```

**Sample**: [Console test app](console-test-app.md). **Project**: Partner Center SDK Samples **Class**: CustomerUserRestore.cs

## REST request

### Request syntax

| Method    | Request URI                                                                                            |
|-----------|--------------------------------------------------------------------------------------------------------|
| **PATCH** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users/{user-id} HTTP/1.1 |

### URI parameter

Use the following query parameters to specify the customer id and user id.

| Name                   | Type     | Required | Description                                                                                                              |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------|
| **customer-tenant-id** | **guid** | Y        | The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results to a given customer. |
| **user-id**            | **guid** | Y        | The value is a GUID formatted **user-id** that belongs to a single user account.                                         |

### Request headers

For more information, see [Partner Center REST headers](headers.md).

### Request body

This table describes the required properties in the request body.

| Name       | Type   | Required | Description                                                            |
|------------|--------|----------|------------------------------------------------------------------------|
| State      | string | Y        | The user state. To restore a deleted user, this string must contain "active". |
| Attributes | object | N        | Contains "ObjectType": "CustomerUser".                                 |

### Request example

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users/a45f1416-3300-4f65-9e8d-f123b397a4ea HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 6e668bc0-5bd7-44d6-b6fa-529d41ce9659
MS-CorrelationId: 32be760f-8282-4e01-a37b-829c8a700e8a
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 269
Expect: 100-continue

{
    "State": "active",
    "Attributes": {
        "ObjectType": "CustomerUser"
    }
}
```

## REST response

If successful, the response returns the restored user information in the response body.

### Response success and error codes

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center REST Error Codes](error-codes.md).

### Response example

```http
HTTP/1.1 200 OK
Content-Length: 465
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 32be760f-8282-4e01-a37b-829c8a700e8a
MS-RequestId: 6e668bc0-5bd7-44d6-b6fa-529d41ce9659
MS-CV: ZTeBriO7mEaiM13+.0
MS-ServerId: 101112616
Date: Fri, 20 Jan 2017 22:24:55 GMT

{
    "usageLocation": "US",
    "id": "a45f1416-3300-4f65-9e8d-f123b397a4ea",
    "userPrincipalName": "e83763f7f2204ac384cfcd49f79f2749@dtdemocspcustomer005.onmicrosoft.com",
    "firstName": "Ferdinand",
    "lastName": "Filibuster",
    "displayName": "Ferdinand",
    "userDomainType": "none",
    "state": "active",
    "links": {
        "self": {
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users/a45f1416-3300-4f65-9e8d-f123b397a4ea",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "CustomerUser"
    }
}
```
