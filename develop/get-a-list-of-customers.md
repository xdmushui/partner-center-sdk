---
title: Get a list of customers
description: Gets a collection of resources representing all the partner's customers.In the Partner Center dashboard, this operation can be performed by selecting either View Customers under Customer management on the main page, or selecting Customers in the sidebar.
ms.assetid: 6D636257-7C23-4DDF-9895-96F208B66232
ms.date: 9/21/2018
ms.localizationpriority: medium
---

# Get a list of customers


**Applies To**

- Partner Center
- Partner Center operated by 21Vianet
- Partner Center for Microsoft Cloud Germany
- Partner Center for Microsoft Cloud for US Government

Gets a collection of resources representing all the partner's customers.

In the Partner Center dashboard, this operation can be performed by selecting either **View Customers** under **Customer management** on the main page, or selecting **Customers** in the sidebar.

## <span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>Prerequisites

Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.

## <span id="Examples"/><span id="examples"><span id="EXAMPLES"/>Examples

### C#

To get a list of all customers, use your [**IAggregatePartner.Customers**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection to create a **IPartner** object. Then, retrieve the customer list using the [**Query()**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) or [**QueryAsync()**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync) methods. For instructions on creating a query, see the [**QueryFactory**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) class.

``` csharp
// IAggregatePartner partnerOperations;

// All the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

// read customers into chunks of 40s
var customersBatch = scopedPartnerOperations.Customers.Query(QueryFactory.Instance.BuildIndexedQuery(40));
var customersEnumerator = scopedPartnerOperations.Enumerators.Customers.Create(customersBatch);
```

**Sample**: [Console test app](console-test-app.md). **Project**: PartnerSDK.FeatureSamples **Class**: CustomerPaging.cs

### Java

To get a list of all customers, use your [**IAggregatePartner.getCustomers**] function to get a reference to the customer operations. Then, retrieve the customer list using the **query()** function. 

```java
// Query the customers, get the first page if a page size was set, otherwise get all customers
SeekBasedResourceCollection<Customer> customersPage = partnerOperations.getCustomers().query(QueryFactory.getInstance().buildIndexedQuery(40));

// Create a customer enumerator which will aid us in traversing the customer pages
IResourceCollectionEnumerator<SeekBasedResourceCollection<Customer>> customersEnumerator =
    partnerOperations.getEnumerators().getCustomers().create( customersPage );

int pageNumber = 1;

while (customersEnumerator.hasValue())
{
    /*
     * Use the customersEnumerator.getCurrent() function to
     * access the current page of customers.   
     */

    // Get the next page of customers
    customersEnumerator.next();
}
```

### PowerShell

Execute the [**Get-PartnerCustomer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomer.md) command with no parameters to get a complete list of customers.

```powershell
Get-PartnerCustomer
```

## <span id="REST_Request"/><span id="rest_request"/><span id="REST_REQUEST"/>REST Request

**Request syntax**

| Method  | Request URI                                                                   |
|---------|-------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers?size={size} HTTP/1.1 |

**URI parameter**

Use the following query parameter to get a list of customers.

| Name     | Type    | Required | Description                                        |
|----------|---------|----------|----------------------------------------------------|
| **size** | **int** | Y        | The number of results to be displayed at one time. |

**Request headers**

- See [Headers](headers.md) for more information.

**Request body**

None.

**Request example**

```http
GET https://api.partnercenter.microsoft.com/v1/customers?size=40 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 3705fc6d-4127-4a87-bdba-9658f73fe019
MS-CorrelationId: b12260fb-82de-4701-a25f-dcd367690645
```

## <span id="REST_Response"/><span id="rest_response"/><span id="REST_RESPONSE"/>REST Response


If successful, this method returns a collection of [Customers](customers.md) resources in the response body.

**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Error Codes](error-codes.md).

**Response example**

```http
HTTP/1.1 200 OK
Content-Length: 15650
Content-Type: application/json
MS-CorrelationId: b12260fb-82de-4701-a25f-dcd367690645
MS-RequestId: 3705fc6d-4127-4a87-bdba-9658f73fe019
Date: Fri, 20 Nov 2015 01:08:23 GMT

{
    "totalCount": 2,
    "items": [{
        "id": "b44bb1fb-c595-45b0-9e09-d657365580bf",
        "companyProfile": {
            "tenantId": "<guid>",
            "domain": "domain",
            "companyName": "companyName",
            "attributes": {
                "objectType": "CustomerCompanyProfile"
            }
        },
        "relationshipToPartner": "reseller",
        "attributes": {
            "objectType": "Customer"
        }
    },
    {
        "id": "45c44870-ef77-4fdd-b6fe-3dacb075cff2",
        "companyProfile": {
            "tenantId": "<guid>",
            "domain": "domain",
            "companyName": "companyName",
            "attributes": {
                "objectType": "CustomerCompanyProfile"
            }
        },
        "relationshipToPartner": "reseller",
        "attributes": {
            "objectType": "Customer"
        }
    }],
    "links": {
        "self": {
            "uri": "/v1/customers?size=40",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
