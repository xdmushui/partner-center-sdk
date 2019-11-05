---
title: Get licenses deployment information
description: How to get deployment information for Office and Dynamics licenses.
ms.date: 10/25/2018
ms.service: partner-dashboard
ms.subservice: PartnerCenterCSP
ms.localizationpriority: medium
---

# Get licenses deployment information

**Applies To**

- Partner Center

How to get deployment information for Office and Dynamics licenses.

## <span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>Prerequisites


Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with App+User credentials.


## <span id="Request"/><span id="request"/><span id="REQUEST"/>Request

**Request syntax**

| Method  | Request URI                                                                                     |
|---------|-------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/analytics/commercial/deployment/license/ HTTP/1.1 |

 
**Request headers**

- See [Partner Center REST headers](headers.md) for more information.  

**URI parameters**

| Parameter         | Type     | Description | Required |  
|-------------------|----------|-------------|----------|  
| top               | string   | The number of rows of data to return in the request. The maximum value and the default value if not specified is 10000. If there are more rows in the query, the response body includes a next link that you can use to request the next page of data. | No | 
| skip              | int      | The number of rows to skip in the query. Use this parameter to page through large data sets. For example, top=10000 and skip=0 retrieves the first 10000 rows of data, top=10000 and skip=10000 retrieves the next 10000 rows of data, and so on. | No | 
| filter            | string   | <p>The <em>filter</em> parameter of the request contains one or more statements that filter the rows in the response. Each statement contains a field and value that are associated with the **eq** or **ne** operators, and statements can be combined using **and** or **or**. Here are some example <em>filter</em> parameters:</p><ul><li><em>filter=serviceCode eq 'O365'</em></li><li><em>filter=serviceCode eq 'O365'</em> or (<em>channel eq 'Reseller'</em>)</li></ul><p>You can specify the following fields</p><ul><li><strong>serviceCode</strong></li><li><strong>serviceName</strong></li><li><strong>channel</strong></li><li><strong>customerTenantId</strong></li><li><strong>customerName</strong></li><li><strong>productId</strong></li><li><strong>productName</strong></li></ul> | No | 
| groupby           | string   | <p>A statement that applies data aggregation only to the specified fields. You can specify the following fields:</p><ul><li><strong>serviceCode</strong></li><li><strong>serviceName</strong></li><li><strong>channel</strong></li><li><strong>customerTenantId</strong></li><li><strong>customerName</strong></li><li><strong>productId</strong></li><li><strong>productName</strong></li></ul><p>The returned data rows will contain the fields specified in the <em>groupby</em> parameter as well as the following:</p><ul><li><strong>licensesDeployed</strong></li><li><strong>licensesSold</strong></li></ul> | No | 
| processedDateTime | DateTime | One can specify the date from which usage data was processed. Defaults to the latest date when the data was processed | No | 


**Request example**

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/commercial/deployment/license?filter=customerTenantId%20eq%20%270112A436-B14E-4888-967B-CA4BB2CF1234%27 HTTP 1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: bad5f75f-fd44-43ab-9325-bbc79dcba9da
MS-CorrelationId: 9cbdf63c-2608-4ad8-b0a9-abae27d859d9
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```


## <span id="Response"/><span id="response"/><span id="RESPONSE"/>Response

If successful, the response body contains the following fields containing data about the licenses deployed.

| Field             | Type     | Description                           |
|-------------------|----------|---------------------------------------|
| serviceCode       | string   | Service code                          |
| serviceName       | string   | Service name                          |
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
      "serviceCode": "crm",
      "serviceName": "Microsoft Dynamics",
      "channel": "reseller",
      "customerTenantId": "0112A436-B14E-4888-967B-CA4BB2CF1234",
      "customerName": "TEST COMPANY",
      "productId": "54B84594-9C77-4499-8D65-5E0D5F410E78",
      "productName": "DYNAMICS AX TASK",
      "licensesDeployed": 0,
      "licensesSold": 9
    },
    {
      "processedDateTime": "2018-10-14T00:00:00",
      "serviceCode": "o365",
      "serviceName": "Microsoft Office 365",
      "channel": "reseller",
      "customerTenantId": "0112A436-B14E-4888-967B-CA4BB2CF1234",
      "customerName": "TEST COMPANY",
      "productId": "D3B4FE1F-9992-4930-8ACB-CA6EC609365E",
      "productName": "DOMESTIC AND INTERNATIONAL CALLING PLAN",
      "licensesDeployed": 0,
      "licensesSold": 5
    }
],
  "@nextLink": null,
  "TotalCount": 2
}
```