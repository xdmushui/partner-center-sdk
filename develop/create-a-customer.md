---
title: Create a customer
description: Learn how a Cloud Solution Provider (CSP) partner can use Partner Center APIs to create a new customer. Article describes prerequisites and what else happens. 
ms.date: 11/13/2020
ms.service: partner-dashboard
ms.subservice:  partnercenter-sdk
author: dineshvu
ms.author: dineshvu
---

# Create a customer using Partner Center APIs

**Applies to:**

- Partner Center
- Partner Center operated by 21Vianet
- Partner Center for Microsoft Cloud for US Government

This article explains how to create a new customer.

> [!IMPORTANT]
> If you are an indirect provider and you want to create a customer for an indirect reseller, please see [Create a customer for an indirect reseller](create-a-customer-for-an-indirect-reseller.md).

As a cloud solution provider (CSP) partner, when you create a customer you can place orders on behalf of the customer. When you create a customer, you also create:

- An Azure Active Directory (AD) tenant object for the customer.

- A relationship between the reseller and customer, used for delegated admin privileges.

- A user name and password to sign in as an admin for the customer.

Once the customer is created, be sure to save the customer ID and Azure AD details for future use with the Partner Center SDK (for example, account management).

## Prerequisites

- Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.

> [!IMPORTANT]
> To create a customer tenant you must provide a valid physical address during the creation process. An address can be validated by following the steps outlined in the
[Validate an address](validate-an-address.md) scenario. If you create a customer using an invalid address in the sandbox environment, you will not be able to delete that customer tenant.

## C\#

To add a customer:

1. Instantiate a new [**Customer**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer) object. Be sure to fill in the [**BillingProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile) and [**CompanyProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customercompanyprofile).

2. Add the new customer to your [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection by calling [**Create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync).

### C\# example

```csharp
// IAggregatePartner partnerOperations;

var partnerOperations = this.Context.UserPartnerOperations;

var customerToCreate = new Customer()
{
    CompanyProfile = new CustomerCompanyProfile()
    {
        Domain = string.Format(CultureInfo.InvariantCulture,
            "SampleApplication{0}.{1}",
            new Random().Next(),
            this.Context.Configuration.Scenario.CustomerDomainSuffix),
        //// OrganizationRegistrationNumber = "123456" // Please add if in specific country that requires
    },
    BillingProfile = new CustomerBillingProfile()
    {
        Culture = "EN-US",
        Email = "someone@example.com",
        Language = "En",
        CompanyName = "Some Company" + new Random().Next(),
        DefaultAddress = new Address()
        {
            FirstName = "Tania",
            MiddleName = "MiddleName",
            LastName = "Carr",
            AddressLine1 = "One Microsoft Way",
            City = "Redmond",
            State = "WA",
            Country = "US",
            PostalCode = "98052",
            PhoneNumber = ""
        }
    }
};

var newCustomer = partnerOperations.Customers.Create(customerToCreate);
```

**Sample**: [Console test app](console-test-app.md). **Project**: Partner Center SDK Samples **Class**: CreateCustomer.cs

## Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

To create a new customer:

1. Create a new instance of the **CustomerBillingProfile** and the **CustomerCompanyProfile** objects. Be sure to populate the required fields.

2. Create the customer by calling the **IAggregatePartner.getCustomers().create** function.

### Java example

```java
// IAggregatePartner partnerOperations;

Address address = new Address();

address.setFirstName( "Gena" );
address.setLastName( "Soto" );
address.setAddressLine1( "One Microsoft Way" );
address.setCity( "Redmond" );
address.setState( "WA" );
address.setCountry( "US" );
address.setPostalCode( "98052" );
address.setPhoneNumber( "4255550101" );

CustomerBillingProfile billingProfile = new CustomerBillingProfile();

billingProfile.setCulture( "en-US" );
billingProfile.setEmail( "gena@wingtiptoys.com" );
billingProfile.setLanguage( "en" );
billingProfile.setCompanyName( "Wingtip Toys" + new Random().nextInt() );
billingProfile.setDefaultAddress( address );

CustomerCompanyProfile companyProfile = new CustomerCompanyProfile();

companyProfile.setDomain( "WingtipToys" + Math.abs( new Random().nextInt() ) + ".onmicrosoft.com" );

Customer customerToCreate = new Customer();

customerToCreate.setBillingProfile( billingProfile );
customerToCreate.setCompanyProfile( companyProfile );

Customer newCustomer = partnerOperations.getCustomers().create( customerToCreate );
```

## PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

To create a customer execute the [**New-PartnerCustomer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/New-PartnerCustomer.md) command.

```powershell
New-PartnerCustomer -BillingAddressLine1 '1 Microsoft Way' -BillingAddressCity 'Redmond' -BillingAddressCountry 'US' -BillingAddressPostalCode '98052' -BillingAddressState 'WA' -ContactEmail 'jdoe@customer.com' -ContactFirstName 'Jane' -ContactLastName 'Doe' -Culture 'en-US' -Domain 'newcustomer.onmicrosoft.com' -Language 'en' -Name 'New Customer'
```

## REST request

### Request syntax

| Method   | Request URI                                                       |
|----------|-------------------------------------------------------------------|
| **POST** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers HTTP/1.1 |

### Request headers

- This API is idempotent (it will not yield a different result if you call it multiple times).

- A request ID and correlation ID are required.

- For more information, see [Partner Center REST headers](headers.md).

### Request body

This table describes the required properties in the request body.

| Name                              | Type   | Description                                 |
|-----------------------------------|--------|---------------------------------------------|
| [BillingProfile](#billing-profile) | object | The customer's billing profile information. |
| [CompanyProfile](#company-profile) | object | The customer's company profile information. |

#### Billing profile

This table describes the minimum required fields from the [CustomerBillingProfile](customer-resources.md#customerbillingprofile) resource needed to create a new customer.

| Name             | Type                                     | Description                                                                                                                                                                                                     |
|------------------|------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| email            | string                                   | The customer's email address.                                                                                                                                                                                   |
| culture          | string                                   | Their preferred culture for communication and currency, such as "en-US". See [Partner Center supported languages and locales](partner-center-supported-languages-and-locales.md) for the supported cultures. |
| language         | string                                   | The default language. Two character language codes (for example `en` or `fr`) are supported.                                                                                                                                |
| company\_name    | string                                   | The registered company/organization name.                                                                                                                                                                       |
| default\_address | [Address](utility-resources.md#address) | The registered address of the customer's company/organization. See the [Address](utility-resources.md#address) resource for information on any length limitations.                                             |

#### Company profile

This table describes the minimum required fields from the [CustomerCompanyProfile](customer-resources.md#customercompanyprofile) resource needed to create a new customer.

| Name   | Type   | Description                                                  |
|--------|--------|--------------------------------------------------------------|
| domain | string | The customer's domain name, such as contoso.onmicrosoft.com. |
|organizationRegistrationNumber|String|The customer’s organization registration number (also referred to as INN number in certain countries). Only required for customer’s company/organization located in the following countries. Armenia(AM), Azerbaijan(AZ), Belarus(BY), Hungary(HU), Kazakhstan(KZ), Kyrgyzstan(KG), Moldova(MD), Russia(RU), Tajikistan(TJ), Uzbekistan(UZ), Ukraine(UA). For customer’s company/organization located in other countries this should not be specified.|


### Request example

```http
POST https://api.partnercenter.microsoft.com/v1/customers HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 789
Expect: 100-continue
Connection: Keep-Alive

{
    "CompanyProfile": {
        "Domain": "xyz.ccsctp.net",
    },
    "BillingProfile": {
        "Culture": "EN-US",
        "Email": "test@outlook.com",
        "Language": "en",
        "CompanyName": "test company",
        "DefaultAddress": {
            "FirstName": "Test",
            "LastName": "Test",
            "AddressLine1": "One Microsoft Way",
            "City": "Redmond",
            "State": "WA",
            "PostalCode": "98052",
            "Country": "US",
        }
    }
}
```

## REST response

If successful, this API returns a [Customer](customer-resources.md#customer) resource for the new customer. Save the customer ID and Azure AD details for future use with the Partner Center SDK. You will need them for use with account management, for example.

### Response success and error codes

Responses come with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center REST error codes](error-codes.md).

### Response example

```http
HTTP/1.1 201 Created
Content-Length: 834
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CV: ObwhuhD2tUKJoM+Z.0
MS-ServerId: 202010223
Date: Tue, 14 Feb 2017 20:06:02 GMT

{
    "id": "dfd8cc0a-c592-468c-8461-869a38d24738",
    "commerceId": "0a4ce58a-6f96-4273-8035-d9c7d31b9ba4",
    "companyProfile": {
        "tenantId": "dfd8cc0a-c592-468c-8461-869a38d24738",
        "domain": "xyz.ccsctp.net",
        "attributes": {
            "objectType": "CustomerCompanyProfile"
        }
    },
    "billingProfile": {
        "id": "d17c0275-da92-5c33-9032-782ef1d0b69b",
        "email": "test@outlook.com",
        "culture": "en-US",
        "language": "en",
        "companyName": "test company",
        "defaultAddress": {
            "country": "US",
            "city": "Redmond",
            "state": "WA",
            "addressLine1": "One Microsoft Way",
            "postalCode": "98052",
            "firstName": "Test",
            "lastName": "Test",
            "phoneNumber": ""
        },
        "attributes": {
            "etag": "5920358838484612121",
            "objectType": "CustomerBillingProfile"
        }
    },
    "relationshipToPartner": "none",
    "userCredentials": {
        "userName": "admin",
        "password": "=;;n.=s9Z"
    },
    "attributes": {
        "objectType": "Customer"
    }
}
```
