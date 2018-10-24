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


<!-- 
## <span id="C_"></span><span id="c_"></span>C#

To retrieve aggregated data on licenses deployment, first get an interface to partner level analytics collection operations from the [**IAggregatePartner.Analytics**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.ipartner.analytics) property. Then retrieve an interface to the partner level licenses analytics collection from the [**Licenses**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.analytics.ipartneranalyticscollection.licenses) property. Finally, call the [**Deployment.Get**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) method to get the aggregated data on licenses deployment. If the method succeeds you'll get a collection of [**PartnerLicensesDeploymentInsights**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.analytics.partnerlicensesdeploymentinsights) objects.

``` csharp
// IAggregatePartner partnerOperations;

var partnerLicensesDeploymentAnalytics = partnerOperations.Analytics.Licenses.Deployment.Get();
```
 -->

## <span id="Request"></span><span id="request"></span><span id="REQUEST"></span>Request

**Request syntax**

| Method  | Request URI                                                                                     |
|---------|-------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/analytics/commercial/deployment/license/ HTTP/1.1 |

 
**Request headers**

-   See [Partner Center REST headers](headers.md) for more information.  


**Request body**

| Parameter         | Type     | Description | Required |  
|-------------------|----------|-------------|----------|  
| top               | string   | The number of rows of data to return in the request. The maximum value and the default value if not specified is 10000. If there are more rows in the query, the response body includes a next link that you can use to request the next page of data. | No | 
| skip              | int      | The number of rows to skip in the query. Use this parameter to page through large data sets. For example, top=10000 and skip=0 retrieves the first 10000 rows of data, top=10000 and skip=10000 retrieves the next 10000 rows of data, and so on. | No | 
| filter            | string   | <p>The filter parameter of the request contains one or more statements that filter the rows in the response. Each statement contains a field and value that are associated with the **eq** or **ne** operators, and statements can be combined using **and** or **or**. Here are some example filter parameters:</p><ul><li><em>filter=serviceCode eq 'O365'</em></li><li><em>filter=serviceCode eq 'O365'</em> or (<em>channel eq 'Reseller'</em>)</li></ul><p>You can specify the following fields</p><ul><li><strong>serviceCode</strong></li><li><strong>serviceName</strong></li><li><strong>channel</strong></li><li><strong>customerTenantId</strong></li><li><strong>customerName</strong></li><li><strong>productId</strong></li><li><strong>productName</strong></li></ul> | No | 
| groupby           | string   | <p>A statement that applies data aggregation only to the specified fields. You can specify the following fields:</p><ul><li><strong>serviceCode</strong></li><li><strong>serviceName</strong></li><li><strong>channel</strong></li><li><strong>customerTenantId</strong></li><li><strong>customerName</strong></li><li><strong>productId</strong></li><li><strong>productName</strong></li></ul><p>The returned data rows will contain the fields specified in the groupby parameter as well as the following:</p><ul><li><strong>licensesDeployed</strong></li><li><strong>licensesSold</strong></li></ul> | No | 
| processedDateTime | DateTime | One can specify the date from which usage data was processed. Defaults to the latest date when the data was processed | No | 



**Request example**

```http
GET https://api.partnercenter.microsoft.com/v1/analytics/commercial/deployment/license/ HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 25b6edd5-1f53-456b-b48c-c64f60ec2dda
MS-CorrelationId: 6492b9d6-5629-429b-934c-040b1946e760
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```


## <span id="Response"></span><span id="response"></span><span id="RESPONSE"></span>Response

If successful, the response body contains a collection of [CustomerLicensesDeploymentInsights](analytics.md#customerlicensesdeploymentinsights) resources that provide information about the licenses deployed.

**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center REST error codes](error-codes.md).

**Response example**

```http
HTTP/1.1 200 OK
Content-Length: 487
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 6492b9d6-5629-429b-934c-040b1946e760
MS-RequestId: 25b6edd5-1f53-456b-b48c-c64f60ec2dda
MS-CV: f0trvmq8mEScHcFS.0
MS-ServerId: 102030524
Date: Tue, 14 Mar 2017 17:55:01 GMT

{
  "Value": [
    {
      "processedDateTime": "2018-10-02T00:00:00",
      "serviceCode": "o365",
      "serviceName": "Microsoft Office 365",
      "channel": "reseller",
      "customerTenantId": "4F9D7DF5-8EBD-4973-B221-013976C1078A",
      "customerName": "LARACHOTEST123",
      "productId": "D42C793F-6C78-4F43-92CA-E8F6A02B035F",
      "productName": "SKYPE FOR BUSINESS ONLINE (PLAN 2)",
      "licensesDeployed": 0,
      "licensesSold": 2
    },
    {
      "processedDateTime": "2018-10-02T00:00:00",
      "serviceCode": "o365",
      "serviceName": "Microsoft Office 365",
      "channel": "reseller",
      "customerTenantId": "4FD49354-715A-4B49-9079-A77AE978D1DC",
      "customerName": "TESTORG",
      "productId": "CDD28E44-67E3-425E-BE4C-737FAB2899D3",
      "productName": "OFFICE 365 BUSINESS",
      "licensesDeployed": 0,
      "licensesSold": 2
    }
],
  "@nextLink": null,
  "TotalCount": 2
}
```