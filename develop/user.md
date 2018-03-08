---
title: User
description: 
    Describes an individual Partner Center user, their personal and account
    information, and the permissions they have within Partner Center.
ms.assetid: A2DEDDAB-C4DA-4ECA-931F-2054AB005973
ms.author: v-thpr
ms.date: 12/15/2017
ms.topic: article
ms.prod: partner-center
ms.technology: partner-center-sdk
---

# User


<span class="sidebar_heading" style="font-weight: bold;">Applies
To</span>

-   Partner Center
-   Partner Center operated by 21Vianet
-   Partner Center for Microsoft Cloud Germany
-   Partner Center for Microsoft Cloud for US Government

Describes an individual Partner Center user, their personal and account
information, and the permissions they have within Partner Center.

## <span id="User"></span><span id="user"></span><span id="USER"></span>User


Describes an individual user.

| Property              | Type                                                           | Description                                                                                                                                                                                                                |
|-----------------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id                    | string                                                         | The user identifier.                                                                                                                                                                                                       |
| userPrincipalName     | string                                                         | The user principal identifier.                                                                                                                                                                                             |
| firstName             | string                                                         | The first name of the user.                                                                                                                                                                                                |
| lastName              | string                                                         | The last name of the user.                                                                                                                                                                                                 |
| displayName           | string                                                         | The displayed name of the user.                                                                                                                                                                                            |
| passwordProfile       | [PasswordProfile](utility-resources.md#passwordprofile)       | The user's password profile.                                                                                                                                                                                               |
| phoneNumber           | string                                                         | The user's phone number.                                                                                                                                                                                                   |
| lastDirectorySyncTime | string in UTC date time format                                 | The last time that information for this user was synced between Azure Active Directory and on-premises Active Directory. A date time value only appears if Azure AD Connect sync is enabled. Otherwise, the value is null. |
| userDomainType        | string                                                         | The user domain type: "none", "managed," or "federated".                                                                                                                                                                   |
| state                 | string                                                         | The state of the user: "active", "inactive" (for a deleted user).                                                                                                                                                          |
| softDeletionTime      | string in UTC date time format                                 | Represents the start of the thirty day period after which data associated with a deleted user is permanently deleted and therefore unrecoverable.                                                                          |
| links                 | [ResourceLinks](utility-resources.md#resourcelinks)           | The resource links.                                                                                                                                                                                                        |
| attributes            | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes.                                                                                                                                                                                                   |

 

## <span id="CustomerUser"></span><span id="customeruser"></span><span id="CUSTOMERUSER"></span>CustomerUser


Describes a customer user.

| Property              | Type                                                           | Description                                                                                                                                                                                                                |
|-----------------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| usageLocation         | string                                                         | The location where the user intends to use the license.                                                                                                                                                                    |
| id                    | string                                                         | The user identifier.                                                                                                                                                                                                       |
| userPrincipalName     | string                                                         | The user principal identifier.                                                                                                                                                                                             |
| firstName             | string                                                         | The first name of the user.                                                                                                                                                                                                |
| lastName              | string                                                         | The last name of the user.                                                                                                                                                                                                 |
| displayName           | string                                                         | The displayed name of the user.                                                                                                                                                                                            |
| immutableId           | string                                                         | The immutable id of the user.                                                                                                                                                                                              |
| passwordProfile       | [PasswordProfile](utility-resources.md#passwordprofile)       | The user's password profile.                                                                                                                                                                                               |
| phoneNumber           | string                                                         | The user's phone number.                                                                                                                                                                                                   |
| lastDirectorySyncTime | string in UTC date time format                                 | The last time that information for this user was synced between Azure Active Directory and on-premises Active Directory. A date time value only appears if Azure AD Connect sync is enabled. Otherwise, the value is null. |
| userDomainType        | string                                                         | The user domain type: "none", "managed," or "federated".                                                                                                                                                                   |
| state                 | string                                                         | The state of the user: "active", "inactive" (for a deleted user).                                                                                                                                                          |
| softDeletionTime      | string in UTC date time format                                 | Represents the start of the thirty day period after which data associated with a deleted user is permanently deleted and therefore unrecoverable.                                                                          |
| links                 | [ResourceLinks](utility-resources.md#resourcelinks)           | The resource links.                                                                                                                                                                                                        |
| attributes            | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes.                                                                                                                                                                                                   |

 

## <span id="UserCredentials"></span><span id="usercredentials"></span><span id="USERCREDENTIALS"></span>UserCredentials


Describes a user's login credentials.

| Property | Type                                               | Description                          |
|----------|----------------------------------------------------|--------------------------------------|
| userName | string                                             | The name of the user.                |
| password | [SecureString](utility-resources.md#securestring) | The user's securely stored password. |

 

## <span id="UserMember"></span><span id="usermember"></span><span id="USERMEMBER"></span>UserMember


Describes a user's member information.

| Property          | Type                                                           | Description                        |
|-------------------|----------------------------------------------------------------|------------------------------------|
| displayName       | string                                                         | The displayed name for the user.   |
| userPrincipalName | string                                                         | The name of the user principal.    |
| roleId            | string                                                         | The identifier of the user's role. |
| id                | string                                                         | The identifier of the member.      |
| attributes        | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes.           |

 

 

 




