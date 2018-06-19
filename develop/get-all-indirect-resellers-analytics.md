---
title: Get all indirect resellers analytics information
description: How to get all the indirect resellers analytics information. 
author: Xansky
ms.author: mhopkins   
ms.assetid: CCF9D929-EE5F-4141-9884-ECA559A5171B
robots: noindex,nofollow   
ms.date: 06/12/2018
ms.topic: article
ms.prod: partner-center
ms.technology: partner-center-sdk
---

# Get all indirect resellers analytics information

>[!IMPORTANT]   
>This information relates to pre-released product which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here. 

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

| Method  | Request URI                                                                                                                   |
|---------|-------------------------------------------------------------------------------------------------------------------------------|
| **GET** | [*\{baseURL\}*](partner-center-rest-urls.md)/partner/v1/analytics/indirectresellers |

 

**URI parameters**

<table>
<thead>
	<tr>
		<th>Parameter</th>
		<th>Type</th>
		<th>Description</th>
	</tr>
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
		<td>date</td>
		<td>The creation date of the first subscription based on which you want to retrieve indirect resellers data.</td>
	</tr>
	<tr>
		<td>latestSubscriptionCreationDate</td>
		<td>Date</td>
		<td>The creation date of the latest subscription.</td>
	</tr>
	<tr>
		<td>firstSubscriptionEndDate</td>
		<td>Date</td>
		<td>First time any subscription was ended.</td>
	</tr>
	<tr>
		<td>latestSubscriptionEndDate</td>
		<td>Date</td>
		<td>Latest date when any subscription was ended. </td>
	</tr>
	<tr>
		<td>firstSubscriptionSuspendedDate</td>
		<td>Date</td>
		<td>First time any subscription was suspended.</td>
	</tr>
	<tr>
		<td>latestSubscriptionSuspendedDate</td>
		<td>Date</td>
		<td>Latest date when any subscription was suspended.</td>
	</tr>
	<tr>
		<td>firstSubscriptionDeprovisionedDate</td>
		<td>Date</td>
		<td>First time any subscription was deprovisioned.</td>
	</tr>
	<tr>
		<td>latestSubscriptionDeprovisionedDate</td>
		<td>Date</td>
		<td>Latest date when any subscription was deprovisioned.</td>
	</tr>
	<tr>
		<td>subscriptionCount</td>
		<td>Double</td>
		<td>Subscription count for all value added resellers</td>
	</tr>
	<tr>
		<td>licenseCount</td>
		<td>Double</td>
		<td>License count for all value added resellers</td>
	</tr>
	<tr>
		<td>indirectResellerCount</td>
		<td>Double</td>
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
		<td>The number of rows to skip in the query. Use this parameter to page through large data sets. For example, top=10000 and skip=0 retrieves the first 10000 rows of data,top=10000 and skip=10000 retrieves the next 10000 rows of data, and so on.</td>
	</tr>
	<tr>
		<td>filter</td>
		<td>string</td>
		<td><p>The <em>filter</em> parameter of the request contains one or more statements that filter the rows in the response. Each statement contains a field and value that are associated with the eq or ne operators, and statements can be combined using and or or. Here are some example filter parameters:</p>
		<ul>
		    <li>filter=market eq 'US'</li>
		    <li><em>filter=market eq 'US' or (</em>firstSubscriptionCreationDate <em>le cast('2018-01-01',Edm.DateTimeOffset) and </em> firstSubscriptionCreationDate <em>le      cast('2018-04-01',Edm.DateTimeOffset))</em></li> 
		</ul> 
		<p>You can specify the following fields:</p>
		<ul>
		    <li>partnerTenantId</li>
		    <li>id</li>
		    <li>Name</li>
		    <li>market</li>
		    <li>firstSubscriptionCreationDate</li>
		    <li>latestSubscriptionCreationDate</li>
		    <li>firstSubscriptionEndDate</li>
		    <li>latestSubscriptionEndDate</li>
		    <li>firstSubscriptionSuspendedDate</li>
		    <li>latestSubscriptionSuspendedDate</li>
		    <li>firstSubscriptionDeprovisionedDate</li>
		    <li>latestSubscriptionDeprovisionedDate</li>
		 </ul>
	    </td>
	</tr>
	<tr>
		<td>aggregationLevel</td>
		<td>string</td>
		<td><p>Specifies the time range for which to retrieve aggregate data. Can be one of the following strings: day, week, or month. If unspecified, the default is day.</p>
		<p><em>aggregationLevel</em> is not supported without a <strong>groupby</strong>. <em>aggregationLevel</em> applies to all <strong>datefields</strong> present in the <strong>groupby</strong></p>
		</td>
	</tr>
	<tr>
		<td>orderby</td>
		<td>string</td>
		<td>A statement thatorders the result data values for each install. The syntax is orderby=field[order],field [order],.... The field parameter can be one of the followingstrings:</p>
		<ul>
    		<li>partnerTenantId</li> 
    		<li>id</li> 
    		<li>name</li> 
    		<li>market</li> 
    		<li>firstSubscriptionCreationDate</li> 
    		<li>latestSubscriptionCreationDate</li> 
    		<li>firstSubscriptionEndDate</li> 
    		<li>latestSubscriptionEndDate</li> 
    		<li>firstSubscriptionSuspendedDate</li> 
    		<li>latestSubscriptionSuspendedDate</li> 
    		<li>firstSubscriptionDeprovisionedDate</li> 
    		<li>latestSubscriptionDeprovisionedDate</li>
    		<li>subscriptionCount</li> 
    		<li>licenseCount</li>
		</ul>
		<p>The <em>order</em> parameter is optional, and can be "asc" or "desc" to specify ascending or descending order for each field. The default is "asc".</p>
		<p>Example <em>orderby</em> string: <em>orderby=market,subscriptionCount</em> </td>
	</tr>
	<tr>
		<td>groupby</td>
		<td>string</td>
		<td><p>A statement that applies data aggregation only to the specified fields. You can specify the following fields:</p>
		<ul>
		    <li>partnerTenantId</li>
		    <li>id</li>
		    <li>Name</li>
		    <li>market</li>
		    <li>firstSubscriptionCreationDate</li>
		    <li>latestSubscriptionCreationDate</li>
		    <li>firstSubscriptionEndDate</li>
		    <li>latestSubscriptionEndDate</li>
		    <li>firstSubscriptionSuspendedDate</li>
		    <li>latestSubscriptionSuspendedDate</li>
		    <li>firstSubscriptionDeprovisionedDate</li>
		    <li>latestSubscriptionDeprovisionedDate</li>
		</ul>
		<p>The returned data rows will contain the fields specified in the <em>groupby</em> parameter as well as the following:</p>
		<ul>
		    <li>indirectResellerCount</li>
		    <li>licenseCount</li>
		    <li>subscriptionCount</li>
		</ul>
		<p>The <em>groupby</em> parameter can be used with the aggregationLevel parameter. For example: <em>&amp;groupby=ageGroup,market&amp;aggregationLevel=week</em></td>
	</tr>
</tbody>
</table>

 

**Request headers**

-   See [Headers](headers.md) for more information.

**Request body**

None.

**Request example**

```
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/indirectresellers
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <span id="Response"></span><span id="response"></span><span id="RESPONSE"></span>Response


If successful, the response body contains a collection of [indirect resellers](partner-center-analytics.md#indirect_resellers) resources.

**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Error Codes](error-codes.md).

**Response example**

```
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
