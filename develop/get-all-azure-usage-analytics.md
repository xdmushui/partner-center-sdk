---
title: Get all Azure usage analytics information
description: How to get all the Azure usage analytics information. 
ms.assetid: CDBD04A4-BA34-49B8-9815-7C19253E6C70
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: PartnerCenterCSP
ms.localizationpriority: medium
---

# Get all Azure usage analytics information

**Applies To**

- Partner Center
- Partner Center operated by 21Vianet
- Partner Center for Microsoft Cloud Germany
- Partner Center for Microsoft Cloud for US Government


How to get all the Azure usage analytics information for your customers. 

## <span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>Prerequisites


- Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with User credentials only. 

## <span id="Request"/><span id="request"/><span id="REQUEST"/>REST Request


**Request syntax**

| Method  | Request URI |
|---------|-------------|
| **GET** | [*\{baseURL\}*](partner-center-rest-urls.md)/partner/v1/analytics/usage/azure HTTP/1.1 |

 

**URI parameters**

<table>
  <thead>
      <th>
        <p>Parameter</p>
      </th>
      <th>
        <p>Type</p>
      </th>
      <th>
        <p>Description</p>
      </th>
  </thead>
  <tbody>
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
    </tr>
    <tr>
      <td>
        <p>filter</p>
      </td>
      <td>
        <p>string</p>
      </td>
      <td>
        <p>The <em>filter</em> parameter of the request contains one or more statements that filter the rows in the response. Each statement contains a field and value that are associated with the <strong>eq</strong> or <strong>ne</strong> operators, and statements can be combined using <strong>and</strong> or <strong>or</strong>. You can specify the following fields:</p>
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
        <p><strong>Example:</strong></br>
          <code>.../usage/azure?filter=meterCategory eq &#39;Data Management&#39;</code>
        </p>
        <p><strong>Example:</strong></br>
          <code>.../usage/azure?filter=meterCategory eq &#39;Data Management&#39; or (usageDate le cast(&#39;2018-01-01&#39;, Edm.DateTimeOffset) and usageDate le cast(&#39;2018-04-01&#39;, Edm.DateTimeOffset))</code>
        </p>
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
        <p>Specifies the time range for which to retrieve aggregate data. Can be one of the following strings: &quot;day&quot;, &quot;week&quot;, or &quot;month&quot;. If unspecified, the default is &quot;day&quot;.</p>
      <p>The <em>aggregationLevel</em> parameter is not supported without a <em>groupby</em>. The <em>aggregationLevel</em> parameter applies to all date fields present in the <em>groupby</em>.</p>
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
        <p>A statement that orders the result data values for each install. The syntax is <code>...&orderby=field [order],field [order],...</code> The <em>field</em> parameter can be one of the following strings:</p>
        <ul>
          <li>&quot;customerTenantId&quot;</li>
          <li>&quot;customerName&quot;</li>
          <li>&quot;subscriptionId&quot;</li>
          <li>&quot;subscriptionName&quot;</li>
          <li>&quot;usageDate&quot;</li>
          <li>&quot;resourceLocation&quot;</li>
          <li>&quot;meterCategory&quot;</li>
          <li>&quot;meterSubcategory&quot;</li>
          <li>&quot;meterUnit&quot;</li>
          <li>&quot;reservationOrderId&quot;</li>
          <li>&quot;reservationId&quot;</li>
          <li>&quot;consumptionMeterId&quot;</li>
          <li>&quot;serviceType&quot;</li>
        </ul>
        <p>The <em>order</em> parameter is optional and can be &quot;asc&quot; or &quot;desc&quot; to specify ascending or descending order for each field, respectively. The default is &quot;asc&quot;.</p>
        <p><strong>Example:</strong><br/> 
          <code>...&orderby=meterCategory,meterUnit</code>
        </p>
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
        <p>The returned data rows will contain the fields specified in the <em>groupby</em> parameter as well as the <em>Quantity</em>.</p>
        <p>The <em>groupby</em> parameter can be used with the
        <em>aggregationLevel</em> parameter.</p>
        <p><strong>Example:</strong></br>
          <code>...&groupby=meterCategory,meterUnit</code>
        </p>
      </td>
    </tr>
  </tbody>
</table>


**Request headers**

- See [Headers](headers.md) for more information.

**Request body**

None.

**Request example**

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/usage/azure HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <span id="Response"/><span id="response"/><span id="RESPONSE"/>Response


If successful, the response body contains a collection of [Azure usage](partner-center-analytics-resources.md#azure_usage) resources.

**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Error Codes](error-codes.md).

**Response example**

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


## <span id="See_Also"/><span id="see_also"/><span id="SEE_ALSO"/>See also
  - [Partner Center Analytics - Resources](partner-center-analytics-resources.md)

