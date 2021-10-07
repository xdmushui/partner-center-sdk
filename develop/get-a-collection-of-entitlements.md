---
title: Get a collection of entitlements
description: How to get a collection of entitlements.
ms.date: 01/28/2019
ms.service: partner-dashboard
ms.subservice:  partnercenter-sdk
---

# Get a collection of entitlements

How to get a collection of entitlements.

## Prerequisites

- Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with App+User credentials.

- A customer ID (`customer-tenant-id`). If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard). Select **CSP** from the Partner Center menu, followed by **Customers**. Select the customer from the customer list, then select **Account**. On the customer's Account page, look for the **Microsoft ID** in the **Customer Account Info** section. The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).

## C\#

To get an entitlements collection for a customer, obtain an interface to [**Entitlement**](entitlement-resources.md#entitlement) operations by calling the  [**IAggregatePartner.Customers.ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer. Then, retrieve the interface from the **Entitlements** property and call the **Get()** or **GetAsync()** method to retrieve the collection of entitlements.

``` csharp
IAggregatePartner partnerOperations;
string customerId;

// Get the collection of entitlements.
var entitlements = partnerOperations.Customers.ById(customerId).Entitlements.Get();
```

To populate expiry dates for the entitlements to be retrieved, call the same methods above and set the optional boolean parameter **showExpiry** to true **Get(true)** or **GetAsync(true)**. This indicates that entitlement expiry dates are required (when applicable).

> [!IMPORTANT]
> On-premises entitlement types do not have expiry dates.

## REST request

### Request syntax

| Method | Request URI |
|--------|-------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customerId}/entitlements HTTP/1.1                            |

### URI parameters

Use the following path and query parameters when creating the request.

| Name | Type | Required | Description |
|------|------|----------|-------------|
| customerId | string | Yes | A GUID formatted customerId that identifies the customer. |
| entitlementType | string | No | Can be used to specify the type of entitlements to be retrieved (**software** or **reservedInstance** ). If not set, all types will be retrieved |
| showExpiry | boolean | No | Optional flag that indicates if entitlements expiry dates are required. |

### Request headers

For more information, see [Partner Center REST headers](headers.md).

### Request body

None.

### Request example

```http
GET https://api.partnercenter.microsoft.com/v1/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/entitlements HTTP/1.1
Authorization: Bearer <Token>
Accept: application/json
MS-RequestId: cdc428d2-035b-41c4-9a32-e643c4471cbd
MS-CorrelationId: 799eee8d-07d1-452a-a035-388259df137c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## REST response

If successful, the response body contains a collection of [Entitlement](entitlement-resources.md#entitlement) resources.

### Response success and error codes

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Error Codes](error-codes.md).

### Response example

```http
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
            "uri": "/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/artifacts/reservedinstance/groups/2caf524395724e638ef64e109f1f79ca/lineitems/03500b1b-f2d6-4e23-ab4b-9fd67b917012/resource/ebf2e74b-630e-4a09-857d-a1f6c6351336",
            "method": "GET",
            "headers": []
          },
          "resourceId": "ebf2e74b-630e-4a09-857d-a1f6c6351336",
          "artifactType": "reservedinstance"
        }
      ],
      "skuId": "007J",
      "entitlementType": "reservedinstance"
      "dynamicAttributes": {
               "reservationType": "virtualmachines"
        }
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
          "entitledArtifacts": [],
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
            "entitledArtifacts": [],
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
        "entitledArtifacts": [],
        "skuId": "0002",
        "entitlementType": "software"
    }
  ],
  "attributes": {
    "objectType": "Collection"
  }
}
```

## Additional Examples

The following example shows you how to retrieve a specific type of entitlements along with expiry dates (when applicable)

### C\# example

To retrieve a specific type of entitlements, obtain the **ByEntitlementType** interface from the **Entitlements** interface and use the **Get()** or **GetAsync()** methods.

``` csharp
ResourceCollection<Entitlement> entitlements = partnerOperations.Customers.ById(selectedCustomerId).Entitlements.ByEntitlementType("software").Get(true);
```

### Request example

```http
GET https://api.partnercenter.microsoft.com/v1/customers/de3dcef9-9991-459c-ac71-2903d1127414/entitlements?entitlementtype=software&showExpiry=true
Authorization: Bearer <Token>
Accept: application/json
MS-RequestId: 6517a410-67ce-4995-9bb7-116a52179f92
MS-CorrelationId: d9eb8194-9b99-4057-a2fe-98bdf05f013c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

### Response example

```http
HTTP/1.1 200 OK
Content-Length: 1791
Content-Type: application/json; charset=utf-8
MS-CorrelationId: d9eb8194-9b99-4057-a2fe-98bdf05f013c
MS-RequestId: 6517a410-67ce-4995-9bb7-116a52179f92
X-Locale: en-US
MS-CV: yD+4LBKePUSp/vqJ.0
MS-ServerId: 000002
Date: Mon, 28 Jan 2019 18:31:43 GMT

{
    "totalCount": 2,
    "items": [
        {
            "includedEntitlements": [
                {
                    "includedEntitlements": [],
                    "referenceOrder": {
                        "id": "4teYMtWYEeKM77JftGLIQYMOZPTwyOEV1",
                        "lineItemId": "0",
                        "alternateId": "8f3af3dea1ea"
                    },
                    "productId": "DG7GMGF0DWM2",
                    "quantity": 1,
                    "entitledArtifacts": [],
                    "skuId": "0001",
                    "entitlementType": "software"
                },
                {
                    "includedEntitlements": [],
                    "referenceOrder": {
                        "id": "4teYMtWYEeKM77JftGLIQYMOZPTwyOEV1",
                        "lineItemId": "0",
                        "alternateId": "8f3af3dea1ea"
                    },
                    "productId": "DG7GMGF0DWMK",
                    "quantity": 1,
                    "entitledArtifacts": [],
                    "skuId": "0001",
                    "entitlementType": "software"
                }
            ],
            "referenceOrder": {
                "id": "4teYMtWYEeKM77JftGLIQYMOZPTwyOEV1",
                "lineItemId": "0",
                "alternateId": "8f3af3dea1ea"
            },
            "productId": "DG7GMGF0DWM3",
            "quantity": 1,
            "entitledArtifacts": [],
            "skuId": "0002",
            "entitlementType": "software"
        },
        {
            "includedEntitlements": [
                {
                    "includedEntitlements": [],
                    "referenceOrder": {
                        "id": "4teYMtWYEeKM77JftGLIQYMOZPTwyOEV1",
                        "lineItemId": "1",
                        "alternateId": "8f3af3dea1ea"
                    },
                    "productId": "DG7GMGF0DWV1",
                    "quantity": 1,
                    "entitledArtifacts": [],
                    "skuId": "0002",
                    "entitlementType": "software"
                },
                {
                    "includedEntitlements": [],
                    "referenceOrder": {
                        "id": "4teYMtWYEeKM77JftGLIQYMOZPTwyOEV1",
                        "lineItemId": "1",
                        "alternateId": "8f3af3dea1ea"
                    },
                    "productId": "DG7GMGF0DWV2",
                    "quantity": 1,
                    "entitledArtifacts": [],
                    "skuId": "0002",
                    "entitlementType": "software"
                }
            ],
            "referenceOrder": {
                "id": "4teYMtWYEeKM77JftGLIQYMOZPTwyOEV1",
                "lineItemId": "1",
                "alternateId": "8f3af3dea1ea"
            },
            "productId": "DG7GMGF0DWBQ",
            "quantity": 1,
            "entitledArtifacts": [],
            "skuId": "0003",
            "entitlementType": "software",
            "expiryDate": "2022-01-28T00:00:00Z"
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```

The following examples show you how to retrieve information about products and reservations from an entitlement.

### Retrieve virtual machine reservation details from an entitlement by using SDK V1.8

### C\# example

To retrieve more details related to the virtual machine reservations from an entitlement, invoke the URI exposed under entitledArtifacts.link with artifactType = virtual_machine_reserved_instance.

``` csharp
ResourceCollection<Entitlement> entitlements = partnerOperations.Customers.ById(selectedCustomerId).Entitlements.ByEntitlementType("VirtualMachineReservedInstance").Get();

((VirtualMachineReservedInstanceArtifact)entitlements.First().EntitledArtifacts.First(x => x.Type == ArtifactType.VirtualMachineReservedInstance)).Link.InvokeAsync<VirtualMachineReservedInstanceArtifactDetails>(partnerOperations)
```

### Request example

```http
GET https://api.partnercenter.microsoft.com/v1/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/artifacts/virtualmachinereservedinstance/groups/2caf524395724e638ef64e109f1f79ca/lineitems/03500b1b-f2d6-4e23-ab4b-9fd67b917012/resource/ebf2e74b-630e-4a09-857d-a1f6c6351336 HTTP/1.1
Authorization: Bearer <Token>
Accept: application/json
MS-RequestId: cdc428d2-035b-41c4-9a32-e643c4471cbd
MS-CorrelationId: 799eee8d-07d1-452a-a035-388259df137c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

### Response example

```http
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

### Retrieve reservation details from an entitlement by using SDK V1.9

### C\# example

To retrieve more details related to the reservations from a reserved instance entitlement, invoke the URI exposed under ```entitledArtifacts.link``` with ```artifactType = reservedinstance```.

``` csharp
ResourceCollection<Entitlement> entitlements = partnerOperations.Customers.ById(selectedCustomerId).Entitlements.ByEntitlementType("ReservedInstance").Get();

((ReservedInstanceArtifact)entitlements.First().EntitledArtifacts.First(x => x.Type == ArtifactType.ReservedInstance)).Link.InvokeAsync<ReservedInstanceArtifactDetails>(partnerOperations);
```

### Request example

```http
GET https://api.partnercenter.microsoft.com/v1/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/artifacts/reservedinstance/groups/2caf524395724e638ef64e109f1f79ca/lineitems/03500b1b-f2d6-4e23-ab4b-9fd67b917012/resource/ebf2e74b-630e-4a09-857d-a1f6c6351336 HTTP/1.1
Authorization: Bearer <Token>
Accept: application/json
MS-RequestId: cdc428d2-035b-41c4-9a32-e643c4471cbd
MS-CorrelationId: 799eee8d-07d1-452a-a035-388259df137c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

### Response example

```http
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
  "type": "reservedinstance",
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

### API Consumers

Partners who are using the API to query virtual machine reserved instance entitlements - Update the request URI from **/customers/{customerId}/entitlements to /customers/{customerId}/entitlements?entitlementType=virtualmachinereservedinstance** to maintain backward compatibility. To consume virtual machine or Azure SQL with enhanced contract, update the request URI to **/customers/{customerId}/entitlements?entitlementType=reservedinstance**.
