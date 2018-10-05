---
title: Get a customer's utilization records for Azure
description: Gets the utilization records of a customer's Azure subscription for a specified time period.
ms.assetid: 0270DBEA-AAA3-46FB-B5F0-D72B9BAC3112
ms.date: 9/28/2018
ms.localizationpriority: medium
---

# Get a customer's utilization records for Azure

**Applies To**

-   Partner Center
-   Partner Center for Microsoft Cloud Germany
-   Partner Center for Microsoft Cloud for US Government

Gets the utilization records of a customer's Azure subscription for a specified time period.

This Azure utilization API provides access to utilization records for a time period that represents when the utilization was reported in the billing system. It provides access to the same utilization data that is used to create and calculate the reconciliation file, but it does not have knowledge of billing system reconciliation file logic. Consequently, you should not expect reconciliation file summary results to exactly match the result retrieved from this API for the same time period.

For example, the billing system takes the same utilization data and then applies lateness rules to determine what is accounted for in a reconciliation file. When a billing period closes all usage until the end of the day that the billing period ends is included in the reconciliation file. Any late usage within the billing period that is reported within 24 hours after the billing period ends is accounted for, but in the next reconciliation file. The lateness rules of how the partner is billed are documented [here](https://msdn.microsoft.com/library/azure/mt219001).

This REST API is paged. If the response payload is larger than a single page, you must follow the next link to get the next page of utilization records.

## <span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>Prerequisites

-   Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone app and App+User credentials.
-   A customer identifier.
-   A subscription identifier.

## <span id="Examples"></span><span id="examples"><span id="EXAMPLES"></span>Examples

### C#

To obtain the Azure Utilization Records, you first need a customer ID and a subscription ID. You then call the [**IAzureUtilizationCollection.Query**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.utilization.iazureutilizationcollection.query) method to return a [**ResourceCollection**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.resourcecollection-1) that contains the utilization records. Because the resource collection is paged, you must then obtain an Azure utilization record enumerator to traverse the utilization pages.

```csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string subscriptionId;

IPartner partner = PartnerService.Instance.CreatePartnerOperations(credentials);

// Retrieve the utilization records for the last year in pages of 100 records.
var utilizationRecords = partner.Customers[customerId].Subscriptions[subscriptionId].Utilization.Azure.Query(
    DateTimeOffset.Now.AddYears(-1),
    DateTimeOffset.Now,
    size: 100);

// Create an Azure utilization enumerator which will aid us in traversing the utilization pages.
var utilizationRecordEnumerator = partner.Enumerators.Utilization.Azure.Create(utilizationRecords);

while (utilizationRecordEnumerator.HasValue)
{
    // 
    // Insert code here to work with this page.
    //

    // Get the next page.
    utilizationRecordEnumerator.Next();
}
```

**Sample**: [Console test app](console-test-app.md). **Project**: Partner Center SDK Samples **Class**: GetAzureSubscriptionUtilization.cs

### Java

To obtain the Azure Utilization Records, you first need a customer identifier and a subscription identifier. You then call the **IAzureUtilizationCollection.query** function to return a **ResourceCollection** that contains the utilization records. Because the resource collection is paged, you must then obtain an Azure utilization record enumerator to traverse the utilization pages.

```java
// IAggregatePartner partnerOperations;
// String customerId;
// String subscriptionId;

ResourceCollection<AzureUtilizationRecord> utilizationRecords = partnerOperations.getCustomers()
  .byId(customerId).getSubscriptions().byId(subscriptionId)
  .getUtilization().getAzure().query(
      new DateTime().minusYears(1), 
      new DateTime(), 
      AzureUtilizationGranularity.Daily, 
      true, 
      100);

// Create an Azure utilization enumerator which will aid us in traversing the utilization pages
IResourceCollectionEnumerator<ResourceCollection<AzureUtilizationRecord>> utilizationRecordEnumerator = 
    partnerOperations.getEnumerators().getUtilization().getAzure().create(utilizationRecords);

while (utilizationRecordEnumerator.hasValue())
{
    // 
    // Insert code here to work with this page.
    //

    // get the next page
    utilizationRecordEnumerator.next();
}
```

### PowerShell

To obtain the Azure Utilization Records, you first need a customer identifier and a subscription identifier. You then call the [**Get-PartnerCustomerSubscriptionUtilization**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerSubscriptionUtilization.md). This command will return all records available for the specified period of time.

```powershell
# $customerId
# $subscriptionId

Get-PartnerCustomerSubscriptionUtilization -CustomerId $customerId -SubscriptionId $subscriptionId -StartDate (Get-Date).AddDays(-2).ToUniversalTime() -Granularity Hourly -ShowDetails
```

## <span id="Request"></span><span id="request"></span><span id="REQUEST"></span>Request

**Request syntax**

| Method  | Request URI                                                                                                                                                                                                          |
|---------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **GET** | *{baseURL}*/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/utilizations/azure?start\_time={start-time}&end\_time={end-time}&granularity={granularity}&show\_details={True|False}&size={page-size} |

**URI parameters**

Use the following path and query parameters to get the utilization records.

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>Name</th>
<th>Type</th>
<th>Required</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>customer-tenant-id</td>
<td>string</td>
<td>Yes</td>
<td>A GUID-formatted string that identifies the customer.</td>
</tr>
<tr class="even">
<td>subscription-id</td>
<td>string</td>
<td>Yes</td>
<td>A GUID-formatted string that identifies the subscription.</td>
</tr>
<tr class="odd">
<td>start_time</td>
<td>string in UTC date-time offset format</td>
<td>Yes</td>
<td>The start of the time range that represents when the utilization was reported in the billing system.</td>
</tr>
<tr class="even">
<td>end_time</td>
<td>string in UTC date-time offset format</td>
<td>Yes</td>
<td>The end of the time range that represents when the utilization was reported in the billing system.</td>
</tr>
<tr class="odd">
<td>granularity</td>
<td>string</td>
<td>No</td>
<td>Defines the granularity of usage aggregations. Available options are:
<ul>
<li>daily (default)</li>
<li>hourly</li>
</ul></td>
</tr>
<tr class="even">
<td>show_details</td>
<td>boolean</td>
<td>No</td>
<td>Specifies whether to get the instance-level usage details. The default is true.</td>
</tr>
<tr class="odd">
<td>size</td>
<td>number</td>
<td>No</td>
<td>Specifies the number of aggregations returned by a single API call. The default is 1000. The max is 1000.</td>
</tr>
</tbody>
</table>

**Request headers**

-   See [Partner Center REST headers](headers.md) for more information.

**Request body**

None

**Request example - Attempting to reproduce reconciliation file results**

The following example will produce results that are the closest to what the reconciliation file will show for the period 7/2 - 8/1. They may not match exactly for the reasons stated in the introduction to this topic. The request that follows returns utilization data reported in the billing system between 7/2 at 12 AM (UTC) and 8/2 at 12 AM (UTC).

```http
GET https://api.partnercenter.microsoft.com/v1/customers/E499C962-9218-4DBA-8B83-8ADC94F47B9F/subscriptions/FC8F8908-F918-4406-AF13-D5BC0FE41865/utilizations/azure?start_time=2017-07-02T00:00:00-08:00&amp;end_time=2017-08-02T00:00:00-08:00 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e6a3b6b2-230a-4813-999d-57f883b60d38
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <span id="Response"></span><span id="response"></span><span id="RESPONSE"></span>Response


If successful, this method returns a collection of [Azure Utilization Record](azure-utilization-record.md) resources in the response body. In some cases, the Azure utilization data is not yet ready in a dependent system and this method will return an HTTP Status Code 204 with a Retry-After header. 

**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center REST error codes](error-codes.md).

**Response example**

```http
HTTP/1.1 200 OK
Content-Length: 2630
Content-Type: application/json; charset=utf-8
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
MS-RequestId: e6a3b6b2-230a-4813-999d-57f883b60d38
MS-CV: PjuGoYrw806o6A3Y.0
MS-ServerId: 030020525
Date: Fri, 04 Aug 2017 23:48:28 GMT

{
  "totalCount": 2,
  "items": [
    {
      "usageStartTime": "2017-06-07T17:00:00-07:00",
      "usageEndTime": "2017-06-08T17:00:00-07:00",
      "resource": {
        "id": "8767aeb3-6909-4db2-9927-3f51e9a9085e",
        "name": "Storage Admin",
        "category": "Storage",
        "subcategory": "Block Blob",
        "region": "Azure Stack"
      },
      "quantity": 0.217790327034891,
      "unit": "1 GB/Hr",
      "infoFields": {},
      "instanceData": {
        "resourceUri": "/subscriptions/ab7e2384-eeee-489a-a14f-1eb41ddd261d/resourcegroups/system.local/providers/Microsoft.Storage/storageaccounts/srphealthaccount",
        "location": "azurestack",
        "partNumber": "",
        "orderNumber": "",
        "additionalInfo": {
          "azureStack.MeterId": "09F8879E-87E9-4305-A572-4B7BE209F857",
          "azureStack.SubscriptionId": "dbd1aa30-e40d-4436-b465-3a8bc11df027",
          "azureStack.Location": "local",
          "azureStack.EventDateTime": "06/05/2017 06:00:00"
        }
      },
      "attributes": {
        "objectType": "AzureUtilizationRecord"
      }
    },
    {
      "usageStartTime": "2017-06-07T17:00:00-07:00",
      "usageEndTime": "2017-06-08T17:00:00-07:00",
      "resource": {
        "id": "8767aeb3-6909-4db2-9927-3f51e9a9085e",
        "name": "Storage Admin",
        "category": "Storage",
        "subcategory": "Block Blob",
        "region": "Azure Stack"
      },
      "quantity": 0.217790327034891,
      "unit": "1 GB/Hr",
      "infoFields": {},
      "instanceData": {
        "resourceUri": "/subscriptions/ab7e2384-eeee-489a-a14f-1eb41ddd261d/resourcegroups/system.local/providers/Microsoft.Storage/storageaccounts/srphealthaccount",
        "location": "azurestack",
        "partNumber": "",
        "orderNumber": "",
        "additionalInfo": {
          "azureStack.MeterId": "09F8879E-87E9-4305-A572-4B7BE209F857",
          "azureStack.SubscriptionId": "dbd1aa30-e40d-4436-b465-3a8bc11df027",
          "azureStack.Location": "local",
          "azureStack.EventDateTime": "06/05/2017 06:00:00"
        },
        "attributes": {
          "objectType": "AzureUtilizationRecord"
        }
      },

      "links": {
        "self": {
          "uri": "customers/E499C962-9218-4DBA-8B83-8ADC94F47B9F/subscriptions/FC8F8908-F918-4406-AF13-D5BC0FE41865/utilizations/azure?start_time=2017-06-10T00:00:00Z&amp;end_time=2017-07-09T00:00:00Z&amp;granularity=Daily&amp;show_details=True&amp;size=1000",
          "method": "GET",
          "headers": []
        }
      },
      "attributes": {
        "objectType": "Collection"
      }
    }
  ]
}
```