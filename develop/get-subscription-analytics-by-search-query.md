---
title: Get subscription analytics by search query
description: How to get subscription analytics information filtered by a search query. 
ms.assetid: 
ms.author: v-thpr   
robots: noindex,nofollow   
ms.date: 05/10/2018
ms.topic: article
ms.prod: partner-center
ms.technology: partner-center-sdk
---

# Get subscription analytics information filtered by a search query

>[!IMPORTANT]   
>This information relates to pre-released product which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here. 

**Applies To**

-   Partner Center
-   Partner Center operated by 21Vianet
-   Partner Center for Microsoft Cloud Germany
-   Partner Center for Microsoft Cloud for US Government


How to get subscription analytics information for your customers filtered by a search query.

## <span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>Prerequisites


-   Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with User credentials only.


## <span id="Request"></span><span id="request"></span><span id="REQUEST"></span>REST Request


**Request syntax**

| Method  | Request URI                                                                                                                   |
|---------|-------------------------------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/partner/v1/analytics/subscriptions?filter={filter_string} HTTP/1.1 |

 

**URI parameters**

Use the following path parameter to identify your organization and filter the search.

| Name                   | Type     | Required | Description                                        |
|------------------------|----------|----------|----------------------------------------------------|
| filter_string          | string   | Yes      | The filter to apply to the subscription analytics. See the Filter syntax and Filter fields sections for the syntax, fields, and operators to use in this parameter. |
 

**Filter syntax**

The filter parameter must be composed as a series of comma separated, key-value pairs. Each key and value must be individually quoted and separated by a colon. The entire filter must be encoded.

An unencoded example looks like this:
-   String: ?filter=Field operator ‘Value’
-   Boolean: ?filter=Field operator Value
-   Contains ?filter//contains(field,’value’)

The following table lists the parameters and their descriptions:

| Parameter            | Type        | Required | Description                                                                                  |
|----------------------|-------------|----------|----------------------------------------------------------------------------------------------|
| top                  | int         | No       | The number of rows of data to return in the request. If the value is not specified, the maximum value and the default value are 10000. If there are more rows in the query, the response body includes a next link that you can use to request the next page of data.         |
| skip                 | int         | No       | The number of rows to skip in the query. Use this parameter to page through large data sets. For example, top=10000 and skip=0 retrieves the first 10000 rows of data, top=10000 and skip=10000 retrieves the next 10000 rows of data.                            |
| filter               | string      | No       | One or more statements that filter the rows in the response. Each filter statement contains a field name from the response body and a value that are associated with the **eq**, **ne**, or for certain fields, the **contains** operator. Statements can be combined using **and** or **or**. String values must be surrounded by single quotes in the filter parameter. See the following section for a list of fields that can be filtered and the operators that are supported with those fields.           |
| aggregationLevel     | string      | No       | Specifies the time range for which to retrieve aggregate data. Can be one of the following strings: **day**, **week**, or **month**. If the value is not specified, the default is **dateRange**. **Note**: This parameter applies only when a date field is passed as part of the groupBy parameter. |
| groupBy              | string      | No       | A statement that applies data aggregation only to the specified fields. See the following section for a list of filter fields. |


**Filter fields**

The filter parameter of the request contains one or more statements that filter the rows in the response. Each statement contains a field and value that are associated with the **eq** or **ne** operators, and some fields also support the **contains**, **gt**, **lt**, **ge**, and **le** operators. Statements can be combined using **and** or **or**.

The following are examples of filter strings: 
```
autoRenewEnabled eq true

autoRenewEnabled eq true and customerMarket eq 'US'
```

The following table shows a list of the supported fields and support operators for the filter parameter. String values must be surrounded by single quotes.

| Parameter                 | Supported Operators     | Description                                                                                  |
|---------------------------|-------------------------|----------------------------------------------------------------------------------------------|
| customerTenantId          | eq,ne                   | A GUID-formatted string that identifies the customer tenant.                                 |
| customerName              | contains                | The name of the customer.                                                                    |
| customerMarket            | eq,ne                   | The country/region that the customer does business in.                                       |
| id                        | eq,ne                   | A GUID-formatted string that identifies the subscription.                                    |
| status                    | eq,ne                   | The subscription status. Supported values are: "ACTIVE", "SUSPENDED", or "DEPROVISIONED".    |
| productName               | contains, eq,ne         | The name of the product.                                                                     |
| subscriptionType          | eq,ne                   | The subscription type. **Note**: This field is case sensitive. Supported values are: "Office", "Azure", "Microsoft365", "Dynamics", "EMS". |
| autoRenewEnabled          | eq,ne                   | A value indicating whether the subscription is renewed automatically.                        |
| partnerId                 | eq,ne                   | The MPN ID. For a direct reseller, this will be the MPN ID of the partner. For an indirect reseller, this will be the MPN ID of the indirect reseller. |
| friendlyName              | contains                | The name of the subscription.                                                                |
| creationDate              | eq, ne, gt, lt, ge, le  | The date the subscription was created.                                                       |
| effectiveStartDate        | eq, ne, gt, lt, ge, le  | The date the subscription starts.                                                            |
| commitmentEndDate         | eq, ne, gt, lt, ge, le  | The date the subscription ends.                                                              |
| currentStateEndDate       | eq, ne, gt, lt, ge, le  | The date that the current status of the subscription will change.                            |
| trialToPaidConversionDate | eq, ne, gt, lt, ge, le  | The date that the subscription converts from trial to paid. The default value is null.        |
| trialStartDate            | eq, ne, gt, lt, ge, le  | The date that the trial period for the subscription started. The default value is null.       |
| lastUsageDate             | eq, ne, gt, lt, ge, le  | The date that the subscription was last used. The default value is null.                      |
| deprovisionedDate         | eq, ne, gt, lt, ge, le  | The date that the subscription was deprovisioned. The default value is null.                  |
| lastRenewalDate           | eq, ne, gt, lt, ge, le  | The date that the subscription was last renewed. The default value is null.                   |



**Request headers** 

-   See [Headers](headers.md) for more information.

**Request body**

None.

**Request example**

```
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/subscriptions?filter=autoRenewEnabled eq true HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105123
Content-Type: application/json
Content-Length: 0
```

## <span id="Response"></span><span id="response"></span><span id="RESPONSE"></span>REST Response


If successful, the response body contains a collection of [Subscription](partner-center-analytics.md#subscription) resources that meet the fileter criteria.

**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Error Codes](error-codes.md).

**Response example**

```
HTTP/1.1 200 OK
Content-Length: 177
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-RequestId: ec8f62e5-1d92-47e9-8d5d-1924af105123

{
    "customerTenantId": "735920EB-A564-4C72-9FE5-52632562712C",
    "customerName": "SURFACE TEST2",
    "customerMarket": "US",
    "id": "B76412DA-D382-4688-A6A4-711A207C1C2E",
    "status": "ACTIVE",
    "productName": "UNKNOWN",
    "subscriptionType": "Azure",
    "autoRenewEnabled": true,
    "partnerId": "3B33E682-00C3-41EE-9DD2-A548ADF56438",
    "friendlyName": "MICROSOFT AZURE",
    "creationDate": "2017-06-02T23:11:58.747",
    "effectiveStartDate": "2017-06-02T00:00:00",
    "commitmentEndDate": null,
    "currentStateEndDate": null,
    "trialToPaidConversionDate": null,
    "trialStartDate": null,
    "trialEndDate": null,
    "lastUsageDate": null,
    "deprovisionedDate": null,
    "lastRenewalDate": null,
    "licenseCount": 0
}
```
