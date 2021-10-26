---
title: Transition resources
description: Describes the resources used to transition new commerce subscriptions.
ms.date: 02/23/2021
ms.service: partner-dashboard
ms.subservice:  partnercenter-sdk
author: BrentSerbus
ms.author: brserbus
---

# Transition resources

**Applies To**

- Partner Center

**Appropriate roles**

- Global admin
- Admin agent

> [!Note] 
> New Commerce changes are currently available only to partners who are part of the M365/D365 new commerce experience technical preview.

Describes the resources used to transition from one new commerce subscription to another.

## TransitionEligibility

Describes the behavior of an individual subscription transition resource.

| Property          | Type                    | Description                                                                                  |
|-------------------|-------------------------|----------------------------------------------------------------------------------------------|
| CatalogItemId | string                  | The catalog item id being checked for. |
| Title  | string                  | The SKU title. |
| Description | string                  | The SKU description. |
| Quantity | integer                 | The quantity of the new offer to be purchased. |
| Eligibilities | list of TransitionEligibilityDetail | A list of transition eligibility details. | 

## TransitionEligibilityDetail

Describes the behavior of an individual transition eligibility details resource.

| Property          | Type                    | Description                                                                                  |
|-------------------|-------------------------|----------------------------------------------------------------------------------------------|
| IsEligible | boolean | Returns the eligibility is valid or not. |
| TransitionType | TransitionType | The type of transition. Can be transition_with_license_transfer or transition_only. |
| Errors | List of TransitionErrors | The metadata attributes corresponding to the error. |

## Transition

Describes the behavior of an individual subscription transition resource.

| Property          | Type                    | Description                                                                                  |
|-------------------|-------------------------|----------------------------------------------------------------------------------------------|
| FromCatalogItemId | string                  | The From catalog item id. |
| FromSubscriptionId | string                 | The From subscription id. |
| ToCatalogItemId   | string                  | The To catalog item id. |
| ToSubscriptionId  | string                  | The To subscription id. This is only populated if the subscription changes. Currently only Legacy Upgrade needs this, but modern partial transition will also. |
| Quantity          | integer                 | The quantity being transitioned to the target catalog item. |
| TermDuration          | string                 | The term duration for the subscription. |
| BillingCycle          | string                 | The billing cycle for the subscription. |
| TransitionType    | string 		      | The transition type. Possible values - `transition_only`, `transition_with_license_transfer`.   |
| Events            | list of TransitionEvents | The events of the transition. |

## TransitionEvent

Describes a reason why an upgrade cannot be performed.

| Property          | Type               | Description                                                                                                                                                                                                                                                                                                                                                                                     |
|-------------------|--------------------|------------------------------------------------------------------------------|
| Name | string | The name of the transition event. Possible values Conversion or LicenseReassignment. |
| Status | string  | The status of transition event. Possible values InProgress, Completed or Failed.  |
| Timestamp | DateTime | The UTC timestamp of the event. |
| Errors | List of TransitionErrors | The metadata attributes corresponding to the error. |

## TransitionError

Represents an error for subscription transfer eligibility. Provides a reason why a transition cannot be performed.

| Property          | Type               | Description                                                                                                                                                                                                                                                                                                                                                                                     |
|-------------------|--------------------|--------------------------------------------------------------|
| Code | TransitionErrorCode | The error code associated with the issue. |
| Description | string  | Friendly text describing the error. |

