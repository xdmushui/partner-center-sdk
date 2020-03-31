---
title: Device deployment resources
description: Resources related to Partner Center device deployment.
ms.assetid: DF237297-7956-42EE-8F09-4304F6EFBF26
ms.date: 06/11/2019
ms.service: partner-dashboard
ms.subservice:  partnercenter-sdk
ms.localizationpriority: medium
---

# Device deployment resources

Applies to:

- Partner Center
- Partner Center for Microsoft Cloud Germany

The following resources are related to device deployment.

## ConfigurationPolicy

**ConfigurationPolicy** provides information about a configuration policy.

| Property             | Type                                                           | Description                                                        |
|----------------------|----------------------------------------------|--------------------------------------------------------------------------------------|
| id                   | string                                       | A GUID-formatted string that identifies the policy.                                  |
| name                 | string                                       | The friendly name for the policy.                                                    |
| category             | string                                       | The category.                                                                        |
| description          | string                                       | The policy description.                                                              |
| devicesAssignedCount | number                                       | The number of devices assigned to this policy.                                       |
| policySettings       | array of strings                             | The policy settings: "none","remove\_oem\_preinstalls","oobe\_user\_not\_local\_admin","skip\_express\_settings","skip\_oem\_registration", "skip\_eula".    |
| createdDate          | string in UTC date-time format               | The date and time the policy was created.                                            |
| lastModifiedDate     | string in UTC date-time format               | The date and time the policy was last modified.                                      |
| attributes           | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes.                                            |

## Device

**Device** provides information about a device.

| Property            | Type                                                           | Description                                                              |
|---------------------|----------------------------------------------------------------|--------------------------------------------------------------------------|
| id                  | string                                                         | A GUID-formatted string that identifies the device.                      |
| serialNumber        | string                                                         | The serial number uniquely associated with the device.                   |
| productKey          | string                                                         | The product key uniquely associated with the device.                     |
| hardwareHash        | string                                                         | The hardware hash uniquely associated with the device.                   |
| modelName           | string                                                         | The model name associated with the device.                               |
| oemManufacturerName | string                                                         | The name of the OEM manufacturer associated with the device.             |
| policies            | array of objects                                               | The list of policies assigned to the device.                             |
| uploadedDate        | string in UTC date-time format                                 | The date and time the device details were uploaded.                      |
| allowedOperations   | array of strings                                               | The list of HTTP methods allowed on a device sync as GET, PATCH, DELETE. |
| attributes          | [ResourceAttributes](utility-resources.md#resourceattributes)  | The metadata attributes.                                                 |

## BatchUploadDetails

**BatchUploadDetails** describes the status of a device batch upload of information about each device in a list of devices.

| Property        | Type     | Description                                                                  |
|-----------------|----------|------------------------------------------------------------------------------|
| batchTrackingId | string   | A GUID-formatted string that is associated with the batch of devices uploaded. |
| status          | string   | The status of the batch upload: "unknown","queued","processing","finished","finished\_with\_errors". |
| startedTime     | string in UTC date-time format | The date and time that the batch upload process started.   |
| completedTime   | string in UTC date-time format  | The date and time that the batch upload process completed.   |
| devicesStatus   | array of [DeviceUploadDetails](#deviceuploaddetails) resources | An array of objects that specify the status of each device information upload. |
| attributes      | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes.  |

## DeviceUploadDetails

**DeviceUploadDetails** describes the status of an upload of information about a device.

| Property         | Type                    | Description                                 |
|------------------|-------------------------|---------------------------------------------|
| deviceId         | string                  | A GUID-formatted string that is associated with the device. |
| serialNumber     | string                  | The serial number uniquely associated with the device. |
| productKey       | string                  | The product key uniquely associated with the device. |
| status           | string                  | The status of the device information upload: "in-progress", "finished", "finished\_with\_errors". |
| errorCode        | string                  | The HTTP status error code returned if the device upload fails. |
| errorDescription | string                  | The HTTP error description if the device upload fails. |
| attributes       | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes.   |

## DeviceBatch

**DeviceBatch** represents a collection of devices.

| Property     | Type                                                           | Description                                                           |
|--------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| id           | string                                                         | A GUID-formatted string that is associated with the batch of devices. |
| createdBy    | string                                                         | The name of the tenant that created the collection.                   |
| creationDate | string in UTC date-time format                                 | The data and time that the collection was created.                    |
| deviceCount  | number                                                         | The number of devices in the collection.                              |
| devicesLink  | [Link](utility-resources.md#link)                              | A link to the devices contained in this batch.                        |
| attributes   | [ResourceAttributes](utility-resources.md#resourceattributes)  | The metadata attributes.                                              |

## DeviceBatchCreationRequest

**DeviceBatchCreationRequest** provides the information required to create a device batch and populates it with devices.

| Property     | Type                                                           | Description                                                           |
|--------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| batchId      | string                                                         | A GUID-formatted string that is associated with the batch of devices. |
| devices      | array of [Device](#device) objects                             | Each object specifies a device. The following combinations of fields for identifying a device are accepted: hardwareHash + productKey, hardwareHash + serialNumber, hardwareHash + productKey + serialNumber, hardwareHash only, productKey only, serialNumber + oemManufacturerName + modelName. |
| attributes   | [ResourceAttributes](utility-resources.md#resourceattributes)  | The metadata attributes.                                              |

## DevicePolicyUpdateRequest

**DevicePolicyUpdateRequest** provides the information required to update a list of devices with a policy.

| Property     | Type                                                           | Description                                                           |
|--------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| devices      | array of [Device](#device) objects                             | Each object specifies a device. The following properties are required: Id, Policies. |
| attributes   | [ResourceAttributes](utility-resources.md#resourceattributes)  | The metadata attributes.                                              |
