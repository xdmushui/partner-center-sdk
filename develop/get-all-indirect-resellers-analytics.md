---
title: Get all indirect resellers analytics information
description: How to get all the indirect resellers analytics information. 
ms.assetid: CCF9D929-EE5F-4141-9884-ECA559A5171B
ms.date: 06/22/2018
ms.localizationpriority: medium
---

# Get all indirect resellers analytics information

**Applies To**

-   Partner Center
-   Partner Center operated by 21Vianet
-   Partner Center for Microsoft Cloud Germany
-   Partner Center for Microsoft Cloud for US Government


How to get all the indirect resellers analytics information for your customers. 

## <span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>Prerequisites


-   Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with User credentials only. 

## <span id="Request"></span><span id="request"></span><span id="REQUEST"></span>REST Request


**Request syntax**

| Method  | Request URI |
|---------|-------------|
| **GET** | [*\{baseURL\}*](partner-center-rest-urls.md)/partner/v1/analytics/indirectresellers HTTP/1.1 |

 

**URI parameters**

<table>
<thead>
	<th>Parameter</th>
	<th>Type</th>
	<th>Description</th>
</thead>
<tbody>
	<tr>
		<td>partnerTenantId</td>
		<td>string</td>
		<td>The Tenant ID of the partner for which you want to retrieve indirect resellers data. </td>
	</tr>
	<tr>
		<td>id</td>
		<td>string</td>
		<td>Indirect reseller ID</td>
	</tr>
	<tr>
		<td>name</td>
		<td>string</td>
		<td>The Name of the partner for which you want to retrieve indirect resellers data.</td>
	</tr>
	<tr>
		<td>market</td>
		<td>string</td>
		<td>The Market of the partner for which you want to retrieve indirect resellers data.</td>
	</tr>
	<tr>
		<td>firstSubscriptionCreationDate</td>
		<td>string in UTC date time format</td>
		<td>The creation date of the first subscription based on which you want to retrieve indirect resellers data.</td>
	</tr>
	<tr>
		<td>latestSubscriptionCreationDate</td>
		<td>string in UTC date time format</td>
		<td>The creation date of the latest subscription.</td>
	</tr>
	<tr>
		<td>firstSubscriptionEndDate</td>
		<td>string in UTC date time format</td>
		<td>First time any subscription was ended.</td>
	</tr>
	<tr>
		<td>latestSubscriptionEndDate</td>
		<td>string in UTC date time format</td>
		<td>Latest date when any subscription was ended. </td>
	</tr>
	<tr>
		<td>firstSubscriptionSuspendedDate</td>
		<td>string in UTC date time format</td>
		<td>First time any subscription was suspended.</td>
	</tr>
	<tr>
		<td>latestSubscriptionSuspendedDate</td>
		<td>string in UTC date time format</td>
		<td>Latest date when any subscription was suspended.</td>
	</tr>
	<tr>
		<td>firstSubscriptionDeprovisionedDate</td>
		<td>string in UTC date time format</td>
		<td>First time any subscription was deprovisioned.</td>
	</tr>
	<tr>
		<td>latestSubscriptionDeprovisionedDate</td>
		<td>string in UTC date time format</td>
		<td>Latest date when any subscription was deprovisioned.</td>
	</tr>
	<tr>
		<td>subscriptionCount</td>
		<td>double</td>
		<td>Subscription count for all value added resellers</td>
	</tr>
	<tr>
		<td>licenseCount</td>
		<td>double</td>
		<td>License count for all value added resellers</td>
	</tr>
	<tr>
		<td>indirectResellerCount</td>
		<td>double</td>
		<td>Indirect resellers count</td>
	</tr>
	<tr>
		<td>top</td>
		<td>string</td>
		<td>The number of rows of data to return in the request. The maximum value and the default value if not specified is 10000. If there are more rows in the query, the response body includes a next link that you can use to request the next page of data.</td>
	</tr>
	<tr>
		<td>skip</td>
		<td>int</td>
		<td>
		  <p>The number of rows to skip in the query. Use this parameter to page through large data sets. For example, <code>top=10000 and skip=0</code> retrieves the first 10000 rows of data, <code>top=10000 and skip=10000</code> retrieves the next 10000 rows of data, and so on.</p>
		</td>
	</tr>
	<tr>
		<td>filter</td>
		<td>string</td>
		<td>
			<p>The <em>filter</em> parameter of the request contains one or more statements that filter the rows in the response. Each statement contains a field and value that are associated with the <strong>eq</strong> or <strong>ne</strong> operators, and statements can be combined using <strong>and</strong> or <strong>or</strong>. You can specify the following fields:</p>
			<ul>
				<li><em>partnerTenantId</em></li>
				<li><em>id</em></li>
				<li><em>Name</em></li>
				<li><em>market</em></li>
				<li><em>firstSubscriptionCreationDate</em></li>
				<li><em>latestSubscriptionCreationDate</em></li>
				<li><em>firstSubscriptionEndDate</em></li>
				<li><em>latestSubscriptionEndDate</em></li>
				<li><em>firstSubscriptionSuspendedDate</em></li>
				<li><em>latestSubscriptionSuspendedDate</em></li>
				<li><em>firstSubscriptionDeprovisionedDate</em></li>
				<li><em>latestSubscriptionDeprovisionedDate</em></li>
			</ul>
			<p><strong>Example:</strong></br>
			  <code>.../indirectresellers?filter=market eq 'US'</code></p>
			<p><strong>Example:</strong></br>
				<code>.../indirectresellers?filter=market eq 'US' or (firstSubscriptionCreationDate le cast('2018-01-01',Edm.DateTimeOffset) and firstSubscriptionCreationDate le cast('2018-04-01',Edm.DateTimeOffset))</code>
			</p>
	    </td>
	</tr>
	<tr>
		<td>aggregationLevel</td>
		<td>string</td>
		<td><p>Specifies the time range for which to retrieve aggregate data. Can be one of the following strings: "day", "week", or "month". If unspecified, the default is "day".</p>
		<p><em>aggregationLevel</em> is not supported without a <strong>groupby</strong>. <em>aggregationLevel</em> applies to all <strong>datefields</strong> present in the <strong>groupby</strong></p>
		</td>
	</tr>
	<tr>
		<td>orderby</td>
		<td>string</td>
		<td>
			<p>A statement that orders the result data values for each install. The syntax is <code>...&amp;orderby=field[order],field [order],...</code> The field parameter can be one of the following strings:</p>
			<ul>
				<li>"partnerTenantId"</li> 
				<li>"id"</li> 
				<li>"name"</li> 
				<li>"market"</li> 
				<li>"firstSubscriptionCreationDate"</li> 
				<li>"latestSubscriptionCreationDate"</li> 
				<li>"firstSubscriptionEndDate"</li> 
				<li>"latestSubscriptionEndDate"</li> 
				<li>"firstSubscriptionSuspendedDate"</li> 
				<li>"latestSubscriptionSuspendedDate"</li> 
				<li>"firstSubscriptionDeprovisionedDate"</li> 
				<li>"latestSubscriptionDeprovisionedDate"</li>
				<li>"subscriptionCount"</li> 
				<li>"licenseCount"</li>
			</ul>
			<p>The <em>order</em> parameter is optional, and can be "asc" or "desc" to specify ascending or descending order for each field. The default is "asc".</p>
			<p><strong>Example:</strong></br> 
				<code>...&amp;orderby=market,subscriptionCount</code>
			</p> 
		</td>
	</tr>
	<tr>
		<td>groupby</td>
		<td>string</td>
		<td>
			<p>A statement that applies data aggregation only to the specified fields. You can specify the following fields:</p>
			<ul>
				<li><em>partnerTenantId</em></li>
				<li><em>id</em></li>
				<li><em>Name</em></li>
				<li><em>market</em></li>
				<li><em>firstSubscriptionCreationDate</em></li>
				<li><em>latestSubscriptionCreationDate</em></li>
				<li><em>firstSubscriptionEndDate</em></li>
				<li><em>latestSubscriptionEndDate</em></li>
				<li><em>firstSubscriptionSuspendedDate</em></li>
				<li><em>latestSubscriptionSuspendedDate</em></li>
				<li><em>firstSubscriptionDeprovisionedDate</em></li>
				<li><em>latestSubscriptionDeprovisionedDate</em></li>
			</ul>
			<p>The returned data rows will contain the fields specified in the <em>groupby</em> parameter as well as the following:</p>
			<ul>
				<li><em>indirectResellerCount</em></li>
				<li><em>licenseCount</em></li>
				<li><em>subscriptionCount</em></li>
			</ul>
			<p>The <em>groupby</em> parameter can be used with the <em>aggregationLevel</em> parameter.</p>
			<p><strong>Example:</strong></br>
				<code>...&amp;groupby=ageGroup,market&amp;aggregationLevel=week</code>
			</p>
		</td>
	</tr>
</tbody>
</table>
 

**Request headers**

-   See [Headers](headers.md) for more information.

**Request body**

None.

**Request example**

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/indirectresellers HTTP 1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <span id="Response"></span><span id="response"></span><span id="RESPONSE"></span>Response


If successful, the response body contains a collection of [indirect resellers](partner-center-analytics-resources.md#indirect_resellers) resources.

**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Error Codes](error-codes.md).

**Response example**

```http
{ 
    "partnerTenantId": "AAAAAAAA-BBBB-CCCC-DDDD-EEEEEEEEEEEE", 
    "id": "1111111", 
    "name": "RESELLER NAME", 
    "market": "US", 
    "firstSubscriptionCreationDate": "2016-10-18T19:16:25.107", 
    "latestSubscriptionCreationDate": "2016-10-18T19:16:25.107", 
    "firstSubscriptionEndDate": "2018-11-07T00:00:00", 
    "latestSubscriptionEndDate": "2018-11-07T00:00:00", 
    "firstSubscriptionSuspendedDate": "0001-01-01T00:00:00", 
    "latestSubscriptionSuspendedDate": "0001-01-01T00:00:00", 
    "firstSubscriptionDeprovisionedDate": "0001-01-01T00:00:00", 
    "latestSubscriptionDeprovisionedEndDate": "0001-01-01T00:00:00", 
    "subscriptionCount": 10, 
    "licenseCount": 20 
}
```


## <span id="See_Also"></span><span id="see_also"></span><span id="SEE_ALSO"></span>See also
 - [Partner Center Analytics - Resources](partner-center-analytics-resources.md)
