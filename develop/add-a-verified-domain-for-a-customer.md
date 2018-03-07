---
title: Add a verified domain for a customer
description: This topic explains how to add a verified domain to the list of approved domains for a customer. 
ms.assetid: 
ms.author: v-thpr
ms.date: 3/06/2017
ms.topic: article
ms.prod: partner-center
ms.technology: partner-center-sdk
---

# Add a verified domain for a customer


**Applies To**

-   Partner Center
-   Partner Center operated by 21Vianet
-   Partner Center for Microsoft Cloud Germany
-   Partner Center for Microsoft Cloud for US Government

How to add a verified domain to the list of approved domains for an existing customer.


## <span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>Prerequisites


-   Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.
-   A customer ID (customer-tenant-id). If you do not have a customer's ID, you can look up the ID in Partner Center by choosing the customer from the customers list, selecting Account, then saving their Microsoft ID. 




## <span id="_Request"></span><span id="_request"></span><span id="_REQUEST"></span>REST Request


**Request syntax**

| Request URI                                                                                        |
|----------------------------------------------------------------------------------------------------|
| [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{CustomerTenantId}/verifieddomain HTTP/1.1 |



**URI parameter**

Use the following query parameter to specify the customer you are adding a verified domain for.

| Name                   | Type     | Required | Description                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| CustomerTenantId | guid | Y        | The value is a GUID formatted **CustomerTenantId** that allows you to specify a customer. |



**Request headers**

-   See [Partner Center REST headers](headers.md) for more information.



**Request body**

This table describes the required properties in the request body.

| Name                                                  | Type   | Required                                      | Description                                                |
|-------------------------------------------------------|--------|-----------------------------------------------|--------------------------------------------------------|
| VerifiedDomainName                                    | string | Yes                                           | The verified domain name. |
| [Domain](#domain)                                     | object | Yes                                           | Contains the domain information. |
| [DomainFederationSettings](#domainfederationsettings) | object | Yes (If AuthenticationType = "Federated")     | The domain federation settings to be used if the domain is a "Federated" domain and not a "Managed" domain. |


 

### <span id="domain"></span><span id="domain"></span><span id="DOMAIN"></span>

**Domain**

This table describes the required and optional **Domain** properties in the request body.

| Name               | Type                                     | Required | Description                                                                                                                                                                                                     |
|--------------------|------------------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| AuthenticationType                                    | string           | Yes      | Defines whether the domain is a "Managed" domain or a "Federated" domain. Supported values: Managed, Federated.|
| Capabilities                                          | string           | Yes      | Specifies the domain capabilities. For example, "Email".                  |
| IsDefault                                             | nullable boolean | No       | Indicates whether the domain is the default domain for the tenant. Supported values: True, False, Null.        |
| IsInitial                                             | nullable boolean | No       | Indicates whether the domain is an initial domain. Supported values: True, False, Null.                       |
| Name                                                  | string           | Yes      | The domain name.                                                          |
| RootDomain                                            | string           | No       | The name of the root domain.                                              |
| Status                                                | string           | Yes      | The domain status. For example, "Verified". Supported values:  Unverified, Verified, PendingDeletion.                               |
| VerificationMethod                                    | string           | Yes      | The domain verification method type. Supported values: None, DnsRecord, Email.                                    |

 


### <span id="domainFederationSettings"></span><span id="domainfederationsettings"></span><span id="DOMAINFEDERATIONSETTINGS"></span>

**Domain Federation Settings**

This table describes the required and optional **DomainFederationSettings** properties in the request body.

| Name   | Type   | Required | Description                                                  |
|--------|--------|----------|--------------------------------------------------------------|
| ActiveLogOnUri                         | string           | No      | The logon URI used by rich clients. This is the partner’s STS Auth URL. |
| DefaultInteractiveAuthenticationMethod | string           | No      | Indicates the default authentication method that should be used when an application requires the user to have interactive login. |
| FederationBrandName                    | string           | No      | The federation brand name.        |
| IssuerUri                              | string           | Yes     | The name of the issuer of the certificates.                        |
| LogOffUri                              | string           | Yes     | The logoff URI. This describes the federated domain sign-out URI.        |
| MetadataExchangeUri                    | string           | No      | The URL that specifies the metadata exchange endpoint used for authentication from rich client applications. |
| NextSigningCertificate                 | string           | No      | The certificate used for the coming future by the ADFS V2 STS to sign claims. This is a base64 encoded representation of the certificate. |
| OpenIdConnectDiscoveryEndpoint         | string           | No      | The OpenID Connect Discovery Endpoint of the federated IDP STS. |
| PassiveLogOnUri                        | string           | Yes     | The logon URI used by older passive Clients. This is the address to send federated sign-in requests. |
| PreferredAuthenticationProtocol        | string           | Yes     | The format for the authentication token. For example, "WsFed". Supported values: WsFed, Samlp |
| PromptLoginBehavior                    | string           | Yes     | The prompt login behavior type.  For example, "TranslateToFreshPasswordAuth". Supported values: TranslateToFreshPasswordAuth, NativeSupport, Disabled |
| SigningCertificate                     | string           | Yes     | The certificate currently used by the ADFS V2 STS to sign claims. This is a base64 encoded representation of the certificate. |
| SigningCertificateUpdateStatus         | string           | No      | Indicates the update status of the Signing certificate. |
| SigningCertificateUpdateStatus         | nullable boolean | No      | Indicates whether the IDP STS supports MFA. Supported values: True, False, Null.|

 

**Request example**

```
https://api.partnercenter.microsoft.com/v1/customers/{CustomerTenantId}/verifieddomain HTTP/1.1
Authorization: Bearer <token>
Accept: application/json, text/plain, */*
MS-RequestId: 312b044d-dc41-4b37-c2d5-7d27322d9654
MS-CorrelationId: 7cb67bb7-4750-403d-cc2e-6bc44c52d52c
Content-Type: application/json;charset=utf-8
X-Locale: "en-US"

{
    "VerifiedDomainName": "MyDomainName.com",
    "Domain": {
        "AuthenticationType": "Federated",
        "Capabilities": "None",
        "IsDefault": null,
        "IsInitial": null,
	    "Name": "MyDomainName.com",
	    "RootDomain": null,
	    "Status": "Verified",
	    "VerificationMethod": "None"
    },
    "DomainFederationSettings": {
        "ActiveLogOnUri": "https://sts.microsoftonline.com/FederationPassive/",
        "DefaultInteractiveAuthenticationMethod": "http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password",
        "FederationBrandName": "FederationBrandName",
        "IssuerUri": "MyDomainName.com",
        "LogOffUri": "https://sts.microsoftonline.com/FederationPassive/",
        "MetadataExchangeUri": null,
        "NextSigningCertificate": null,
        "OpenIdConnectDiscoveryEndpoint": "https://sts.contoso.com/adfs/.well-known/openid-configuration",
        "PassiveLogOnUri": "https://sts.microsoftonline.com/Trust/2005/UsernameMixed", 
        "PreferredAuthenticationProtocol": "WsFed",
        "PromptLoginBehavior": "TranslateToFreshPasswordAuth",
        "SigningCertificate": <Certificate Signature goes here>,
        "SigningCertificateUpdateStatus": null,
        "SupportsMfa": true
    }
}
```

