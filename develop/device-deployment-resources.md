---
title: Device deployment resources
description: Describes resources related to device deployment.
ms.assetid: DF237297-7956-42EE-8F09-4304F6EFBF26
ms.date: 12/15/2017
ms.localizationpriority: medium
---

# Device deployment resources


**Applies To**

- Partner Center
- Partner Center for Microsoft Cloud Germany

Describes resources related to device deployment.

## <span id="ConfigurationPolicy"/><span id="configurationpolicy"/><span id="CONFIGURATIONPOLICY"/>ConfigurationPolicy


Provides information about a configuration policy.

| Property             | Type                                                           | Description                                                                                                                                               |
|----------------------|----------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|
| id                   | string                                                         | A GUID-formatted string that identifies the policy.                                                                                                       |
| name                 | string                                                         | The friendly name for the policy.                                                                                                                         |
| category             | string                                                         | The category.                                                                                                                                             |
| description          | string                                                         | The policy description.                                                                                                                                   |
| devicesAssignedCount | number                                                         | The number of devices assigned to this policy.                                                                                                            |
| policySettings       | array of strings                                               | The policy settings: "none","remove\_oem\_preinstalls","oobe\_user\_not\_local\_admin","skip\_express\_settings","skip\_oem\_registration", "skip\_eula". |
| createdDate          | string in UTC date-time format                                 | The date and time the policy was created.                                                                                                                 |
| lastModifiedDate     | string in UTC date-time format                                 | The date and time the policy was last modified.                                                                                                           |
| attributes           | [ResourceAttributes](utilityauditing-resources.md.md#resourceattributes) | The metadata attributes.                                                                                                                                  |

 

## <span id="Device"/><span id="device"/><span id="DEVICE"/>Device


Provides information about a device.

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
| attributes          | [ResourceAttributes](utilityauditing-resources.md.md#resourceattributes) | The metadata attributes.                                                 |

 

## <span id="BatchUploadDetails"/><span id="batchuploaddetails"/><span id="BATCHUPLOADDETAILS"/>BatchUploadDetails


Describes the status of a device batch upload of information about each
device in a list of devices.

| Property        | Type                                                           | Description                                                                                          |
|-----------------|----------------------------------------------------------------|------------------------------------------------------------------------------------------------------|
| batchTrackingId | string                                                         | A GUID-formatted string that is associated with the batch of devices uploaded.                       |
| status          | string                                                         | The status of the batch upload: "unknown","queued","processing","finished","finished\_with\_errors". |
| startedTime     | string in UTC date-time format                                 | The date and time that the batch upload process started.                                             |
| completedTime   | string in UTC date-time format                                 | The date and time that the batch upload process completed.                                           |
| devicesStatus   | array of [DeviceUploadDetails](#deviceuploaddetails) resources | An array of objects that specify the status of each device information upload.                       |
| attributes      | [ResourceAttributes](utilityauditing-resources.md.md#resourceattributes) | The metadata attributes.                                                                             |

 

## <span id="DeviceUploadDetails"/><span id="deviceuploaddetails"/><span id="DEVICEUPLOADDETAILS"/>DeviceUploadDetails


Describes the status of an upload of information about a device.

| Property         | Type                                                           | Description                                                                                       |
|------------------|----------------------------------------------------------------|---------------------------------------------------------------------------------------------------|
| deviceId         | string                                                         | A GUID-formatted string that is associated with the device.                                       |
| serialNumber     | string                                                         | The serial number uniquely associated with the device.                                            |
| productKey       | string                                                         | The product key uniquely associated with the device.                                              |
| status           | string                                                         | The status of the device information upload: "in-progress", "finished", "finished\_with\_errors". |
| errorCode        | string                                                         | If the device upload fails, the HTTP status error code returned.                                  |
| errorDescription | string                                                         | If the device upload fails, the HTTP error description.                                           |
| attributes       | [ResourceAttributes](utilityauditing-resources.md.md#resourceattributes) | The metadata attributes.                                                                          |

 

## <span id="DeviceBatch"/><span id="devicebatch"/><span id="DEVICEBATCH"/>DeviceBatch


Represents a collection of devices.

| Property     | Type                                                           | Description                                                           |
|--------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| id           | string                                                         | A GUID-formatted string that is associated with the batch of devices. |
| createdBy    | string                                                         | The name of the tenant that created the collection.                   |
| creationDate | string in UTC date-time format                                 | The data and time that the collection was created.                    |
| deviceCount  | number                                                         | The number of devices in the collection.                              |
| devicesLink  | [Link](utilityauditing-resources.md.md#link)                             | A link to the devices contained in this batch.                        |
| attributes   | [ResourceAttributes](utilityauditing-resources.md.md#resourceattributes) | The metadata attributes.                                              |

 

## <span id="DeviceBatchCreationRequest"/><span id="devicebatchcreationrequest"/><span id="DEVICEBATCHCREATIONREQUEST"/>DeviceBatchCreationRequest


Provides the information required to create a device batch and populate
it with devices.

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Property</th>
<th>Type</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>batchId</td>
<td>string</td>
<td>A GUID-formatted string that is associated with the batch of devices.</td>
</tr>
<tr class="even">
<td>devices</td>
<td>array of <a href="#device">Device</a> objects</td>
<td>Each object specifies a device.
<p>The following combinations of fields for identifying a device are accepted:</p>
<ul>
<li>hardwareHash + productKey.</li>
<li>hardwareHash + serialNumber.</li>
<li>hardwareHash + productKey + serialNumber.</li>
<li>hardwareHash only.</li>
<li>productKey only.</li>
<li>serialNumber + oemManufacturerName + modelName.</li>
</ul></td>
</tr>
<tr class="odd">
<td>attributes</td>
<td><a href="utilityauditing-resources.md.md#resourceattributes">ResourceAttributes</a></td>
<td>The metadata attributes.</td>
</tr>
</tbody>
</table>

 

## <span id="DevicePolicyUpdateRequest"/><span id="devicepolicyupdaterequest"/><span id="DEVICEPOLICYUPDATEREQUEST"/>DevicePolicyUpdateRequest


Provides the information required to update a list of devices with a
policy.

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Property</th>
<th>Type</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>devices</td>
<td>array of <a href="#device">Device</a> objects</td>
<td>Each object specifies a device. The following properties are required:
<ul>
<li>Id.</li>
<li>Policies.</li>
</ul></td>
</tr>
<tr class="even">
<td>attributes</td>
<td><a href="utilityauditing-resources.md.md#resourceattributes">ResourceAttributes</a></td>
<td>The metadata attributes.</td>
</tr>
</tbody>
</table>

 

 

 




