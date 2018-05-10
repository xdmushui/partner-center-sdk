---
title: Get subscription analytics grouped by dates or terms
description: How to get subscription analytics information grouped by dates or terms. 
ms.assetid: 
ms.author: v-thpr   
robots: noindex,nofollow   
ms.date: 05/10/2018 
ms.topic: article
ms.prod: partner-center
ms.technology: partner-center-sdk
---

# Get subscription analytics grouped by dates or terms

>[!IMPORTANT]   
>This information relates to pre-released product which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here. 

**Applies To**

-   Partner Center
-   Partner Center operated by 21Vianet
-   Partner Center for Microsoft Cloud Germany
-   Partner Center for Microsoft Cloud for US Government


How to get subscription analytics information for your customers grouped by dates or terms.

## <span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>Prerequisites


-   Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with User credentials only.


## <span id="Request"></span><span id="request"></span><span id="REQUEST"></span>REST Request


**Request syntax**

| Method  | Request URI                                                                                                                   |
|---------|-------------------------------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/partner/v1/analytics/subscriptions?groupby={groupby_queries} HTTP/1.1 |

 

**URI parameters**

Use the following path parameters to identify your organization and to group the results.

| Name                   | Type                            | Required | Description                                        |
|------------------------|---------------------------------|----------|----------------------------------------------------|
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
GET https://api.partnercenter.microsoft.com/analytics/v1/{myorg}/subscriptions/?filter{"Field":"customerName","Value":"TESTORG","Operator":"starts_with"} HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105123
Content-Type: application/json
Content-Length: 0
```

## <span id="Response"></span><span id="response"></span><span id="RESPONSE"></span>REST Response


If successful, the response body contains a collection of [Subscription](partner-center-analytics.md#subscription) resources grouped by the specified terms and dates.

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
