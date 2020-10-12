---
title: Get all Azure usage analytics information
description: How to get all the Azure usage analytics information.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice:  partnercenter-sdk
author: khpavan
ms.author: sakhanda
---

# Get all Azure usage analytics information

**Applies To**

- Partner Center
- Partner Center operated by 21Vianet
- Partner Center for Microsoft Cloud Germany
- Partner Center for Microsoft Cloud for US Government

How to get all the Azure usage analytics information for your customers.

## Prerequisites

- Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with User credentials only.

## REST request

### Request syntax

| Method  | Request URI |
|---------|-------------|
| **GET** | [*\{baseURL\}*](partner-center-rest-urls.md)/partner/v1/analytics/usage/azure HTTP/1.1 |

### URI parameters

|Parameter        |Type                        |Description               |
|:----------------|:---------------------------|:-------------------------|
|top              | string                     | The number of rows of data to return in the request. The maximum value and the default value if not specified is 10000. If there are more rows in the query, the response body includes a next link that you can use to request the next page of data.                        |
|skip             | int                        | The number of rows to skip in the query. Use this parameter to page through large data sets. For example, `top=10000 and skip=0` retrieves the first 10000 rows of data, `top=10000 and skip=10000` retrieves the next 10000 rows of data, and so on.                       |
|filter           | string                     | The *filter* parameter of the request contains one or more statements that filter the rows in the response. Each statement contains a field and value that are associated with the `eq` or `ne` operators, and statements can be combined using `and` or `or`. You can specify the following strings:<br/><br/>                                                       `customerTenantId`<br/> `customerName`<br/> `subscriptionId`<br/> `subscriptionName`<br/> `usageDate` <br/> `resourceLocation` <br/> `meterCategory` <br/> `meterSubcategory` <br/> `meterUnit`<br/> `reservationOrderId` <br/> `reservationId`<br/> `consumptionMeterId` <br/> `serviceType` <br/><br/>**Example:**<br/> `.../usage/azure?filter=meterCategory eq 'Data Management'`<br/><br/> **Example:**<br/>`.../usage/azure?filter=meterCategory eq 'Data Management' or (usageDate le cast('2018-01-01', Edm.DateTimeOffset) and usageDate le cast('2018-04-01', Edm.DateTimeOffset))`                        |
|aggregationLevel | string                    | Specifies the time range for which to retrieve aggregate data. Can be one of the following strings: `day`, `week`, or `month`. If unspecified, the default is `day`.<br/><br/>                                              The `aggregationLevel` parameter isn't supported without a `groupby`. The `aggregationLevel` parameter applies to all date fields present in the `groupby`.                                                      |
|orderby          |string                     | A statement that orders the result data values for each install. The syntax is `...&orderby=field [order],field [order],...`. The `field` parameter can be one of the following strings:<br/><br/>                    `customerTenantId`<br/>`customerName`<br/>`subscriptionId`<br/>`subscriptionName`<br/>`usageDate`<br/>`resourceLocation`<br/>`meterCategory`<br/>`meterSubcategory`<br/>`meterUnit`<br/> `reservationOrderId` <br/> `reservationId`<br/> `consumptionMeterId` <br/> `serviceType` <br/><br/> The *order* parameter is optional and can be `asc` or `desc` to specify ascending or descending order for each field, respectively. The default is `asc`.<br/><br/>**Example:**<br/> `...&orderby=meterCategory,meterUnit`                                                                                           |
|groupby          |string                    | A statement that applies data aggregation only to the specified fields. You can specify the following fields:<br/><br/>                                                                                                                     `customerTenantId`<br/>`customerName`<br/> `subscriptionId` <br/> `subscriptionName` <br/> `usageDate` <br/> `resourceLocation` <br/> `meterCategory` <br/> `meterSubcategory` <br/> `meterUnit` <br/> `reservationOrderId` <br/> `reservationId` <br/> `consumptionMeterId` <br/> `serviceType` <br/><br/>The returned data rows will contain the fields specified in the `groupby`  parameter as well as the *Quantity*.<br/><br/>The `groupby` parameter can be used with the `aggregationLevel` parameter.<br/><br/>**Example:**<br/>`...&groupby=meterCategory,meterUnit` |

### Request headers

For more information, see [Partner Center REST headers](headers.md).

### Request body

None.

### Request example

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/usage/azure HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## REST response

If successful, the response body contains a collection of [Azure usage](partner-center-analytics-resources.md#csp-program-azure-usage-analytics) resources.

### Response success and error codes

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Error Codes](error-codes.md).

### Response example

```http
{
  "customerTenantId": "39A1DFAC-4969-4F31-AF94-D76588189CFE",
  "customerName": "A",
  "subscriptionId": "EC649980-D623-49F5-B7C1-80CC772B83A8",
  "subscriptionName": "AZURE PURCHSE SAMPLE APP",
  "usageDate": "2018-05-27T00:00:00",
  "resourceLocation": "useast",
  "meterCategory": "Data Management",
  "meterSubcategory": "None",
  "meterUnit": "10,000s",
  "reservationOrderId": "",
  "reservationId": "",
  "consumptionMeterId": "",
  "serviceType": "",
  "quantity": 20
}
```

## See also

- [Partner Center Analytics - Resources](partner-center-analytics-resources.md)
