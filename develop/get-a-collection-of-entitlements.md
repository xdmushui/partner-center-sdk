---
title: Get a collection of entitlements
description: How to get a collection of entitlements.
ms.assetid: 3EE2F67D-8D99-4FAB-A2D6-D33BAD1F324F
ms.author: v-thpr
ms.date: 12/15/2017
ms.topic: article
ms.prod: partner-center
ms.technology: partner-center-sdk
---

# Get a collection of entitlements


**Applies To**

-   Partner Center

How to get a collection of entitlements.

## <span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>Prerequisites


-   Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with App+User credentials.
-   A customer identifier.

## <span id="C_"></span><span id="c_"></span>C#


To get an entitlements collection for a customer, obtain an interface to [**Entitlement**](entitlement.md#entitlement) operations by calling the  [**IAggregatePartner.Customers.ById()**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer. Then, retrieve the interface from the **Entitlements** property and call the **Get()** or **GetAsync()** method to retrieve the collection of entitlements.

```CSharp
IAggregatePartner partnerOperations;
string customerId;

// Get the collection of entitlements.
var entitlements = partnerOperations.Customers.ById(customerId).Entitlements.Get();
```

## <span id="Request"></span><span id="request"></span><span id="REQUEST"></span>REST Request


**Request syntax**

| Method  | Request URI                                                                                                           |
|---------|-----------------------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customerId}/entitlements HTTP/1.1                            |

 

**URI parameters**

Use the following path and query parameters when creating the request.

| Name                   | Type   | Required | Description                                                       |
|------------------------|--------|----------|-------------------------------------------------------------------|
| customerId             | string | Yes      | A GUID formatted customerId that identifies the customer.         |

 

**Request headers**

-   See [Partner Center REST headers](headers.md) for more information.

**Request body**

None.

**Request example**

```
GET https://api.partnercenter.microsoft.com/v1/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/entitlements HTTP/1.1
Authorization: Bearer <Token>
Accept: application/json
MS-RequestId: cdc428d2-035b-41c4-9a32-e643c4471cbd
MS-CorrelationId: 799eee8d-07d1-452a-a035-388259df137c
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Host: api.partnercenter.microsoft.com
```

## <span id="REST_Response"></span><span id="rest_response"></span><span id="REST_RESPONSE"></span>REST Response


If successful, the response body contains a collection of [Entitlement](entitlement.md#entitlement) resources.

**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Error Codes](error-codes.md).

**Response example**

```
HTTP/1.1 200 OK
Content-Length: 103778
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 799eee8d-07d1-452a-a035-388259df137c
MS-RequestId: cdc428d2-035b-41c4-9a32-e643c4471cbd
X-Locale: en-US
MS-CV: EjFdw8fCpkKyMyza.0
MS-ServerId: 000002
Date: Mon, 19 Mar 2018 07:42:51 GMT

{
  "totalCount": 2,
  "items": [
    {
      "includedEntitlements": [],
      "referenceOrder": {
        "id": "KaJ8XvkKc_GoNZOUyjVaRJalTBN5MWdV1",
        "lineItemId": "0"
      },
      "productId": "DZH318Z0BQ3W",
      "quantity": 1,
      "entitledArtifacts": [
        {
          "link": {
            "uri": "/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/artifacts/virtualmachinereservedinstance/groups/2caf524395724e638ef64e109f1f79ca/lineitems/03500b1b-f2d6-4e23-ab4b-9fd67b917012/resource/ebf2e74b-630e-4a09-857d-a1f6c6351336",
            "method": "GET",
            "headers": []
          },
          "resourceId": "ebf2e74b-630e-4a09-857d-a1f6c6351336",
          "artifactType": "virtual_machine_reserved_instance"
        }
      ],
      "skuId": "007J",
      "skuTitle": "Reserved VM Instance, Standard_F2, US East 2, 1 Year",
      "entitlementType": "virtual_machine_reserved_instance"
    },    
    {
      "includedEntitlements": [
        {
          "includedEntitlements": [],
          "referenceOrder": {
              "id": "NUXMSvmS20EQ4kFsZmzkSqb747fqKmNk1",
              "lineItemId": "0"
          },
          "productId": "DG7GMGF0DWTJ",
          "quantity": 1,
          "entitledArtifacts": [
            {
              "link": {
                "uri": "/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/artifacts/productkey/groups/2caf524395724e638ef64e109f1f79ca/lineitems/0095a02f-1b12-4bb3-a805-f2b71b055ea7/items/DG7GMGF0DWTJ:0001:0095a02f-1b12-4bb3-a805-f2b71b055ea7",
                "method": "GET",
                "headers": []
              },
              "reason": "",
              "state": "Active",
              "artifactType": "product_key"
            }
          ],
          "skuId": "0001",
          "entitlementType": "software"
        },
        {
          "includedEntitlements": [],
          "referenceOrder": {
            "id": "NUXMSvmS20EQ4kFsZmzkSqb747fqKmNk1",
            "lineItemId": "0"
          },
            "productId": "DG7GMGF0DWLG",
            "quantity": 1,
            "entitledArtifacts": [
              {
                "link": {
                  "uri": "/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/artifacts/productkey/groups/2caf524395724e638ef64e109f1f79ca/lineitems/0095a02f-1b12-4bb3-a805-f2b71b055ea7/items/DG7GMGF0DWLG:0002:0095a02f-1b12-4bb3-a805-f2b71b055ea7",
                  "method": "GET",
                  "headers": []
                },
                "reason": "",
                "state": "Active",
                "artifactType": "product_key"
              }
            ],
            "skuId": "0002",
            "entitlementType": "software"
          }
        ],
        "referenceOrder": {
          "id": "NUXMSvmS20EQ4kFsZmzkSqb747fqKmNk1",
          "lineItemId": "0"
        },
        "productId": "DG7GMGF0DWTK",
        "quantity": 1,
        "entitledArtifacts": [
          {
            "link": {
              "uri": "/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/artifacts/productkey/groups/2caf524395724e638ef64e109f1f79ca/lineitems/0095a02f-1b12-4bb3-a805-f2b71b055ea7/items/DG7GMGF0DWTK:0002:0095a02f-1b12-4bb3-a805-f2b71b055ea7",
              "method": "GET",
              "headers": []
            },
            "reason": "",
            "state": "Active",
            "artifactType": "product_key"
          }
        ],
        "skuId": "0002",
        "entitlementType": "software"
    }
  ],
  "attributes": {
    "objectType": "Collection"
  }
}
```

## <span id="AdditionalExamples"></span><span id="additionalexamples"></span>Additional Examples   


The following examples show you how to retrieve information about products and reservations from an entitlement.

### <span id="ProductKeyExample"></span><span id="productkeyexample"></span><span id="PRODUCTKEYEXAMPLE"></span>Retrieve software product key details from an entitlement. 

**C# example**

To retrieve more details related to the software product key from an entitlement, invoke the URI exposed under entitledArtifacts.link with artifactType = product_key.

```CSharp
ResourceCollection<Entitlement> entitlements = partnerOperations.Customers.ById(selectedCustomerId).Entitlements.Get();

((ProductKeyArtifact)entitlements.First().EntitledArtifacts.First(x => x.Type == ArtifactType.ProductKey)).Link.InvokeAsync<ProductKeyArtifactDetails>(partnerOperations)
```   

**Request example**

```
GET https://api.partnercenter.microsoft.com/v1/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/artifacts/productkey/groups/2caf524395724e638ef64e109f1f79ca/lineitems/0095a02f-1b12-4bb3-a805-f2b71b055ea7/items/DG7GMGF0DWTK:0002:0095a02f-1b12-4bb3-a805-f2b71b055ea7 HTTP/1.1
Authorization: Bearer <Token>
Accept: application/json
MS-RequestId: 43d5d020-5318-482a-912e-12dcaed50b40
MS-CorrelationId: 1820804f-56b8-47b0-93a0-1b162ac50409
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Host: api.partnercenter.microsoft.com 
```

**Response example**

```
HTTP/1.1 200 OK
Content-Length: 368
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 1820804f-56b8-47b0-93a0-1b162ac50409
MS-RequestId: 43d5d020-5318-482a-912e-12dcaed50b40
X-Locale: en-US
MS-CV: YNrxOt3wPEync2an.0
MS-ServerId: 000004
Date: Wed, 06 Jun 2018 22:53:18 GMT

{
    "type": "product_key",
    "productKey": "8F9FN-2JWYW-12345-67890-XWRTF"
}
```

### <span id="VirtualMachineReservationExample"></span><span id="virtualmachinereservationexample"></span><span id="VIRTUALMACHINERESERVATIONEXAMPLE"></span>Retrieve virtual machine reservation details from an entitlement. 

**C# example**   

To retrieve more details related to the virtual machine reservations from an entitlement, invoke the URI exposed under entitledArtifacts.link with artifactType = virtual_machine_reserved_instance.

```CSharp
ResourceCollection<Entitlement> entitlements = partnerOperations.Customers.ById(selectedCustomerId).Entitlements.Get();

((VirtualMachineReservedInstanceArtifact)entitlements.First().EntitledArtifacts.First(x => x.Type == ArtifactType.VirtualMachineReservedInstance)).Link.InvokeAsync<VirtualMachineReservedInstanceArtifactDetails>(partnerOperations)
```

**Request example**

```
GET https://api.partnercenter.microsoft.com/v1/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/artifacts/virtualmachinereservedinstance/groups/2caf524395724e638ef64e109f1f79ca/lineitems/03500b1b-f2d6-4e23-ab4b-9fd67b917012/resource/ebf2e74b-630e-4a09-857d-a1f6c6351336 HTTP/1.1
Authorization: Bearer <Token>
Accept: application/json
MS-RequestId: cdc428d2-035b-41c4-9a32-e643c4471cbd
MS-CorrelationId: 799eee8d-07d1-452a-a035-388259df137c
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Host: api.partnercenter.microsoft.com 
```

**Response example**

```
HTTP/1.1 200 OK
Content-Length: 368
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 799eee8d-07d1-452a-a035-388259df137c
MS-RequestId: cdc428d2-035b-41c4-9a32-e643c4471cbd
X-Locale: en-US
MS-CV: yrdTGsZ7IU2v9okv.0
MS-ServerId: 000002
Date: Mon, 19 Mar 2018 07:45:14 GMT

{
  "type": "virtual_machine_reserved_instance",
  "virtualMachineReservations": [
    {
      "reservationId": "99f320db-c029-4c1b-a157-dad76e4481b6",
      "scopeType": "Shared",
      "quantity": 1,
      "expiryDateTime": "2019-02-23T00:00:00",
      "effectiveDateTime": "2018-02-23T18:15:24.6724884Z",
      "provisioningState": "Created"
    }
  ]
}
```


