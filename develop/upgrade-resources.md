---
title: Upgrade resources
description: Describes the resources used to upgrade a user from a source subscription to a target subscription.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice:  partnercenter-sdk
---

# Upgrade resources

**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

Describes the resources used to upgrade a user from a source
subscription to a target subscription.

## Upgrade

Describes the behavior of an individual upgrade resource.

| Property      | Type                   | Description                                                                                  |
|---------------|------------------------|----------------------------------------------------------------------------------------------|
| TargetOffer   | Offer                  | The offer of the target subscription.                                                        |
| UpgradeType   | string                 | The type of upgrade: "none", "upgrade\_only", or "upgrade\_with\_license\_transfer".         |
| IsEligible    | boolean                | Identifies if the upgrade can be performed.                                                  |
| Quantity      | integer                | The quantity of the new offer to be purchased. Defaults to the source subscription quantity. |
| UpgradeErrors | array of UpgradeErrors | Reasons the upgrade cannot be performed, if applicable.                                      |
| Attributes    | ResourceAttributes     | The metadata attributes corresponding to the upgrade.                                        |

## UpgradeError

Describes a reason why an upgrade cannot be performed.

| Property          | Type               | Description                                                                                                                                                                                                                                                                                                                                                                                     |
|-------------------|--------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Code              | string             | The error code associated with the issue: "other", "delegated\_admin\_permissions\_disabled", "subscription\_status\_not\_active", "conflicting\_service\_types", "concurrency\_conflicts", "user\_context\_required", "subscription\_add\_ons\_present", "subscription\_does\_not\_have\_any\_upgrade\_paths", "subscription\_target\_offer\_not\_found", or "subscription\_not\_provisioned". |
| Description       | string             | Friendly text describing the error.                                                                                                                                                                                                                                                                                                                                                             |
| AdditionalDetails | string             | Additional details regarding the error.                                                                                                                                                                                                                                                                                                                                                         |
| Attributes        | ResourceAttributes | The metadata attributes corresponding to the error.                                                                                                                                                                                                                                                                                                                                             |

## UpgradeResult

Describes the result of the subscription upgrade process.

| Property             | Type                        | Description                                                                          |
|----------------------|-----------------------------|--------------------------------------------------------------------------------------|
| SourceSubscriptionId | string                      | The identifier of the source subscription.                                           |
| TargetSubscriptionID | string                      | The identifier of the target subscription.                                           |
| UpgradeType          | string                      | The type of upgrade: "none", "upgrade\_only", or "upgrade\_with\_license\_transfer". |
| UpgradeErrors        | array of UpgradeErrors      | Errors encountered while attempting to perform the upgrade, if applicable.           |
| LicenseErrors        | array of UserLicenseErrrors | Errors encountered while attempted to migrate user licenses, if applicable.          |
| Attributes           | ResourceAttributes          | The metadata attributes corresponding to the license.                                |

## UserLicenseError

Describes errors arising from failed user license transfer.

| Property     | Type                   | Description                                                               |
|--------------|------------------------|---------------------------------------------------------------------------|
| UserObjectId | string                 | The unique identified of the user object.                                 |
| Name         | string                 | The name of the user.                                                     |
| Email        | string                 | The email of the user.                                                    |
| Errors       | array of ServiceFaults | A list of exceptions thrown when trying to perform user license transfer. |
| Attributes   | ResourceAttributes     | The metadata attributes corresponding to the license.                     |

