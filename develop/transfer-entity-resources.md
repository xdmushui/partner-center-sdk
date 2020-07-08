---
title: TransferEntity resources
description: A partner creates a transfer when a customer wants his subscription with the partner to be transferred to another partner.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice:  partnercenter-sdk
---

# TransferEntity resources

**Applies to:**

- Partner Center

A partner creates a transfer when a customer wants his subscription with the partner to be transferred to another partner.

## TransferEntity

Describes a transferEntity.

| Property              | Type             | Description                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| id                    | string           | A transferEntity identifier that is supplied upon successful creation of the transferEntity.                               |
| createdTime           | DateTime         | The date the transferEntity was created, in date-time format. Applied upon successful creation of the transferEntity.      |
| lastModifiedTime      | DateTime         | The date the transferEntity was last updated, in date-time format. Applied upon successful creation of the transferEntity. |
| lastModifiedUser      | string           | The user who last updated the transferEntity. Applied upon successful creation of transferEntity.                          |
| customerName          | string           | Optional. The name of the customer whose subscriptions are being transferred.                                              |
| customerTenantId      | string           | A GUID formatted customer-id that identifies the customer. Applied upon successful creation of the transferEntity.         |
| partnertenantid       | string           | A GUID formatted partner-id that identifies the partner.                                                                   |
| sourcePartnerName     | string           | Optional. The name of the partner's organization who is initiating the transfer.                                           |
| sourcePartnerTenantId | string           | A GUID formatted partner-id that identifies the partner initiating the transfer.                                           |
| targetPartnerName     | string           | Optional. The name of the partner's organization to whom the transfer is targeted.                                         |
| targetPartnerTenantId | string           | A GUID formatted partner-id that identifies the partner to whom the transfer is targeted.                                  |
| lineItems             | Array of objects | An Array of [TransferLineItem](#transferlineitem) resources.                                                   |
| status                | string           | The status of the transferEntity. Possible values are "Active" (can be deleted/submitted) and "Completed" (has already been completed). Applied upon successful creation of the transferEntity.|

## TransferLineItem

Represents one item contained in a transferEntity.

| Property             | Type                             | Description                                                                                             |
|----------------------|----------------------------------|---------------------------------------------------------------------------------------------------------|
| id                   | string                           | A unique identifier for a transfer line item. Applied upon successful creation of the transferEntity.   |
| subscriptionId       | string                           | The subscription identifier.                                                                            |
| quantity             | int                              | The number of licenses or instances.                                                                    |
| billingCycle         | Object                           | The type of billing cycle set for the current period.                                                   |
| friendlyName         | string                           | Optional. The friendly name for the item defined by the partner to help disambiguate.                   |
| partnerIdOnRecord    | string                           | PartnerId on Record (MPNID) on the purchase that happens when the transfer is accepted.                 |
| offerId              | string                           | The offer identifier.    |
| addonItems           | List of **TransferLineItem** objects | A collection of transferEntity line items for addons that will be transferred along with the base subscription that is being transferred. Applied upon successful creation of the transferEntity.|
| transferError        | string                           | Applied after transferEntity is accepted in case of an error.                |
| status               | string           | The status of the lineitem in the transferEntity.|

## TransferSubmitResult

Represents the result of a transfer accept.

| Property          | Type                                                  | Description                        |
|-------------------|-------------------------------------------------------|------------------------------------|
| orders            | List of [Order](order-resources.md#order) objects.    | The collection of orders.          |
| transferErrors    | List of [TransferError](#transfererror) objects.      | The collection of transfer errors. |

## TransferError

Represents an error that occurs when a transfer is accepted.

| Property          | Type   | Description                                     |
|-------------------|--------|-------------------------------------------------|
| transferGroupId   | string | The order group ID of the order with the error. |
| code              | int    | The error code.                                 |
| description       | string | The description of the error.                   |
| lineItems         | List of **TransferLineItem** objects | A collection of transferEntity line items that are part of the transfer error.|

## TransferErrorCode

An [Enum](https://docs.microsoft.com/dotnet/api/system.enum) with values that indicate a type of order error.

| Value | Position | Description |
| --- | --- | --- |
| PartnerTokenMissing | 800001 | Partner Token missing in request context. |
| InvalidInput | 800002 | Invalid request input. |
| ServiceException | 800003 | Unexpected service error. |
| InvalidOfferId | 800004 | Invalid offer ID. |
| CreateOrderError | 800005 | Create order is not successful. |
| MpnIdNotFound | 800015 | MPN Id is not found. |
| NotValidIndirectResellerMpnId | 800016 | MPN Id is not a valid Indirect Reseller. |
| TransferIdNotFound | 900100   | Transfer request not found.   |
| TransferNotAllowedIfStatusIsInProgress | 900101 | The transfer request is already in progress.|
| TransferNotAllowedIfStatusIsCompleted | 900102 | The transfer request is already complete.|
| TransferCreateOrderError | 900103 | The transfer order is not successful.|
| TransferProcessedByAnotherRequest | 900104 | The transfer is being processed by another request.|