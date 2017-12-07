---
title: Upload a list of devices to create a new batch for the specified customer
description: How to upload a list of information about devices to create a new batch for the specified customer. This creates a device batch for enrollment in zero-touch deployment, and associates the devices and the device batch with the specified customer.
ms.assetid: 94DB98F2-2188-46BB-97BA-100B8C94F120
ms.author: v-thpr
ms.date: 12/15/2017
ms.topic: article
ms.prod: partner-center
ms.technology: partner-center-sdk
---

# Upload a list of devices to create a new batch for the specified customer


**Applies To**

-   Partner Center
-   Partner Center for Microsoft Cloud Germany

How to upload a list of information about devices to create a new batch for the specified customer. This creates a device batch for enrollment in zero-touch deployment, and associates the devices and the device batch with the specified customer.

## <span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>Prerequisites


-   Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.
-   The customer identifier.
-   The list of device resources that provide the information about the individual devices.

## <span id="C_"></span><span id="c_"></span>C#


To upload a list of devices to create a new device batch, first, instantiate a new [List](https://msdn.microsoft.com/en-us/library/6sh2ey19.aspx) of type [**Device**](https://review.docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device) and populate the list with the devices. The following combinations of populated properties are required at a minimum for identifying each device:

-   [**HardwareHash**](https://review.docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device_hardwarehash) + [**ProductKey**](https://review.docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device_productkey).
-   [**HardwareHash**](https://review.docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device_hardwarehash) + [**SerialNumber**](https://review.docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device_serialnumber).
-   [**HardwareHash**](https://review.docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device_hardwarehash) + [**ProductKey**](https://review.docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device_productkey) + [**SerialNumber**](https://review.docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device_serialnumber).
-   [**HardwareHash**](https://review.docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device_hardwarehash) only.
-   [**ProductKey**](https://review.docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device_productkey) only.
-   [**SerialNumber**](https://review.docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device_serialnumber) + [**OemManufacturerName**](https://review.docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device_oemmanufacturername) + [**ModelName**](https://review.docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device_modelname).

Next, instantiate a [**DeviceBatchCreationRequest**](https://review.docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest) object and set the [**BatchId**](https://review.docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest_batchid) property to a unique name of your choosing, and the [**Devices**](https://review.docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest_devices) property to the list of devices to upload. Then, to process the device batch creation request, call the [**IAggregatePartner.Customers.ById**](https://review.docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier to retrieve an interface to operations on the specified customer. Finally, call the [**DeviceBatches.Create**](https://review.docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations.create) or [**CreateAsync**](https://review.docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations.createasync) method with the device batch creation request to create the batch.

```
IAggregatePartner partnerOperations;
string selectedCustomerId;       

List<Device> devicesToBeUploaded = new List<Device>
{
    new Device
    {
        HardwareHash = "DummyHash123",
        ProductKey = "00329-00000-0003-AA606",
        SerialNumber = "1R9-ZNP67"
    }
};

DeviceBatchCreationRequest 
    newDeviceBatch = new DeviceBatchCreationRequest
{
    BatchId = "SDKTestDeviceBatch",
    Devices = devicesToBeUploaded
};

var trackingLocation = 
    partnerOperations.Customers.ById(selectedCustomerId).DeviceBatches.Create(newDeviceBatch);
```

**Sample**: [Console test app](console-test-app.md). **Project**: Partner Center SDK Samples **Class**: CreateDeviceBatch.cs

## <span id="Request"></span><span id="request"></span><span id="REQUEST"></span>Request


**Request syntax**

| Method   | Request URI                                                                                   |
|----------|-----------------------------------------------------------------------------------------------|
| **POST** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/deviceBatches HTTP/1.1 |

 

**URI parameter**

Use the following path parameters when creating the request.

| Name        | Type   | Required | Description                                           |
|-------------|--------|----------|-------------------------------------------------------|
| customer-id | string | Yes      | A GUID-formatted string that identifies the customer. |

 

**Request headers**

-   See [Partner Center REST headers](headers.md) for more information.

**Request body**

The request body must contain a [DeviceBatchCreationRequest](devicedeployment.md#devicebatchcreationrequest) resource.

**Request example**

```
POST https://api.partnercenter.microsoft.com/v1/customers/c7f3c849-129f-4b85-a96d-4f8e88b315a3/deviceBatches HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: c245d5f2-1de3-4ae0-9e42-95e38e3cb8ff
MS-CorrelationId: e3f26e6a-044f-4371-ad52-0d91ce4200be
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 340
Expect: 100-continue
Connection: Keep-Alive
{
    "BatchId": "SDKTestDeviceBatch",
    "Devices": [{
            "Id": null,
            "SerialNumber": "1R9-ZNP67",
            "ProductKey": "00329-00000-0003-AA606",
            "HardwareHash": "DummyHash123",
            "Policies": null,
            "CreatedBy": null,
            "UploadedDate": "0001-01-01T00:00:00",
            "AllowedOperations": null,
            "Attributes": {
                "ObjectType": "Device"
            }
        }
    ],
    "Attributes": {
        "ObjectType": "DeviceBatchCreationRequest"
    }
}
```

## <span id="Response"></span><span id="response"></span><span id="RESPONSE"></span>Response


If successful, the response contains a **Location** header that has a URI that can be used to retrieve device upload status. Save this URI for use with other related REST APIs.

**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center REST error codes](error-codes.md).

**Response example**

```
HTTP/1.1 202 Accepted
Content-Length: 0
Location: /customers/c7f3c849-129f-4b85-a96d-4f8e88b315a3/batchJobStatus/beba2053-5401-46ff-9223-7e841ed78fbf
MS-CorrelationId: 772871a9-399b-4f3b-b8c7-38f550e4f22a
MS-RequestId: cb82f7d6-f0d9-44d4-82f9-f6eee6e68390
MS-CV: iqOqN0FnaE2y0HcD.0
MS-ServerId: 030020525
Date: Thu, 28 Sep 2017 20:35:35 GMT
```

 

 




