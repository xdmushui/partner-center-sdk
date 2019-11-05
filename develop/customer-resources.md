---
title: Customer resources
description: Customer resources that represent a customer or reseller.
ms.assetid: C7EC2657-62F2-43B3-B171-2F74498D45E0
ms.date: 05/29/2019
ms.service: partner-dashboard
ms.subservice: PartnerCenterCSP
ms.localizationpriority: medium
---

# Customer resources

Applies to:

- Partner Center
- Partner Center operated by 21Vianet
- Partner Center for Microsoft Cloud Germany
- Partner Center for Microsoft Cloud for US Government

## Customer

The **Customer** resource represents a customer or reseller. Most broadly, a customer resouce can be any person, employee, or organization that wishes to do business
with Microsoft and Microsoft's resellers. Customers also have a company profile and a billing profile.

>[!NOTE]
>The **Customer** resource has a rate limit of 500 requests per minute per tenant identifier.

| Property              | Type                                                             | Description                                                                                                                                  |
|-----------------------|------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
| id                    | string                                                           | The customer ID.                                                                                                                             |
| commerceId            | string                                                           | The commerce ID.                                                                                                                             |
| companyProfile        | [CustomerCompanyProfile](#customercompanyprofile)                | Additional information about the company or organization.                                                                                    |
| billingProfile        | [CustomerBillingProfile](#customerbillingprofile)                | Additional information used for billing.                                                                                                     |
| relationshipToPartner | string                                                           | Defines the licensing program that the partner uses for this customer: "none", "reseller", "advisor", "syndication" or "microsoft\_support". |
| allowDelegatedAccess  | boolean                                                          | Whether the partner has been granted delegated admin privileges by this customer.                                                            |
| userCredentials       | [UserCredentials](user-resources.md#usercredentials) | The user credentials.                                                                                                                        |
| customDomains         | array of strings                                                 | List of custom domains of a customer.                                                                                                        |
| associatedPartnerId   | string                                                           | The indirect reseller associated to this customer account. This value can be set only by indirect CSP partners.                              |
| links                 | [ResourceLinks](utility-resources.md#resourcelinks)             | The resource links contained within the profile.                                                                                             |
| attributes            | [ResourceAttributes](utility-resources.md#resourceattributes)   | The metadata attributes corresponding to the profile.                                                                                        |

## CustomerCompanyProfile

The **CustomerCompanyProfile** resource is additional information about the company or organization.

| Property    | Type                                                           | Description                                                                       |
|-------------|----------------------------------------------------------------|-----------------------------------------------------------------------------------|
| tenantId    | string                                                         | The customer's tenant identifier for Azure AD. This is also called a MicrosoftID. |
| domain      | string                                                         | The customer's name, such as contoso.onmicrosoft.com.                             |
| companyName | string                                                         | The name of the company or organization.                                          |
| links       | [ResourceLinks](utility-resources.md#resourcelinks)           | The resource links contained within the profile.                                  |
| attributes  | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes corresponding to the profile.                             |

## CustomerBillingProfile

The **CustomerBillingProfile** resource is additional information used for billing the customer.

| Property       | Type                                                           | Description                                                                                                                                            |
|----------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| id             | string                                                         | The profile identifier.                                                                                                                                |
| firstName      | string                                                         | The first name of the billing contact at the customer's company. This is the person that invoices and other billing communication will be directed to. |
| lastName       | string                                                         | The last name of the billing contact.                                                                                                                  |
| email          | string                                                         | The billing contact's email address                                                                                                                    |
| culture        | string                                                         | Their preferred culture for communication and currency, such as "en-us".                                                                               |
| language       | string                                                         | Their preferred language for communication.                                                                                                            |
| companyName    | string                                                         | The name of the company or organization.                                                                                                               |
| defaultAddress | [Address](utility-resources.md#address)                       | The address that bills are sent to, where the billing contact works.                                                                                   |
| links          | [ResourceLinks](utility-resources.md#resourcelinks)           | The resource links contained within the profile.                                                                                                       |
| attributes     | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes corresponding to the profile.                                                                                                  |

## CustomerRelationshipRequest

The **CustomerRelationshipRequest** resource contains the URL used by the customer to establish a reseller relationship with a partner.

| Property   | Type                                                           | Description                                                              |
|------------|----------------------------------------------------------------|--------------------------------------------------------------------------|
| url        | string                                                         | The URL used by the customer to establish a relationship with a partner. |
| attributes | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes corresponding to the relationship request.       |