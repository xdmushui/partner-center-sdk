---
title: Retrieve validation status of a customer
description: How to retrieve the validation status of a customer.
ms.author: ali.khaki
ms.date: 10/27/2021
ms.service: partner-dashboard
ms.subservice:  partnercenter-sdk
---

# Retrieve the validation status of a customer

A partner can retrieve the status of a customer validation upon demand.

### Prerequisites

- Establish credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with App+User credentials only.

- A customer ID (customer-tenant-id). If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard). Select **CSP** from the Partner Center menu, followed by **Customers**. Select the customer from the customer list, then select **Account**. On the customer's Account page, look for the **Microsoft ID** in the **Customer Account Info** section. The Microsoft ID is the same as the customer ID (customer-tenant-id).

## API Details

### Request syntax 
|    Method    |  URI         |
|:------|:--------------------|
| GET   | https://api.partnercenter.microsoft.com/v1/customers/{customer-id}/validationStatus?type=account |   

#### URI parameter
Use the following query parameter to specify the customer you are retrieving validation status for.

|    Name    |  Type         | Required | Description      |
|:------|:-------------------|:---------|:-----------|
| {customer-id} | guid       |   Y      | The value is a GUID formatted CustomerTenantId that allows you to specify a customer. |

### Request headers
For more information, see [Partner Center REST headers](headers.md).

## REST response
Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center REST error codes](error-codes).


### Response fields
|    Field    |  Type         | Description | Notes      |
|:------|:-------------------|:---------|:-----------|
| Type | Enum       |  Validation information type      | Same data as *validation-type*. Validation type returns *account* as the response type. |
| Status  |  	Enum |	Validation status  |Available statuses: Unknown, UnderReview, Allowed, NotAllowed |
|Latest Update Time	|DateTime|	last status update time in UTC | |

### Response examples

#### Allowed status

``` HTTP
{
    "type": "account",
    "status": "Allowed",
    "lastUpdateDateTime": "2021-07-14T18:02:00"
}
```
#### In review status
``` HTTP
{
    "type": "account",
    "status": "UnderReview",
    "lastUpdateDateTime": "2021-07-14T18:02:00"
}
```

#### NotAllowed status
``` HTTP 
{
    "type": "account",
    "status": "NotAllowed",
    "lastUpdateDateTime": "2021-07-14T18:02:00"
}
```
#### Unknown status
``` HTTP
{
    "type": "account",
    "status": "Unknown",
    "lastUpdateDateTime": "2021-07-14T18:02:00"
}
```
#### 404 not found error
``` HTTP
{
    "code": 600074,
    "message": "Account Status for the customer, {customer-id} was not found.",
    "description": "Account Status for the customer, {customer-id} was not found.",
    "errorName": "AccountStatusNotFound",
    "isRetryable": false,
    "errorMessageExtended": "InternalErrorCode=600074"
```

