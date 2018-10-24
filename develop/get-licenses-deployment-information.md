---
title: Get licenses deployment information
description: How to get licenses deployment information aggregated to include all customers.
ms.assetid: BC78F9EA-C07C-4FD5-B06D-C87E8330B6E2
ms.date: 12/15/2017
ms.localizationpriority: medium
---

# Get licenses deployment information

**Applies To**

-   Partner Center

How to get licenses deployment information aggregated to include all customers.

## <span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>Prerequisites


Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with App+User credentials.


## <span id="Request"></span><span id="request"></span><span id="REQUEST"></span>Request

**Request syntax**

| Method  | Request URI                                                                                     |
|---------|-------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/analytics/commercial/deployment/license/ HTTP/1.1 |

 
**Request headers**

-   See [Partner Center REST headers](headers.md) for more information.  


**URI parameters**

| Parameter         | Type     | Description | Required |  
|-------------------|----------|-------------|----------|  
| top               | string   | The number of rows of data to return in the request. The maximum value and the default value if not specified is 10000. If there are more rows in the query, the response body includes a next link that you can use to request the next page of data. | No | 
| skip              | int      | The number of rows to skip in the query. Use this parameter to page through large data sets. For example, top=10000 and skip=0 retrieves the first 10000 rows of data, top=10000 and skip=10000 retrieves the next 10000 rows of data, and so on. | No | 
| filter            | string   | <p>The filter parameter of the request contains one or more statements that filter the rows in the response. Each statement contains a field and value that are associated with the **eq** or **ne** operators, and statements can be combined using **and** or **or**. Here are some example filter parameters:</p><ul><li><em>filter=serviceCode eq 'O365'</em></li><li><em>filter=serviceCode eq 'O365'</em> or (<em>channel eq 'Reseller'</em>)</li></ul><p>You can specify the following fields</p><ul><li><strong>serviceCode</strong></li><li><strong>serviceName</strong></li><li><strong>channel</strong></li><li><strong>customerTenantId</strong></li><li><strong>customerName</strong></li><li><strong>productId</strong></li><li><strong>productName</strong></li></ul> | No | 
| groupby           | string   | <p>A statement that applies data aggregation only to the specified fields. You can specify the following fields:</p><ul><li><strong>serviceCode</strong></li><li><strong>serviceName</strong></li><li><strong>channel</strong></li><li><strong>customerTenantId</strong></li><li><strong>customerName</strong></li><li><strong>productId</strong></li><li><strong>productName</strong></li></ul><p>The returned data rows will contain the fields specified in the groupby parameter as well as the following:</p><ul><li><strong>licensesDeployed</strong></li><li><strong>licensesSold</strong></li></ul> | No | 
| processedDateTime | DateTime | One can specify the date from which usage data was processed. Defaults to the latest date when the data was processed | No | 


**Request example**

```http

```


## <span id="Response"></span><span id="response"></span><span id="RESPONSE"></span>Response

If successful, the response body contains the following fields containing data about the licenses deployed.

| Field             | Type     | Description                           |
|-------------------|----------|---------------------------------------|
| serviceCode       | string   | Service Code                          |
| serviceName       | string   | Service Name                          |
| channel           | string   | Channel name, reseller                |
| customerTenantId  | string   | Unique identifier for the customer    |
| customerName      | string   | Customer name                         |
| productId         | string   | Unique identifier for the product     |
| productName       | string   | Product name                          |
| licensesDeployed  | long     | Number of licenses deployed           |
| licensesSold      | long     | Number of licenses sold               |
| processedDateTime | DateTime | Date when the data was last processed |



**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center REST error codes](error-codes.md).

**Response example**

```http

```