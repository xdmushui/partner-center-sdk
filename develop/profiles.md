---
title: Profile
description: Describes the behavior of a Cloud Solution Provider's profiles.
ms.assetid: 42F2959B-D70D-41A7-9A50-E22A2356A339
ms.author: v-thpr
ms.date: 12/15/2017
ms.topic: article
ms.prod: partner-center
ms.technology: partner-center-sdk
---

# Profile


<span class="sidebar_heading" style="font-weight: bold;">Applies
To</span>

-   Partner Center
-   Partner Center operated by 21Vianet
-   Partner Center for Microsoft Cloud Germany
-   Partner Center for Microsoft Cloud for US Government

Describes the behavior of a Cloud Solution Provider's profiles.

## <span id="BillingProfile"></span><span id="billingprofile"></span><span id="BILLINGPROFILE"></span>BillingProfile


Describes a partner's billing profile.

| Property            | Type                                                           | Description                                                 |
|---------------------|----------------------------------------------------------------|-------------------------------------------------------------|
| companyName         | string                                                         | The billing company name.                                   |
| address             | [Address](utility-resources.md#address)                       | The billing address address of the company or organization. |
| primaryContact      | [Contact](utility-resources.md#contact)                       | The primary contact for the company or organization.        |
| purchaseOrderNumber | string                                                         | The company or organization's purchase order number.        |
| taxId               | string                                                         | The company or organization's tax Id.                       |
| billingCurrency     | string                                                         | The currency used by the company or organization.           |
| profileType         | string                                                         | The partner profile type.                                   |
| links               | [ResourceLinks](utility-resources.md#resourcelinks)           | The resource links corresponding to the profile.            |
| attributes          | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes corresponding to the profile.       |

 

## <span id="LegalBusinessProfile"></span><span id="legalbusinessprofile"></span><span id="LEGALBUSINESSPROFILE"></span>LegalBusinessProfile


Describes a partner's legal business profile.

| Property               | Type                                                           | Description                                                                                                                                                          |
|------------------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| companyName            | string                                                         | The legal company name.                                                                                                                                              |
| address                | [Address](utility-resources.md#address)                       | The address of the company or organization.                                                                                                                          |
| primaryContact         | [Contact](utility-resources.md#contact)                       | The primary contact for the company or organization.                                                                                                                 |
| companyApproverAddress | [Address](utility-resources.md#address)                       | The company approver address.                                                                                                                                        |
| companyApproverEmail   | string                                                         | The company approver email.                                                                                                                                          |
| vettingStatus          | string                                                         | The vetting status. This value is the string representation of the one of the member names found in [**VettingStatus**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.partners.vettingstatus).           |
| vettingSubStatus       | string                                                         | The vetting sub-status. This value is the string representation of the one of the member names found in [**VettingSubStatus**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.partners.vettingsubstatus). |
| profileType            | string                                                         | The partner profile type.                                                                                                                                            |
| links                  | [ResourceLinks](utility-resources.md#resourcelinks)           | The resource links corresponding to the profile.                                                                                                                     |
| attributes             | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes corresponding to the profile.                                                                                                                |

 

## <span id="MpnProfile"></span><span id="mpnprofile"></span><span id="MPNPROFILE"></span>MpnProfile


Describes a partner's Microsoft Partner Network profile.

| Property    | Type                                                           | Description                                           |
|-------------|----------------------------------------------------------------|-------------------------------------------------------|
| partnerName | string                                                         | The company or organization name.                     |
| mpnId       | string                                                         | The Microsoft Partner Network Id.                     |
| profileType | string                                                         | The partner profile type.                             |
| links       | [ResourceLinks](utility-resources.md#resourcelinks)           | The resource links corresponding to the profile.      |
| attributes  | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes corresponding to the profile. |

 

## <span id="OrganizationProfile"></span><span id="organizationprofile"></span><span id="ORGANIZATIONPROFILE"></span>OrganizationProfile


Describes a partner's organization profile.

| Property       | Type                                                           | Description                                                            |
|----------------|----------------------------------------------------------------|------------------------------------------------------------------------|
| id             | string                                                         | The organization's Id.                                                 |
| companyName    | string                                                         | The name of the company or organization.                               |
| defaultAddress | [Address](utility-resources.md#address)                       | The default address of the company or organization.                    |
| tenantId       | string                                                         | The tenant identifier.                                                 |
| domain         | string                                                         | The company or organization's domain.                                  |
| email          | string                                                         | Gets or sets the parent subscription.                                  |
| language       | string                                                         | The preferred language for communication.                              |
| culture        | string                                                         | The preferred culture for communication and currency, such as "en-us". |
| profileType    | string                                                         | The partner profile type.                                              |
| links          | [ResourceLinks](utility-resources.md#resourcelinks)           | The resource links corresponding to the profile.                       |
| attributes     | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes corresponding to the profile.                  |

 

## <span id="SupportProfile"></span><span id="supportprofile"></span><span id="SUPPORTPROFILE"></span>SupportProfile


Describes a partner's support profile.

| Property    | Type                                                           | Description                                           |
|-------------|----------------------------------------------------------------|-------------------------------------------------------|
| email       | string                                                         | The email address associated with the profile.        |
| telephone   | string                                                         | The phone number associated with the profile.         |
| website     | string                                                         | The support website.                                  |
| profileType | string                                                         | The partner profile type.                             |
| links       | [ResourceLinks](utility-resources.md#resourcelinks)           | The resource links corresponding to the profile.      |
| attributes  | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes corresponding to the profile. |

 

 

 




