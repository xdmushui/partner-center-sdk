---
title: Get all Azure usage analytics information
description: How to get all the Azure usage analytics information. 
author: Xansky
ms.author: mhopkins   
ms.assetid: CDBD04A4-BA34-49B8-9815-7C19253E6C70
robots: noindex,nofollow   
ms.date: 06/12/2018
ms.topic: article
ms.prod: partner-center
ms.technology: partner-center-sdk
---

# Get all Azure usage analytics information

>[!IMPORTANT]   
>This information relates to pre-released product which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here. 

**Applies To**

-   Partner Center
-   Partner Center operated by 21Vianet
-   Partner Center for Microsoft Cloud Germany
-   Partner Center for Microsoft Cloud for US Government


How to get all the Azure usage analytics information for your customers. 

## <span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>Prerequisites


-   Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with User credentials only. 

## <span id="Request"></span><span id="request"></span><span id="REQUEST"></span>REST Request


**Request syntax**

| Method  | Request URI                                                                                                                   |
|---------|-------------------------------------------------------------------------------------------------------------------------------|
| **GET** | [*\{baseURL\}*](partner-center-rest-urls.md)/partner/v1/analytics/azureusage |

 

**URI parameters**

<table>
 <tr>
  <th>
    <p>Parameter</p>
  </th>
  <th>
    <p>Type</p>
  </th>
  <th>
    <p>Description</p>
  </th>
  <th>
    <p>Required</p>
  </th>
  <th>
    <p>Case Sensitive</p>
  </th>
 </tr>
 <tr>
  <td>
    <p>top</p>
  </td>
  <td>
    <p>string</p>
  </td>
  <td>
    <p>The number of rows of data to return in the request. The maximum value and the
  default value if not specified is 10000. If there are more rows in the query,
  the response body includes a next link that you can use to request the next
  page of data.</p>
  </td>
  <td>
    <p>No</p>
  </td>
  <td>
    <p>&nbsp;</p>
  </td>
 </tr>
 <tr>
  <td>
    <p>skip</p>
  </td>
  <td>
    <p>int</p>
  </td>
  <td>
    <p>The number of rows to skip in the query. Use this parameter to page through large
  data sets. For example, top=10000 and skip=0 retrieves the first 10000 rows
  of data, top=10000 and skip=10000 retrieves the next 10000 rows of data, and
  so on.</p>
  </td>
  <td>
    <p>No</p>
  </td>
  <td>
    <p>&nbsp;</p>
  </td>
 </tr>
 <tr>
  <td>
    <p>filter</p>
  </td>
  <td>
    <p>string</p>
  </td>
  <td>
    <p>The <em>filter</em> parameter of the request
  contains one or more statements that filter the rows in the response. Each
  statement contains a field and value that are associated with the <strong>eq</strong> or <strong>ne</strong>
  operators, and statements can be combined using <strong>and</strong> or <strong>or</strong>. Here are some
  example <em>filter</em> parameters: </p>
  <ul>
   <li><em>filter=meterCategory eq</em> 'Data Management'</li>
   <li><em>filter=meterCategory eq</em> 'Data Management' <em>or (usage</em>Date <em>le
       cast('2018-01-01',Edm.DateTimeOffset) and usage</em>Date <em>le cast('2018-04-01',Edm.DateTimeOffset))</em></li>
  </ul>
  <p>You can specify the following fields</p>
  <ul>
   <li>customerTenantId</li>
   <li>customerName</li>
   <li>subscriptionId</li>
   <li>subscriptionName</li>
   <li>usageDate</li>
   <li>resourceLocation</li>
   <li>meterCategory</li>
   <li>meterSubcategory</li>
   <li>meterUnit</li>
   <li>reservationOrderId</li>
   <li>reservationId</li>
   <li>consumptionMeterId</li>
   <li>serviceType</li>
  </ul>
  </td>
  <td>
    <p>No</p>
  </td>
  <td>
    <p>&nbsp;</p>
  </td>
 </tr>
 <tr>
  <td>
    <p>aggregationLevel</p>
  </td>
  <td>
    <p>string</p>
  </td>
  <td>
    <p>Specifies the time range for which to retrieve aggregate data. Can be one of the
  following strings: <strong>day</strong>, <strong>week</strong>, or <strong>month</strong>.
  If unspecified, the default is <strong>day</strong>.</p>
  <p>aggregationLevel is not supported without a groupby. aggregationLevel applies to all date
  fields present in the groupby</p>
  </td>
  <td>
    <p>No</p>
  </td>
  <td>
    <p>&nbsp;</p>
  </td>
 </tr>
 <tr>
  <td>
    <p>orderby</p>
  </td>
  <td>
    <p>string</p>
  </td>
  <td>
    <p>A statement that orders the result data values for each install. The syntax is <em>orderby=field [order],field [order],...</em>. The
  <em>field</em> parameter can be one of the
  following strings:</p>
  <ul>
   <li>customerTenantId</li>
   <li>customerName</li>
   <li>subscriptionId</li>
   <li>subscriptionName</li>
   <li>usageDate</li>
   <li>resourceLocation</li>
   <li>meterCategory</li>
   <li>meterSubcategory</li>
   <li>meterUnit</li>
   <li>reservationOrderId</li>
   <li>reservationId</li>
   <li>consumptionMeterId</li>
   <li>serviceType</li>
  </ul>
  <p>The <em>order</em> parameter is optional, and can
  be <strong>asc</strong> or <strong>desc</strong> to specify ascending or descending order for each field.
  The default is <strong>asc</strong>.</p>
  <p>Example <em>orderby</em> string: <em>orderby=meterCategory,meterUnit</em></p>
  </td>
  <td>
    <p>No</p>
  </td>
  <td>
    <p>&nbsp;</p>
  </td>
 </tr>
 <tr>
  <td>
    <p>groupby</p>
  </td>
  <td>
    <p>string</p>
  </td>
  <td>
    <p>A statement that applies data aggregation only to the specified fields. You can
  specify the following fields:</p>
  <ul>
   <li>customerTenantId</li>
   <li>customerName</li>
   <li>subscriptionId</li>
   <li>subscriptionName</li>
   <li>usageDate</li>
   <li>resourceLocation</li>
   <li>meterCategory</li>
   <li>meterSubcategory</li>
   <li>meterUnit</li>
   <li>reservationOrderId</li>
   <li>reservationId</li>
   <li>consumptionMeterId</li>
   <li>serviceType</li>
  </ul>
  <p>&nbsp;</p>
  <p>The
  returned data rows will contain the fields specified in the <em>groupby</em> parameter as well as the following:</p>
  <ul>
   <li>Quantity</li>
  </ul>
  <p>&nbsp;</p>
  <p>The
  <em>groupby</em> parameter can be used with the
  <em>aggregationLevel</em> parameter. For
  example: <em>&amp;groupby=meterCategory,meterUnit</em></p>
  </td>
  <td>
    <p>No</p>
  </td>
  <td>
    <p>&nbsp;</p>
  </td>
 </tr>
 <tr>
  <td>
    <p>startDate</p>
  </td>
  <td>
  <p>DateTime</p>
  </td>
  <td>
    <p>One can specify the date from which usage is needed </p>
  </td>
  <td>
    <p>No</p>
  </td>
  <td>
    <p>&nbsp;</p>
  </td>
 </tr>
 <tr>
  <td>
    <p>endDate</p>
  </td>
  <td>
    <p>DateTime</p>
  </td>
  <td>
    <p>One can specify the date until which usage is needed </p>
  </td>
  <td>
    <p>No</p>
  </td>
  <td>
    <p>&nbsp;</p>
  </td>
 </tr>
</table>


**Request headers**

-   See [Headers](headers.md) for more information.

**Request body**

None.

**Request example**

```
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/azureusage
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <span id="Response"></span><span id="response"></span><span id="RESPONSE"></span>Response


If successful, the response body contains a collection of [Azure usage](partner-center-analytics.md#azure_usage) resources.

**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Error Codes](error-codes.md).

**Response example**

```
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
