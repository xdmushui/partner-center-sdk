---
title: Get all Azure usage analytics information
description: How to get all the Azure usage analytics information.
ms.assetid: CDBD04A4-BA34-49B8-9815-7C19253E6C70
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice:  partnercenter-sdk
ms.localizationpriority: medium
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

## REST Request

### Request syntax

| Method  | Request URI |
|---------|-------------|
| **GET** | [*\{baseURL\}*](partner-center-rest-urls.md)/partner/v1/analytics/usage/azure HTTP/1.1 |

### URI parameters

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
        <p>The <em>filter</em> parameter of the request contains one or more statements that filter the rows in the response. Each statement contains a field and value that are associated with the <strong><code>eq</code></strong> or <strong><code>ne</code></strong> operators, and statements can be combined using <strong><code>and</code></strong> or <strong><code>or</code></strong>. You can specify the following s:</p>
        <ul>
          <li><code>customerTenantId</code></li>
          <li><code>customerName</code></li>
          <li><code>subscriptionId</code></li>
          <li><code>subscriptionName</code></li>
          <li><code>usageDate</code></li>
          <li><code>resourceLocation</code></li>
          <li><code>meterCategory</code></li>
          <li><code>meterSubcategory</code></li>
          <li><code>meterUnit</code></li>
          <li><code>reservationOrderId</code></li>
          <li><code>reservationId</code></li>
          <li><code>consumptionMeterId</code></li>
          <li><code>serviceType</code></li>
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
        <p>Specifies the time range for which to retrieve aggregate data. Can be one of the following strings: <code>day</code>, <code>week</code>, or <code>month</code>. If unspecified, the default is <code>day</code>.</p>
      <p>The <code>aggregationLevel</code> parameter isn't supported without a <code>groupby</code>. The <code>aggregationLevel</code> parameter applies to all date fields present in the <code>groupby</code>.</p>
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
        <p>A statement that orders the result data values for each install. The syntax is <code>...&orderby=field [order],field [order],...</code>. The <code>field</code> parameter can be one of the following strings:</p>
        <ul>
          <li><code>customerTenantId</code></li>
          <li><code>customerName</code></li>
          <li><code>subscriptionId</code></li>
          <li><code>subscriptionName</code></li>
          <li><code>usageDate</code></li>
          <li><code>resourceLocation</code></li>
          <li><code>meterCategory</code></li>
          <li><code>meterSubcategory</code></li>
          <li><code>meterUnit</code></li>
          <li><code>reservationOrderId</code></li>
          <li><code>reservationId</code></li>
          <li><code>consumptionMeterId</code></li>
          <li><code>serviceType</code></li>
        </ul>
        <p>The <em>order</em> parameter is optional and can be <code>asc</code> or <code>desc</code>; to specify ascending or descending order for each field, respectively. The default is <code>asc</code>.</p>
        <p><strong>Example:</strong><br/>
          <code>...&orderby=meterCategory,meterUnit</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>groupby</code></p>
      </td>
      <td>
        <p>string</p>
      </td>
      <td>
        <p>A statement that applies data aggregation only to the specified fields. You can specify the following fields:</p>
        <ul>
          <li><code>customerTenantId</code></li>
          <li><code>customerName</code></li>
          <li><code>subscriptionId</code></li>
          <li><code>subscriptionName</code></li>
          <li><code>usageDate</code></li>
          <li><code>resourceLocation</code></li>
          <li><code>meterCategory</code></li>
          <li><code>meterSubcategory</code></li>
          <li><code>meterUnit</code></li>
          <li><code>reservationOrderId</code></li>
          <li><code>reservationId</code></li>
          <li><code>consumptionMeterId</code></li>
          <li><code>serviceType</code></li>
        </ul>
        <p>The returned data rows will contain the fields specified in the <code>groupby</code> parameter as well as the <em>Quantity</em>.</p>
        <p>The <code>groupby</code> parameter can be used with the
        <code>aggregationLevel</code> parameter.</p>
        <p><strong>Example:</strong></br>
          <code>...&groupby=meterCategory,meterUnit</code>
        </p>
      </td>
    </tr>
  </tbody>
</table>

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

## Response

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
