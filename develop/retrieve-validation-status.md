---
title: Retrieve validation status of a customer
description: How to retrieve the validation status of a customer.
ms.date: 10/27/2021
ms.service: partner-dashboard
ms.subservice:  partnercenter-sdk
---

# Retrieve the validation status of a customer

A partner can retrieve the status of a customer validation upon demand.

### Prerequisites

Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with App+User credentials only.

A customer ID (customer-tenant-id). If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard). Select **CSP** from the Partner Center menu, followed by **Customers**. Select the customer from the customer list, then select **Account**. On the customer's Account page, look for the **Microsoft ID** in the **Customer Account Info** section. The Microsoft ID is the same as the customer ID (customer-tenant-id).

### API Details
|        | |
|:------|:--------------------|
| API	| https://api.partnercenter.microsoft.com/v1/customers/{customer-id}/validationStatus?type=account |
| Query |   Parameter	{customer-id}   |
|       |   Required:  Yes              |
|       |   Value: {Customer Tenant ID} |
| Validation Type | 	Please find the available validation type: <br/><br/>  Account: Account Status |
| Response |	<table>  <thead>  <tr>  <th>Field</th>  <th>Type</th>  <th>Description</th>  <th>Notes</th> </tr>  </thead>  <tbody>  <tr>  <td>Type</td>  <td>Enum</td>  <td>Validation information type</td> <td>Same data as *validation-type*</td>  </tr>  <tr>  <td>Status</td>  <td>Enum</td>  <td>Validation Status</td> <td>Available status: Unknown, UnderReview, Allowed, NotAllowed</td> </tr> <tr> <td> Latest Update Time </td> <td>DateTime</td> <td>last status update time in UTC</td> </tbody>  </table> |	
|<table> <td>Sample response</td> 

<td>

``` 
#### allowed status
{
    "type": "account",
    "status": "Allowed",
    "lastUpdateDateTime": "2021-07-14T18:02:00"
}
```

```
#### In review status
{
    "type": "account",
    "status": "UnderReview",
    "lastUpdateDateTime": "2021-07-14T18:02:00"
}
```
```
#### NotAllowed status

{
    "type": "account",
    "status": "NotAllowed",
    "lastUpdateDateTime": "2021-07-14T18:02:00"
}
```
```
#### Unknown status

{
    "type": "account",
    "status": "Unknown",
    "lastUpdateDateTime": "2021-07-14T18:02:00"
}
```
```
#### 404 not found error

{
    "code": 600074,
    "message": "Account Status for the customer, {customer-id} was not found.",
    "description": "Account Status for the customer, {customer-id} was not found.",
    "errorName": "AccountStatusNotFound",
    "isRetryable": false,
    "errorMessageExtended": "InternalErrorCode=600074"
}
```

\#### Purchase Eligibility <br/><br/>
Customer's transactions will be blocked when their account has status below: <br/><br/>
* UnderReview<br/><br/>
* NotAllowed<br/><br/>
* Unknown<br/><br/>

Customer's transactions won't be blocked with the following conditions:<br/><br/>
* Allowed status<br/><br/>
* Customer doesn't have account status<br/><br/>

</td>
</tbody>
</table>|