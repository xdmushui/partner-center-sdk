---
title: Partner Center Analytics
description: Partner Center Analytics public API documentation.
ms.assetid: 
ms.author: v-thpr   
robots: noindex,nofollow   
ms.date: 05/07/2018
ms.topic: article
ms.prod: partner-center
ms.technology: partner-center-sdk
---

# Partner Center Analytics - Public API documentation

>[!IMPORTANT]   
>This information relates to pre-released product which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here. 

**Applies To**

-   Partner Center
-   Partner Center operated by 21Vianet
-   Partner Center for Microsoft Cloud Germany
-   Partner Center for Microsoft Cloud for US Government


The Analytics API allows users to programmatically access all the data that is being presented in the User Experience. This data is currently limited to Subscriptions in the CSP Program. In future, this API will be extended to include data from all other APIs in the CSP program, the Referral and Search Analytics API for the Referral program, and more. 

## <span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>Prerequisites


-   Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.

## <span id="Subscription_Analytics"></span><span id="subscription_analytics"></span><span id="SUBSCRIPTION_ANALYTICS"></span>CSP Program: Subscription Analytics



The following scenarios show you how to use the [Subscription](#subscription) API to retrieve all your Partner Center Analytics information, filter it with a search query, or group it by dates, terms or aggregation level.    

-   [Get all Subscription Analytics information](#get_all_subscription_analytics)    
-   [Get Subscription Analytics information filtered by a search query](#get_subscription_analytics_by_search_query)    
-   [Get Subscription Analytics information grouped by dates or terms](#get_subscription_analytics_by_dates_or_terms)    
-   [Get Subscription Analytics information grouped by aggregation level](#get_subscription_analytics_by_aggregation_level)    


## <span id="Get_all_subscription_analytics"></span><span id="get_all_subscription_analytics"></span><span id="GET_ALL_SUBSCRIPTION_ANALYTICS"></span>Get all subscription analytics information



**Applies To**

-   Partner Center
-   Partner Center operated by 21Vianet
-   Partner Center for Microsoft Cloud Germany
-   Partner Center for Microsoft Cloud for US Government


How to get all the subscription analytics information for your customers. 

## <span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>Prerequisites


-   Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.

## <span id="Request"></span><span id="request"></span><span id="REQUEST"></span>REST Request


**Request syntax**

| Method  | Request URI                                                                                                                   |
|---------|-------------------------------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*]/{myorg}/analytics/v1/subscriptions HTTP/1.1                                                                     |

 

**URI parameter**

Use the following path parameter to identify your organization.

| Name                   | Type     | Required | Description                                |
|------------------------|----------|----------|--------------------------------------------|
| myorg                  | string   | Yes      | A string that identifies the organization. |

 

**Request headers**

-   See [Headers](headers.md) for more information.

**Request body**

None.

**Request example**

```
GET https://api.partnercenter.microsoft.com/{myorg}/analyticsapi/commercial/subscriptions HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105123
Content-Type: application/json
Content-Length: 0
```

## <span id="Response"></span><span id="response"></span><span id="RESPONSE"></span>Response


If successful, the response body contains a collection of [Subscription](#subscriptions) resources.

**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Error Codes](error-codes.md).

**Response example**

```
{
    "customerTenantId": "76906668-27FC-4F5B-A35C-75A9823E13AF",
    "customerName": "TESTORG65656565",
    "customerMarket": "US",
    "id": "4BF546B2-8998-4838-BEE2-5F1BBE65A04F",
    "status": "ACTIVE",
    "productName": "OFFICE 365 BUSINESS PREMIUM",
    "subscriptionType": "Office",
    "autoRenewEnabled": true,
    "partnerId": "3B33E682-00C3-41EE-9DD2-A548ADF56438",
    "friendlyName": "FULL OFFICE SUITE",
    "creationDate": "2016-02-04T19:29:38.037",
    "effectiveStartDate": "2016-02-04T00:00:00",
    "commitmentEndDate": "2019-02-10T00:00:00",
    "currentStateEndDate": "2019-02-10T00:00:00",
    "trialToPaidConversionDate": null,
    "trialStartDate": null,
    "trialEndDate": null,
    "lastUsageDate": null,
    "deprovisionedDate": null,
    "lastRenewalDate": "2018-02-10T02:39:57.729",
    "licenseCount": 2
}
```


## <span id="Get_subscription_analytics_by_search_query"></span><span id="get_subscription_analytics_by_search_query"></span><span id="GET_SUBSCRIPTION_ANALYTICS_BY_SEARCH_QUERY"></span>Get subscription analytics information filtered by a search query



**Applies To**

-   Partner Center
-   Partner Center operated by 21Vianet
-   Partner Center for Microsoft Cloud Germany
-   Partner Center for Microsoft Cloud for US Government


How to get subscription analytics information for your customers filtered by a search query.

## <span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>Prerequisites


-   Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.


## <span id="Request"></span><span id="request"></span><span id="REQUEST"></span>REST Request


**Request syntax**

| Method  | Request URI                                                                                                                   |
|---------|-------------------------------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*]/{myorg}/analytics/v1/subscriptions?filter={field = 'value'} HTTP/1.1 |

 

**URI parameters**

Use the following path parameters to identify your organization and filter the search.

| Name                   | Type     | Required | Description                                        |
|------------------------|----------|----------|----------------------------------------------------|
| myorg                  | string   | Yes      | A string that identifies the organization.         |
| filter                 | string   | Yes      | The filter to apply to the subscription analytics. See the Filter syntax and Filter fields sections for the syntax, fields, and operators to use in this parameter. |
 

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
| filter               | string      | No       | One or more statements that filter the rows in the response. Each filter statement contains a field name from the response body and a value that are associated with the **eq**, **ne**, or for certain fields, the **contains** operator. Statements can be combined using **and** or **or**. String values must be surrounded by single quotes in the filter parameter. For example, *filter=market eq 'US'* and *gender eq 'm'*. See the following section for a list of fields that can be filtered and the operators that are supported with those fields.           |
| aggregationLevel     | string      | No       | Specifies the time range for which to retrieve aggregate data. Can be one of the following strings: **day**, **week**, or **month**. If the value is not specified, the default is **dateRange**. **Note**: This parameter applies only when a date field is passed as part of the groupBy parameter. |
| groupBy              | string      | No       | A statement that applies data aggregation only to the specified fields. See the following section for a list of filter fields. |


**Filter fields**

The filter parameter of the request contains one or more statements that filter the rows in the response. Each statement contains a field and value that are associated with the **eq** or **ne** operators, and some fields also support the **contains**, **gt**, **lt**, **ge**, and **le** operators. Statements can be combined using **and** or **or**.

The following are examples of filter strings: 
```
filter=contains(reviewText,'great') and contains(reviewText,'ads')

deviceRAM lt 2048 and market eq 'US'
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
| subscriptionType          | eq,ne                   | The subscription type. **Note**: This field is case sensitive. Supported values are: "Office", "Azure". |
| autoRenewEnabled          | eq,ne                   | A value indicating whether the subscription is renewed automatically.                        |
| partnerId                 | eq,ne                   | The MPN ID of the partner.                                                                   |
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
GET https://api.partnercenter.microsoft.com/analytics/v1/{myorg}/subscriptions?filter=status%20eq%20%27ACTIVE%27 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105123
Content-Type: application/json
Content-Length: 0
```

## <span id="Response"></span><span id="response"></span><span id="RESPONSE"></span>REST Response


If successful, the response body contains a collection of [Subscription](#subscriptions) resources.

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
    "autoRenewEnabled": false,
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

## <span id="Get_subscription_analytics_by_dates_or_terms"></span><span id="get_subscription_analytics_by_dates_or_terms"></span><span id="GET_SUBSCRIPTION_ANALYTICS_BY_DATES_OR_TERMS"></span>Get subscription analytics grouped by dates or terms



**Applies To**

-   Partner Center
-   Partner Center operated by 21Vianet
-   Partner Center for Microsoft Cloud Germany
-   Partner Center for Microsoft Cloud for US Government


How to get subscription analytics information for your customers grouped by dates or terms.

## <span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>Prerequisites


-   Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.


## <span id="Request"></span><span id="request"></span><span id="REQUEST"></span>REST Request


**Request syntax**

| Method  | Request URI                                                                                                                   |
|---------|-------------------------------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*]/analytics/v1/{myorg}/subscriptions?groupby={termField1, dateField1, termField2, dateField2…} HTTP/1.1 |

 

**URI parameters**

Use the following path parameters to identify your organization and to group the results.

| Name                   | Type                            | Required | Description                                        |
|------------------------|---------------------------------|----------|----------------------------------------------------|
| myorg                  | string                          | Yes      | A string that identifies the organization.         |
| groupby_queries        | pairs of strings and dateTime   | Yes      | The terms and dates to filter the result.          |

 

**GroupBy syntax**

The filter parameter must be composed as a series of comma separated, key-value pairs. Each key and value must be individually quoted and separated by a colon. The entire filter must be encoded.

An unencoded example looks like this:
```
?filter{"Field":"CompanyName","Value":"cont","Operator":"starts_with"}
```

The following table describes the required key-value pairs:

| Key                    | Value                                                                                           |
|------------------------|-------------------------------------------------------------------------------------------------|
| Field                  | The field to filter. The valid values can be found in ?                                         |
| Value                  | The value to filter by. The case of the value is ignored.                                       |
| Operator               | The operator to apply. The only supported value for this customer scenario is "starts_with".    |



**Request headers**

-   See [Headers](headers.md) for more information.

**Request body**

None.

**Request example**

```
GET https://api.partnercenter.microsoft.com/analytics/v1/{myorg}/subscriptions/groupby={termField1, dateField1, termField2, dateField2} HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105123
Content-Type: application/json
Content-Length: 0
```

## <span id="Response"></span><span id="response"></span><span id="RESPONSE"></span>REST Response


If successful, the response body contains a collection of [Subscription](#subscriptions) resources grouped by the specified terms and dates.

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
    "customerTenantId": "76906668-27FC-4F5B-A35C-75A9823E13AF",
    "customerName": "TESTORG65656565",
    "customerMarket": "US",
    "id": "4BF546B2-8998-4838-BEE2-5F1BBE65A04F",
    "status": "ACTIVE",
    "productName": "OFFICE 365 BUSINESS PREMIUM",
    "subscriptionType": "Office",
    "autoRenewEnabled": true,
    "partnerId": "3B33E682-00C3-41EE-9DD2-A548ADF56438",
    "friendlyName": "FULL OFFICE SUITE",
    "creationDate": "2016-02-04T19:29:38.037",
    "effectiveStartDate": "2016-02-04T00:00:00",
    "commitmentEndDate": "2019-02-10T00:00:00",
    "currentStateEndDate": "2019-02-10T00:00:00",
    "trialToPaidConversionDate": null,
    "trialStartDate": null,
    "trialEndDate": null,
    "lastUsageDate": null,
    "deprovisionedDate": null,
    "lastRenewalDate": "2018-02-10T02:39:57.729",
    "licenseCount": 2
}
```


## <span id="Get_subscription_analytics_by_aggregation_level"></span><span id="get_subscription_analytics_by_aggregation_level"></span><span id="GET_SUBSCRIPTION_ANALYTICS_BY_AGGREGATION_LEVEL"></span>Get subscription analytics grouped by aggregation level



**Applies To**

-   Partner Center
-   Partner Center operated by 21Vianet
-   Partner Center for Microsoft Cloud Germany
-   Partner Center for Microsoft Cloud for US Government


How to get subscription analytics information for your customers grouped by dates or terms and filtered by an aggregation level (For example, day).

## <span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>Prerequisites


-   Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.


## <span id="Request"></span><span id="request"></span><span id="REQUEST"></span>REST Request


**Request syntax**

| Method  | Request URI                                                                                                                             |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*]/{myorg}/analytics/v1/subscriptions?groupby={termField1, dateField1, termField2, dateField2}]&aggLevel={agg_level} HTTP/1.1 |

 

**URI parameters**

Use the following path parameters to identify your organization and to group the results.

| Name                   | Type                            | Required | Description                                        |
|------------------------|---------------------------------|----------|----------------------------------------------------|
| myorg                  | string                          | Yes      | A string that identifies the organization.         |
| groupby_queries        | pairs of strings and dateTime   | Yes      | The terms and dates to filter the result.          |
| agg_level              | aggregationlevel                | Yes      | The level at which to aggregate the data. Allowable values are "day", "month", "year". The aggregation level applies to all date fields in the groupby_queries parameter.   |
| size                   | number                          | No       | The maximum number of items to return.             |
| offset                 | number                          | No       | The zero-based index of the first line item to return.          |
| seekOperation          | string                          | No       | Set seekOperation = Next to get the next page of analytics data.          |

 
**Request headers**

-   See [Headers](headers.md) for more information.

**Request body**

None.

**Request example**

```
GET https://api.partnercenter.microsoft.com/analytics/v1/{myorg}/subscriptions/groupby={termField1, dateField1, termField2, dateField2}&aggLevel=day HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105123
Content-Type: application/json
Content-Length: 0
```

## <span id="Response"></span><span id="response"></span><span id="RESPONSE"></span>REST Response


If successful, the response body contains a collection of [Subscription](#subscriptions) resources grouped by the specified terms and dates. Query Params are used for filtering data; aggregation level will apply to dates; aggregation supported by datesa

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
    "customerTenantId": "76906668-27FC-4F5B-A35C-75A9823E13AF",
    "customerName": "TESTORG65656565",
    "customerMarket": "US",
    "id": "4BF546B2-8998-4838-BEE2-5F1BBE65A04F",
    "status": "ACTIVE",
    "productName": "OFFICE 365 BUSINESS PREMIUM",
    "subscriptionType": "Office",
    "autoRenewEnabled": true,
    "partnerId": "3B33E682-00C3-41EE-9DD2-A548ADF56438",
    "friendlyName": "FULL OFFICE SUITE",
    "creationDate": "2016-02-04T19:29:38.037",
    "effectiveStartDate": "2016-02-04T00:00:00",
    "commitmentEndDate": "2019-02-10T00:00:00",
    "currentStateEndDate": "2019-02-10T00:00:00",
    "trialToPaidConversionDate": null,
    "trialStartDate": null,
    "trialEndDate": null,
    "lastUsageDate": null,
    "deprovisionedDate": null,
    "lastRenewalDate": "2018-02-10T02:39:57.729",
    "licenseCount": 2
}
```


# Subscription

**Applies To**

-   Partner Center
-   Partner Center operated by 21Vianet
-   Partner Center for Microsoft Cloud Germany
-   Partner Center for Microsoft Cloud for US Government

An analytics subscription resource contains all analytical data for a subscription. 



## <span id="Subscription"></span><span id="subscription"></span><span id="SUBSCRIPTION"></span>Subscription


Represents all analytical data for a subscription.
 
| Property                  | Type                              | Description                                                                             |
|---------------------------|-----------------------------------|-----------------------------------------------------------------------------------------|
| customerTenantId          | string                            | A GUID-formatted string that identifies the customer tenant.                            |
| customerName              | string                            | The name of the customer.                                                               |
| customerMarket            | string                            | The country/region that the customer does business in.                                  |
| id                        | string                            | The subscription identifier.                                                            |
| status                    | string                            | The subscription status:  "ACTIVE", "SUSPENDED", or "DEPROVISIONED".                    |
| productName               | string                            | The name of the product.                                                                |
| subscriptionType          | string                            | The subscription type: “Office”, “Azure”). **Note**: this field is case sensitive.      |
| autoRenewEnabled          | boolean                           | A value indicating whether the subscription is renewed automatically.                   |
| partnerId                 | string                            | The MPN ID of the partner.                                                              |
| friendlyName              | string                            | The name of the subscription.                                                           |
| creationDate              | string in UTC date time format    | The date the subscription was created.                                                  |
| effectiveStartDate        | string in UTC date time format    | The date the subscription starts.                                                       |
| commitmentEndDate         | string in UTC date time format    | The date the subscription ends.                                                         |
| currentStateEndDate       | string in UTC date time format    | The date that the current status of the subscription will change.                       |
| trialToPaidConversionDate | string in UTC date time format    | The date that the subscription converts from trial to paid. The default value is null.  |
| trialStartDate            | string in UTC date time format    | The date that the trial period for the subscription started. The default value is null. |
| trialEndDate              | string in UTC date time format    | The date that the trial period for the subscription ends. The default value is null.    |
| lastUsageDate             | string in UTC date time format    | The date that the subscription was last used. The default value is null.                |
| deprovisionedDate         | string in UTC date time format    | The date that the subscription was deprovisioned. The default value is null.            |
| lastRenewalDate           | string in UTC date time format    | The date that the subscription was last renewed The default value is null.              |
| licenseCount              | number                            | The total number of licenses.                                                           |
| subscriptionCount         | number                            | The number of subscriptions. Note: This value will only appear in the response of an aggregation query. See [Get subscription analytics by aggregation level](#get_subscription_analytics_by_aggregation_level).  |
