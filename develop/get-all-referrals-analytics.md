---
title: Get all referrals analytics information
description: How to get all the referrals analytics information.
ms.assetid: C6051714-1D8A-4448-9705-12AEC9A6420E
ms.date: 06/27/2018
ms.service: partner-dashboard
ms.subservice:  partnercenter-sdk
ms.localizationpriority: medium
---

# Get all referrals analytics information

**Applies To**

- Partner Center
- Partner Center for Microsoft Cloud Germany
- Partner Center for Microsoft Cloud for US Government

How to get all the referrals analytics information for your customers.

## Prerequisites

- Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with User credentials only.

## REST Request

### Request syntax

| Method  | Request URI |
|---------|-------------|
| **GET** | [*\{baseURL\}*](partner-center-rest-urls.md)/partner/v1/analytics/referrals HTTP/1.1 |

### URI parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| filter | string | Returns data matching the filter condition.</br> **Example:**</br>  `.../referrals?filter=field eq 'value'` |
| groupby | string | Supports both terms and dates. Short circuit logic to limit the number of buckets.</br> **Example:**</br>  `.../referrals?groupby=termField1,dateField1,termField2` |
| aggregationLevel | string | The *aggregationLevel* parameter requires a *groupby*. The *aggregationLevel* parameter applies to all date fields present in the *groupby*.</br> **Example:**</br> `.../referrals?groupby=termField1,dateField1,termField2&aggregationLevel=day` |
| top | string | The page limit is 10000. Takes any value less than 10000.</br> **Example:**</br> `.../referrals?top=100`</br> |
| skip | string | Number of rows to skip.</br> **Example:**</br>  `.../referrals?top=100&skip=100` |

### Request headers

For more information, see [Partner Center REST headers](headers.md).

### Request body

None.

### Request example

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/referrals HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## Response

If successful, the response body contains a collection of [Referrals](partner-center-analytics-resources.md#referrals-resource) resources.

### Response success and error codes

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Error Codes](error-codes.md).

### Response example

```http
{
  "id": "112310",
  "status": "Accepted",
  "customerMarket": "US",
  "customerName": "Best Customer Ever",
  "customerOrgSize": "10to50employees",
  "acceptedDate": "2018-02-07T23:43:19",
  "acknowledgedDate": "2018-02-07T23:40:50",
  "archivedDate": null,
  "declinedDate": null,
  "expiredDate": null,
  "lostDate": null,
  "missedDate": null,
  "createdDate": "2018-02-04T23:08:59",
  "skippedDate": null,
  "wonDate": null,
  "partnerMarket": "US"
}
```

## See also

- [Partner Center Analytics - Resources](partner-center-analytics-resources.md)
