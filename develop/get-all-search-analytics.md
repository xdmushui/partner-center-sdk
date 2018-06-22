---
title: Get all search analytics information
description: How to get all the search analytics information. 
author: Xansky
ms.author: mhopkins   
ms.assetid: CCF9D929-EE5F-4141-9884-ECA559A5171B
robots: noindex,nofollow   
ms.date: 06/21/2018
ms.topic: article
ms.prod: partner-center
ms.technology: partner-center-sdk
---

# Get all search analytics information

>[!IMPORTANT]   
>This information relates to pre-released product which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here. 

**Applies To**

-   Partner Center
-   Partner Center operated by 21Vianet
-   Partner Center for Microsoft Cloud Germany
-   Partner Center for Microsoft Cloud for US Government


How to get all the search analytics information for your customers. 

## <span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>Prerequisites


-   Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with User credentials only. 

## <span id="Request"></span><span id="request"></span><span id="REQUEST"></span>REST Request


**Request syntax**

| Method  | Request URI                                                                                                                   |
|---------|-------------------------------------------------------------------------------------------------------------------------------|
| **GET** | [*\{baseURL\}*](partner-center-rest-urls.md)/partner/v1/analytics/search |

 

**URI parameters**

| Parameter | Type | Description | Required |
|-----------|------|-------------|----------|
| filter | string | `/search?filter=field eq 'value'`</br>	Returns data matching the filter condition. | No |
| groupby | string | `/search?groupby=termField1, dateField1,termField2`</br>	Supports both terms and dates. Short circuit logic to limit the number of buckets. | No |
| aggregationLevel | string | `/search?groupby=termField1, dateField1,termField2&aggregationLevel=day`</br>	The *aggregationLevel* parameter requires a *groupby*. The *aggregationLevel* parameter applies to all date fields present in the *groupby*. | No |
| top | string | `/search?top=100`</br> The page limit is 10000. Takes any value less than 10000. |  |
| skip | string | `/search?top=100&skip=100`</br>	Number of rows to skip. | No |

  
<!--  
<table>
<thead>
  <th>Parameter</th><th>Type</th><th>Description</th><th>Required</th>
</thead>
 <tr>
  <td>
    <p>filter</p>
  </td>
  <td>
    <p>string</p>
  </td>
  <td>
    <p>The <em>filter</em> parameter of the request contains one or more statements that filter the rows in the response. Each statement contains a field and value that are associated with the <strong>eq</strong> or <strong>ne</strong> operators, and statements can be combined using <strong>and</strong> or <strong>or</strong>. Here are some example <em>filter</em> parameters: </p>
  <ul>
   <li><code>filter=meterCategory eq 'Data Management'</code></li>
   <li><code>filter=meterCategory eq 'Data Management' or (usageDate le cast('2018-01-01', Edm.DateTimeOffset) and usageDate le cast('2018-04-01', Edm.DateTimeOffset))</code></li>
  </ul>
  <p>You can specify the following fields:</p>
  <ul>
   <li><em>customerTenantId</em></li>
   <li><em>customerName</em></li>
   <li><em>subscriptionId</em></li>
   <li><em>subscriptionName</em></li>
   <li><em>usageDate</em></li>
   <li><em>resourceLocation</em></li>
   <li><em>meterCategory</em></li>
   <li><em>meterSubcategory</em></li>
   <li><em>meterUnit</em></li>
   <li><em>reservationOrderId</em></li>
   <li><em>reservationId</em></li>
   <li><em>consumptionMeterId</em></li>
   <li><em>serviceType</em></li>
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
    <p>groupby</p>
  </td>
  <td>
    <p>string</p>
  </td>
  <td>
    <p>A statement that applies data aggregation only to the specified fields. You can specify the following fields:</p>
  <ul>
   <li><em>customerTenantId</em></li>
   <li><em>customerName</em></li>
   <li><em>subscriptionId</em></li>
   <li><em>subscriptionName</em></li>
   <li><em>usageDate</em></li>
   <li><em>resourceLocation</em></li>
   <li><em>meterCategory</em></li>
   <li><em>meterSubcategory</em></li>
   <li><em>meterUnit</em></li>
   <li><em>reservationOrderId</em></li>
   <li><em>reservationId</em></li>
   <li><em>consumptionMeterId</em></li>
   <li><em>serviceType</em></li>
   
  </ul>
  <p>&nbsp;</p>
  <p>The
  returned data rows will contain the fields specified in the <em>groupby</em> parameter as well as the following:</p>
  <ul>
   <li><em>Quantity</em></li>
  </ul>
  <p>&nbsp;</p>
  <p>The <em>groupby</em> parameter can be used with the
  <em>aggregationLevel</em> parameter. For example:</br>
  <code>&amp;groupby=meterCategory,meterUnit</code></p>
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
    <p>Specifies the time range for which to retrieve aggregate data. Can be one of the following strings: "day", "week", or "month". If unspecified, the default is "day".</p>
  <p>The <em>aggregationLevel</em> parameter is not supported without a <em>groupby</em>. The <em>aggregationLevel</em> parameter applies to all date fields present in the <em>groupby</em>.</p>
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
    <p>top</p>
  </td>
  <td>
    <p>string</p>
  </td>
  <td>
    <p>The number of rows of data to return in the request. The maximum value and the default value if not specified is 10000. If there are more rows in the query, the response body includes a next link that you can use to request the next page of data.</p>
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
    <p>The number of rows to skip in the query. Use this parameter to page through large data sets. For example, <code>top=10000 and skip=0</code> retrieves the first 10000 rows of data, <code>top=10000 and skip=10000</code> retrieves the next 10000 rows of data, and so on.</p>
  </td>
  <td>
    <p>No</p>
  </td>
  <td>
    <p>&nbsp;</p>
  </td>
 </tr>
</table>
 -->

 
**Request headers**

-   See [Headers](headers.md) for more information.

**Request body**

None.

**Request example**

```
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/search
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <span id="Response"></span><span id="response"></span><span id="RESPONSE"></span>Response


If successful, the response body contains a collection of [Search](partner-center-analytics.md#search) resources.

**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Error Codes](error-codes.md).

**Response example**

```
{
  "companyName": "my company",
  "contactButtonClicked": false,
  "keywordCountry": null,
  "detailsViewed": true,
  "keywordIndustryFocus": null,
  "mpnId": 2604568,
  "partnerMarket": "CN",
  "keywordProduct": null,
  "referralSubmitted": false,
  "searchDate": "2018-05-30",
  "keywordSearchText": " my company"
}
```
