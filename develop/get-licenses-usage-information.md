---
title: Get licenses usage information
description: How to get licenses usage information at the workload level for Office and Dynamics.
ms.date: 10/25/2018
ms.service: partner-dashboard
ms.subservice:  partnercenter-sdk
ms.localizationpriority: medium
---

# Get licenses usage information

**Applies To**

- Partner Center

How to get licenses usage information at the workload level for Office and Dynamics.

## <span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>Prerequisites


Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with App+User credentials.


## <span id="Request"/><span id="request"/><span id="REQUEST"/>Request

**Request syntax**

| Method  | Request URI                                                                                |
|---------|--------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/analytics/commercial/usage/license/ HTTP/1.1 |

 
**Request headers**

- See [Partner Center REST headers](headers.md) for more information.

**URI parameters**

| Parameter         | Type     | Description | Required |  
|-------------------|----------|-------------|----------|  
| top               | string   | The number of rows of data to return in the request. The maximum value and the default value if not specified is 10000. If there are more rows in the query, the response body includes a next link that you can use to request the next page of data. | No | 
| skip              | int      | The number of rows to skip in the query. Use this parameter to page through large data sets. For example, top=10000 and skip=0 retrieves the first 10000 rows of data, top=10000 and skip=10000 retrieves the next 10000 rows of data, and so on. | No | 
| filter            | string   | <p>The <em>filter</em> parameter of the request contains one or more statements that filter the rows in the response. Each statement contains a field and value that are associated with the **eq** or **ne** operators, and statements can be combined using **and** or **or**. Here are some example <em>filter</em> parameters:</p><ul><li><em>filter=workloadCode eq 'SFB'</em></li><li><em>filter=workloadCode eq 'SFB'</em> or (<em>channel eq 'Reseller'</em>)</li></ul><p>You can specify the following fields</p><ul><li><strong>workloadCode</strong></li><li><strong>workloadName</strong></li><li><strong>serviceCode</strong></li><li><strong>serviceName</strong></li><li><strong>channel</strong></li><li><strong>customerTenantId</strong></li><li><strong>customerName</strong></li><li><strong>productId</strong></li><li><strong>productName</strong></li></ul> | No | 
| groupby           | string   | <p>A statement that applies data aggregation only to the specified fields. You can specify the following fields:</p><ul><li><strong>workloadCode</strong></li><li><strong>workloadName</strong></li><li><strong>serviceCode</strong></li><li><strong>serviceName</strong></li><li><strong>channel</strong></li><li><strong>customerTenantId</strong></li><li><strong>customerName</strong></li><li><strong>productId</strong></li><li><strong>productName</strong></li></ul><p>The returned data rows will contain the fields specified in the <em>groupby</em> parameter as well as the following:</p><ul><li><strong>licensesActive</strong></li><li><strong>licensesQualified</strong></li></ul> | No | 
| processedDateTime | DateTime | One can specify the date from which usage data was processed. Defaults to the latest date when the data was processed | No | 


**Request example**

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/commercial/usage/license?filter=customerTenantId%20eq%20%270112A436-B14E-4888-967B-CA4BB2CF1234%27 HTTP 1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: bad5f75f-fd44-43ab-9325-bbc79dcba9da
MS-CorrelationId: 9cbdf63c-2608-4ad8-b0a9-abae27d859d9
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <span id="Response"/><span id="response"/><span id="RESPONSE"/>Response

If successful, the response body contains the following fields containing data about licenses usage.

| Field             | Type     | Description                                   |
|-------------------|----------|-----------------------------------------------|
| workloadCode      | string   | Workload code                                 |
| workloadName      | string   | Workload name                                 |
| serviceCode       | string   | Service code                                  |
| serviceName       | string   | Service name                                  |
| channel           | string   | Channel name, reseller                        |
| customerTenantId  | string   | Unique identifier for the customer            |
| customerName      | string   | Customer name                                 |
| productId         | string   | Unique identifier for the product             |
| productName       | string   | Product name                                  |
| licensesActive    | long     | Number of active licenses per workload        |
| licensesQualified | long     | Number of qualified licenses for the workload |
| processedDateTime | DateTime | Date when the data was last processed         |


**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center REST error codes](error-codes.md).

**Response example**

```http
HTTP/1.1 200 OK 
Content-Length: 487 
Content-Type: application/json; charset=utf-8 
MS-CorrelationId: 9cbdf63c-2608-4ad8-b0a9-abae27d859d9 
MS-RequestId: bad5f75f-fd44-43ab-9325-bbc79dcba9da 
MS-CV: f0trvmq8mEScHcFS.0 
MS-ServerId: 4 
Date: Wed, 24 Oct 2018 22:37:18 GMT

{
  
"Value": [
    {
      "processedDateTime": "2018-10-14T00:00:00",
      "workloadCode": "SPO",
      "workloadName": "SharePoint",
      "serviceCode": "o365",
      "serviceName": "Microsoft Office 365",
      "channel": "reseller",
      "customerTenantId": "0112A436-B14E-4888-967B-CA4BB2CF1234",
      "customerName": "TEST COMPANY",
      "productId": "6FD2C87F-B296-42F0-B197-1E91E994B900",
      "productName": "OFFICE 365 ENTERPRISE E3",
      "licenseActive": 0,
      "licensesQualified": 1
    },
    {
      "processedDateTime": "2018-10-14T00:00:00",
      "workloadCode": "EXO",
      "workloadName": "Exchange",
      "serviceCode": "o365",
      "serviceName": "Microsoft Office 365",
      "channel": "reseller",
      "customerTenantId": "0112A436-B14E-4888-967B-CA4BB2CF1234",
      "customerName": "TEST COMPANY",
      "productId": "45A2423B-E884-448D-A831-D9E139C52D2F",
      "productName": "EXCHANGE ONLINE PROTECTION",
      "licenseActive": 0,
      "licensesQualified": 1
    }
}
```