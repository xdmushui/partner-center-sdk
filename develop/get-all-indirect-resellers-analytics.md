---
title: Get all indirect resellers analytics information
description: How to get all the indirect resellers analytics information.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice:  partnercenter-sdk
author: khpavan
ms.author: sakhanda
---

# Get all indirect resellers analytics information

**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

How to get all the indirect resellers analytics information for your customers.

## Prerequisites

- Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with User credentials only.

## REST request

### Request syntax

| Method  | Request URI |
|---------|-------------|
| **GET** | [*\{baseURL\}*](partner-center-rest-urls.md)/partner/v1/analytics/indirectresellers HTTP/1.1 |

### URI parameters

| Parameter                             | Type     | Description                              |
|:--------------------------------------|:---------|:-----------------------------------------|
| partnerTenantId                       | string   | The Tenant ID of the partner for which you want to retrieve indirect resellers data. |
| id                                    | string   | Indirect reseller ID                                                                 |
| name                                  | string   | The Name of the partner for which you want to retrieve indirect resellers data.      |
| market                                | string   | The Market of the partner for which you want to retrieve indirect resellers data.    |
| firstSubscriptionCreationDate         | string in UTC date time format  | The creation date of the first subscription based on which you want to retrieve indirect resellers data.  |
| latestSubscriptionCreationDate        | string in UTC date time format  | The creation date of the latest subscription.                 |
| firstSubscriptionEndDate              | string in UTC date time format  | First time any subscription was ended.                        |
| latestSubscriptionEndDate             | string in UTC date time format  | Latest date when any subscription was ended.                  |
| firstSubscriptionSuspendedDate        | string in UTC date time         | First time any subscription was suspended.                    |
| latestSubscriptionSuspendedDate       | string in UTC date time format  | Latest date when any subscription was suspended.              |
| firstSubscriptionDeprovisionedDate    | string in UTC date time format  | First time any subscription was deprovisioned.                |
| latestSubscriptionDeprovisionedDate   | string in UTC date time format  | Latest date when any subscription was deprovisioned.          |
| subscriptionCount                     | double   | Subscription count for all value added resellers                                     |
| licenseCount                          | double   | License count for all value added resellers.                                         |
| indirectResellerCount                 | double   | Indirect resellers count                                                             |
|  top                                  | string   | The number of rows of data to return in the request. The maximum value and the default value if not specified is 10000. If there are more rows in the query, the response body includes a next link that you can use to request the next page of data.  |
| skip                                  | int      | The number of rows to skip in the query. Use this parameter to page through large data sets. For example, **`top=10000 and skip=0`** retrieves the first 10000 rows of data, **`top=10000 and skip=10000`** retrieves the next 10000 rows of data, and so on.              |
| filter                                | string   | The *filter* parameter of the request contains one or more statements that filter the rows in the response. Each statement contains a field and value that are associated with the **`eq`** or **`ne`** operators, and statements can be combined using **`and`** or **`or`**. You can specify the following fields:<br/><br/>     *partnerTenantId*<br/> *id*<br/> *Name*<br/>                *market*<br/> *firstSubscriptionCreationDate*<br/> *latestSubscriptionCreationDate*<br/>                *firstSubscriptionEndDate*<br/>                *latestSubscriptionEndDate*<br/>                *firstSubscriptionSuspendedDate*<br/>                *latestSubscriptionSuspendedDate*<br/>                *firstSubscriptionDeprovisionedDate*<br/>                *latestSubscriptionDeprovisionedDate*<br/><br/>         **Example:**<br/>              `.../indirectresellers?filter=market eq 'US'`<br/><br/>            **Example:**<br/>                `.../indirectresellers?filter=market eq 'US' or (firstSubscriptionCreationDate le cast('2018-01-01',Edm.DateTimeOffset) and firstSubscriptionCreationDate le cast('2018-04-01',Edm.DateTimeOffset))` |              
| aggregationLevel                     | string    | Specifies the time range for which to retrieve aggregate data. Can be one of the following strings: &quot;day&quot;, &quot;week&quot;, or &quot;month&quot;. If unspecified, the default is &quot;day&quot;.<br/><br/>                                 `aggregationLevel` isn't supported without a `aggregationLevel`. `aggregationLevel` applies to all **datefields** present in the `aggregationLevel`                         |
| orderby                              | string    | A statement that orders the result data values for each install. The syntax is `...&orderby=field[order],field [order],...`. The field parameter can be one of the following strings:<br/><br/>                &quot;partnerTenantId&quot;<br/>                &quot;id&quot;<br/>                &quot;name&quot;<br/>                &quot;market&quot;<br/>                &quot;firstSubscriptionCreationDate&quot;<br/>               &quot;latestSubscriptionCreationDate&quot;<br/>                &quot;firstSubscriptionEndDate&quot;<br/>               &quot;latestSubscriptionEndDate&quot;<br/>                &quot;firstSubscriptionSuspendedDate&quot;<br/>                &quot;latestSubscriptionSuspendedDate&quot;<br/>               &quot;firstSubscriptionDeprovisionedDate&quot;<br/>                &quot;latestSubscriptionDeprovisionedDate&quot;<br/>                &quot;subscriptionCount&quot;<br/>                &quot;licenseCount&quot;<br/><br/>   The *order* parameter is optional, and can be `asc` or `desc`; to specify ascending or descending order for each field. The default is `asc`.<br/><br/>    **Example:**<br/>                `...&orderby=market,subscriptionCount`                                       |                   
| groupby                              | string    | A statement that applies data aggregation only to the specified fields. You can specify the following fields:<br/><br/>         *partnerTenantId*<br/>    *id*<br/>               *Name*<br/>                *market*<br/>                *firstSubscriptionCreationDate*<br/>                *latestSubscriptionCreationDate*<br/>                *firstSubscriptionEndDate*<br/>                *latestSubscriptionEndDate*<br/>                *firstSubscriptionSuspendedDate*<br/>                *latestSubscriptionSuspendedDate*<br/>                *firstSubscriptionDeprovisionedDate*<br/>                *latestSubscriptionDeprovisionedDate*<br/><br/>                 The data rows returned contain the fields specified in the `groupby` clause, and the following fields:<br/><br/>            *indirectResellerCount*<br/>                *licenseCount*<br/>                *subscriptionCount*<br/><br/>            The `groupby` parameter can be used with the `aggregationLevel` parameter.<br/><br/>            **Example:**</br>               `...&groupby=ageGroup,market&aggregationLevel=week`                         |

### Request headers

For more information, see [Partner Center REST headers](headers.md).

### Request body

None.

### Request example

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/indirectresellers HTTP 1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## REST response

If successful, the response body contains a collection of [indirect resellers](partner-center-analytics-resources.md#csp-program-indirect-resellers-analytics) resources.

### Response success and error codes

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Error Codes](error-codes.md).

### Response example

```http
{
    "partnerTenantId": "AAAAAAAA-BBBB-CCCC-DDDD-EEEEEEEEEEEE",
    "id": "1111111",
    "name": "RESELLER NAME",
    "market": "US",
    "firstSubscriptionCreationDate": "2016-10-18T19:16:25.107",
    "latestSubscriptionCreationDate": "2016-10-18T19:16:25.107",
    "firstSubscriptionEndDate": "2018-11-07T00:00:00",
    "latestSubscriptionEndDate": "2018-11-07T00:00:00",
    "firstSubscriptionSuspendedDate": "0001-01-01T00:00:00",
    "latestSubscriptionSuspendedDate": "0001-01-01T00:00:00",
    "firstSubscriptionDeprovisionedDate": "0001-01-01T00:00:00",
    "latestSubscriptionDeprovisionedEndDate": "0001-01-01T00:00:00",
    "subscriptionCount": 10,
    "licenseCount": 20
}
```

## See also

- [Partner Center Analytics - Resources](partner-center-analytics-resources.md)
