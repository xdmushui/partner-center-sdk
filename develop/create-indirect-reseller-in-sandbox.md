---
title: Create Indirect Reseller in Sandbox
description: Provides information for Sandbox Indirect Providers on enabling end-to-end testing using APIs.
ms.date: 5/24/2021
ms.author: vijvala
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
---

# Create Indirect Reseller in Sandbox

This document shows how to create Sandbox Indirect Providers and enable end-to-end testing using APIs.

**Applies to:** Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany

## Prerequisites

- Credentials as described in [Partner Center Authentication](partner-center-authentication.md). This scenario supports authentication with App+User credentials.

## CSP Indirect Provider

| Production capabilities             | Sandbox capabilities                            |
|-------------------------------------|-------------------------------------------------|
| Sells through the indirect reseller to the end customer | Supported |
| Owns all sales, billing, provisioning, and management/support | Supported |
| Request a partnership with the resellers | Supported |
| View customers by Reseller | Supported |
| Add new customers by resellers | Supported |
| Invite customers | Customer relationship request not supported in Sandbox |
| Sandbox Indirect Provider can select Sandbox IR (MPN ID) as the POR while placing the transaction | Supported |
| Not supported in production | Sandbox Indirect Provider can create Sandbox Indirect Reseller |
| Sandbox MPN ID should be entered, the product MPN ID will not work | Not supported in production |
| Not supported in production | Sandbox Indirect Provider can delete Sandbox Indirect Reseller |

## Sandbox Indirect Provider – Create Sandbox Indirect Reseller

This feature is only available in the Sandbox and gives Sandbox Indirect Providers an ability to create Sandbox Indirect Resellers.

1. Limit of five Sandbox Indirect Resellers allowed per Sandbox Indirect Provider
2. Sandbox Indirect Providers can create customers with `associatedPartnerId` of Sandbox Indirect Reseller
3. Enter the [MPN](/partner-center/mpn-create-a-partner-center-account) ID of a specific region while creating a Sandbox Indirect Reseller. Multiple Sandbox Indirect Resellers can be created with the same Sandbox MPN ID.
4. Only 75 customers are allowed per Sandbox Indirect Provider

## Sandbox Indirect Resellers – View customers

1. Sandbox Indirect Resellers can view the list of sandbox customers by Sandbox Indirect providers.
2. Sandbox Indirect Resellers can manage the customer account by using delegated administrator permissions.

## Create Sandbox Indirect Reseller through API

### REST request

#### Request syntax

| **Method** | **Request URI**                                                        |
|------------|------------------------------------------------------------------------|
| **POST**   | [*{baseURL}*](partner-center-rest-urls.md)/v1//sandboxIndirectReseller |

#### Request headers

- This API is idempotent (it will not yield a different result if you call it multiple times).
- A request ID and correlation ID are required.
- For more information, see [Partner Center REST headers](headers.md).

#### Request body

This table describes the required properties in the request body.

| Property             | Type           | Description                                      |
|----------------------|----------------|--------------------------------------------------|
| mpnId                | string         | The MPN ID for the IR in specific region         |
| tenant               | Dictionary&lt;string, string&gt; | Collection of basic information that defines an account to be created |
| legalBusinessProfile | Dictionary&lt;string, string&gt; | Collection of information that represents the legal business entity such as contact, address, and name |
| organizationProfileLanguage | Dictionary&lt;string, string&gt; | The organization language identifier |

This table describes the required properties in the **tenant** attribute.

| Property           | Type           | Description                         |
|--------------------|----------------|-------------------------------------|
| domainPrefix       | String; unique | Domain for the tenant account       |
| name               | string         | Friendly name of the tenant         |
| displayName        | string         | Display name for the account        |
| adminUserName      | string         | User name for the account for login |
| adminfirstname     | string         | First Name for the admin user       |
| adminlastname      | string         | Last Name for the admin user        |
| adminAlernateEmail | string         | email for the admin user            |
| country            | string         | Country of the account              |
| culture            | string         | Language preference for account     |

This table describes the required properties in the **legalBusinessProfile** attribute.

| Property       | Type                             | Description                          |
|----------------|----------------------------------|--------------------------------------|
| companyName    | string                           | Company name for legal entity        |
| address        | Dictionary&lt;string, string&gt; | Address of the legal entity location |
| primaryContact | Dictionary&lt;string, string&gt; | Contact details of the company       |
| culture        | string                           | Language preferred by the company    |

### Request Example

```http
{
    "mpnId": "6363276",
    "tenant": {
        "domainPrefix": "TipIRIntTest705",
        "name": "TipIRIntTest705",
        "displayName": "TipIRIntTest705",
        "adminUserName": "admin",
        "adminFirstName": "TipIRIntTest705",
        "adminLastName": "TipIRIntTest705",
        "adminAlternateEmail": "TipIRIntTest705@test.com",
        "country": "US",
        "culture": "en-us"
    },
    "legalBusinessProfile": {
        "companyName": "TipIRIntTest705",
        "address": {
            "country": "FR",
            "city": "Issy-les-Moulineaux",
            "state": "",
            "addressLine1": "39-41 quai du Président Roosevelt",
            "addressLine2": "",
            "postalCode": "92130"
        },
        "primaryContact": {
            "firstName": "Sandbox",
            "lastName": "Scenario",
            "email": "Sandbox.Scenario@test.com",
            "phoneNumber": "1234567890"
        },
        "culture": "en-US"
    },
    "organizationProfileLanguage": "en"
}
```

### REST response

If successful, this method returns the populated Sandbox IR resource in the response body.

```http
{

    "accountId": "6f94b119-793c-44c7-862b-c327c9057eab",
    "mpnId": "6363276",
    "tenant": {
        "id": "6f94b119-793c-44c7-862b-c327c9057eab",
        "adminUserAccount": "admin@TipIRIntTest705.onmicrosoft.com",
        "password": "\*\*\*\*\*\*”
    },
    "agreementSignature": {
        "id": "30ac23e7-e200-42cf-a5bc-dd9148cdc632",
        "accountId": "6f94b119-793c-44c7-862b-c327c9057eab",
        "agreementId": "1e18c5b2-e42a-4b84-82c8-d0155aa94c6e",
        "agreementType": "ValueAddedReseller",
        "dateSigned": "2021-02-23T18:10:14.8461137Z",
        "signedByFirstName": "Test123@PLAMUATT2NetNewTip.onmicrosoft.com",
        "signedByUserPrincipalName": "Test123@PLAMUATT2NetNewTip.onmicrosoft.com",
        "signedByUserObjectId": "e6e0c29d-acda-4ef2-b370-d37a4e06fb98",
        "signedByUserTenantId": "0e195b37-4574-4539-bc42-0e539b9684c0",
        "attributes": {
            "objectType": "AgreementSignatureResponse"
        }
    },
    "partnerRelationship": {
        "id": "0e195b37-4574-4539-bc42-0e539b9684c0",
        "name": "PLAMUATT2NetNew",
        "relationshipType": "is\_indirect\_reseller\_of",
        "state": "Active",
        "mpnId": "6363276",
        "attributes": {
            "objectType": "PartnerRelationshipResponse"
        }
    }
}
```
