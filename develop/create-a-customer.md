---
title: Create a customer
description: This topic explains how to create a new customer. If you are an indirect provider and you want to create a customer for an indirect reseller, please see Create a customer for an indirect reseller.
ms.assetid: 7EA3E23F-0EA8-49CB-B98A-C4B74F559873
ms.date: 11/29/2018
ms.localizationpriority: medium
---

# Create a customer

**Applies To**

-   Partner Center
-   Partner Center operated by 21Vianet
-   Partner Center for Microsoft Cloud for US Government

This topic explains how to create a new customer. If you are an indirect provider and you want to create a customer for an indirect reseller, please see [Create a customer for an indirect reseller](create-a-customer-for-an-indirect-reseller.md).

As a cloud solution provider (CSP) partner, when you create a customer you can place orders on behalf of the customer. When you create a customer, you also create:

-   An Azure Active Directory (AD) tenant object for the customer.
-   A relationship between the reseller and customer, used for delegated admin privileges.
-   A user name and password to sign in as an admin for the customer.

Once the customer is created, save the customer ID and Azure AD details for future use with the Partner Center SDK. You will need them for use with account management, for example.

## <span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>Prerequisites

Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.

## <span id="Examples"></span><span id="examples"><span id="EXAMPLES"></span>Examples

### C#

To add a customer, instantiate a new [**Customer**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.customers.customer) object. Be sure to fill in the [**BillingProfile**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile) and [**CompanyProfile**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.customers.customercompanyprofile). Then, add it to your [**IAggregatePartner.Customers**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection by calling [**Create**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) or [**CreateAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync).

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
            this.Context.Configuration.Scenario.CustomerDomainSuffix)
    },
    BillingProfile = new CustomerBillingProfile()
    {
        Culture = "EN-US",
        Email = "SomeEmail@Outlook.com",
        Language = "En",
        CompanyName = "Some Company" + new Random().Next(),
        DefaultAddress = new Address()
        {
            FirstName = "Tania",
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

### Java

To create a new customer create a new instance of the **CustomerBillingProfile** and the **CustomerCompanyProfile** objects. Be sure to populate the required fields. Then, create the customer by calling the **IAggregatePartner.getCustomers().create** function.

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

### PowerShell

To create a customer execute the [**New-ParnterCustomer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/New-PartnerCustomer.md) command. 

```powershell
New-PartnerCustomer -BillingAddressLine1 '1 Microsoft Way' -BillingAddressCity 'Redmond' -BillingAddressCountry 'US' -BillingAddressPostalCode '98052' -BillingAddressState 'WA' -ContactEmail 'jdoe@customer.com' -ContactFirstName 'Jane' -ContactLastName 'Doe' -Culture 'en-US' -Domain 'newcustomer.onmicrosoft.com' -Language 'en' -Name 'New Customer'
```

## <span id="_Request"></span><span id="_request"></span><span id="_REQUEST"></span> Request

**Request syntax**

| Method   | Request URI                                                       |
|----------|-------------------------------------------------------------------|
| **POST** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers HTTP/1.1 |



**Request headers**

-   This API is idempotent (it will not yield a different result if you call it multiple times).
-   A request ID and correlation ID are required.
-   See [Partner Center REST headers](headers.md) for more information.

**Request body**

This table describes the required properties in the request body.

| Name                              | Type   | Description                                 |
|-----------------------------------|--------|---------------------------------------------|
| [BillingProfile](#billingprofile) | object | The customer's billing profile information. |
| [CompanyProfile](#companyprofile) | object | The customer's company profile information. |



### <span id="billingProfile"></span><span id="billingprofile"></span><span id="BILLINGPROFILE"></span>

**Billing Profile**

This table describes the minimum required fields from the [CustomerBillingProfile](customers.md#customerbillingprofile) resource needed to create a new customer.

| Name             | Type                                     | Description                                                                                                                                                                                                     |
|------------------|------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| email            | string                                   | The customer's email address.                                                                                                                                                                                   |
| culture          | string                                   | Their preferred culture for communication and currency, such as "en-US". See [Table of Language Culture Names](https://msdn.microsoft.com/library/ee825488%28v=cs.20%29.aspx) for the supported cultures. |
| language         | string                                   | The default language. Two character language codes (e.g., en, fr) are supported.                                                                                                                                |
| company\_name    | string                                   | The registered company/organization name.                                                                                                                                                                       |
| default\_address | [Address](utility-resources.md#address) | The registered address of the customer's company/organization. See the [Address](utility-resources.md#address) resource for information on any length limitations.                                             |



### <span id="companyProfile"></span><span id="companyprofile"></span><span id="COMPANYPROFILE"></span>

**Company Profile**

This table describes the minimum required fields from the [CustomerCompanyProfile](customers.md#customercompanyprofile) resource needed to create a new customer.

| Name   | Type   | Description                                                  |
|--------|--------|--------------------------------------------------------------|
| domain | string | The customer's domain name, such as contoso.onmicrosoft.com. |



**Request example**

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

## <span id="Response"></span><span id="response"></span><span id="RESPONSE"></span>Response


If successful, this API returns a [Customer](customers.md) resource for the new customer. Save the customer ID and Azure AD details for future use with the Partner Center SDK. You will need them for use with account management, for example.

**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center REST error codes](error-codes.md).

**Response example**

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








