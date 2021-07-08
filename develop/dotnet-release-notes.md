---
title: Partner Center .NET SDK release notes
description: Release notes for the latest version of the Partner Center .NET SDK.
ms.date: 09/18/2020
ms.service: partner-dashboard
ms.subservice:  partnercenter-sdk
---

# .NET SDK release notes

The following release notes are available for new versions of [Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter). You can find [.NET SDK samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) on GitHub. You can find the [Partner Center .NET API reference](/dotnet/api/?view=partnercenter-dotnet-latest&preserve-view=true) in the .NET API Browser.

## Version 2.0.1

[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/2.0.1) v2.0.1 is now general availability. Updated [GitHub samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) are also available. The following changes are included in this version:

> [!NOTE]
> Some of changes introduced as part of New Commerce Experiences (“NCE”) which are currently available based on invitation only to partners who are part of the M365/D365 new commerce experience technical preview. Partners who are not part of New commerce private preview should not notice impacts and should be backward compatible.

### Common
* Change on the reference to authentication library – The reference is changed from Azure Active Directory Authentication Library ([ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-dotnet)) to Microsoft Authentication Library ([MSAL](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet))

  Following changes should be made to ensure MSAL runs correctly on your application or .Net sample:

  * Add ‘https://login.microsoftonline.com/common/oauth2/nativeclient’ as RedirectUrl for Mobile and desktop applications
  * Add **Domain** into UserAuthentication section in your application configuration file. 

    Domain is the Azure Active Directory domain or tenant Id where the Azure AD application was created

* [Erro codes](error-codes.md) – New error code added 
  * 408: Request timeout
  * 504: Gateway timeout 

### Billing

* [Invoice line-items](get-invoiceline-items.md) - new attributes added to following APIs:
  GET /invoices/{invoice-id}/lineitems?provider={provider}&invoicelineitemtype=billinglineitems
  GET /invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=billinglineitems

  New attributes: 
  * productQualifiers
  * subscriptionStartDate
  * subscriptionEndDate
  * referenceId
  * creditReasonCode  (Only applicable to NCE)
  * promotionId 


* [Daily rated usage Line-items](get-invoice-billed-consumption-lineitems.md) – new attributes added to following API: 
  GET /invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=usagelineitems
  * hasPartnerEarnedCredit (Only applicable to NCE)
  * creditType (Only applicable to NCE)
  * rateOfCredit (Only applicable to NCE)


### Subscription Manage 

* [Subscription Resources](subscription-resources.md) – New property added. 
  * CancellationAllowedUntilDate  - (Only applicable to NCE)

* Transition Resources (Only applicable to NCE) – New property added 
  * FromSubscriptionId

### Customer 
* [Validate an address](validate-an-address.md) – Response is changed from a Boolean to a new model for API: 
  POST /validations/address
  
  New response model: 
  * AddressValidationResponse

* Customer’s qualification synchronous API is deprecated.  


## Version 1.17.0

[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.17.0) v1.17.0 is now general availability. Updated [GitHub samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) are also available. The following changes are included in this version:

* Audit Updated - Added new operation types for knowing when the customer approved and terminated DAP
  * [DapAdminRelationshipApproved](auditing-resources.md)
  * [DapAdminRelationshipTerminated](auditing-resources.md)

* Audit Updated – Added new resource and operation types for supporting the customer directory role scenario
  * Resource type "[CustomerDirectoryRole](auditing-resources.md)"
  * Operation types "[AddUserMember](auditing-resources.md)" and "[RemoveUserMember](auditing-resources.md)"

* SDK Updates to Customers Account - Support for following API's
  * GET /customers/{customer-tenant-id}/directSignedMicrosoftCustomerAgreementStatus
  * GET /customers/{customer-tenant-id}/qualifications 
  * POST /customers/{customer_id}/qualifications?code={validationCode}

* **Following changes introduced as part of New Commerce which are currently available based on invitation only to partners who are part of the M365/D365 new commerce experience technical preview.** Partners who are not part of New commerce private preview should not notice impacts and should be backward compatible.
  * Catalog Changes:
    * GET /products/{product-id}/skus/{sku-id}
  * Purchase and Manage:
    * GET /customers/{customerId}/subscriptions
    * GET /customers/{customerId}/subscriptions/{subscriptionId}
    * PATCH /customers/{customerId}/subscriptions/{subscriptionId}
    * GET /customers/{customerId}/subscriptions/{subscriptionId}/transitioneligibilities
    * GET /customers/{customerId}/subscriptions/{subscriptionId}/transitions
    * POST /customers/{customerId}/subscriptions/{subscriptionId}/transitions


## Version 1.16.3

[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.3) v1.16.3 is now general availability. Updated [GitHub samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) are also available. The following changes are included in this version:

* SelfServePolicies - new functionality added
  * [GetSelfServePolicies](get-a-self-serve-policy-by-id.md)
  * [GetListOfSelfServicePolicies](get-a-list-of-self-serve-policies.md)
  * [CreateSelfServePolicies](create-a-self-serve-policy.md)
  * [UpdateSelfServePolicies](update-a-self-serve-policy.md)
  * [DeleteSelfServePolicies](delete-a-self-serve-policy.md)

* Customers Company Profile
  * Added [OrganizationRegistrationNumber](create-a-customer.md)

* CustomerBillingProfile.DefaultAddress
  * Added MiddleName

## Version 1.16.2

[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.2) v1.16.2 is now general availability. Updated [GitHub samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) are also available. The following changes are included in this version:

* Update supported operation types for Audit Record. The newly added ones are:
  * CreateSelfServePolicy
  * UpdateSelfServePolicy
  * DeleteSelfServePolicy
  * RemovePartnerRelationship
  * DeleteTipCustomer
  * CreateRelatedReferral
  * UpdateRelatedReferral

* Service request creation is now deprecated
* Support topics are now deprecated


## Version 1.16.1

[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.1) v1.16.1 is now general availability. Updated [GitHub samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) are also available. The following changes are included in this version:

We have migrated the existing Microsoft Partner Center SDK from .NET Framework to .NET Standard 2.0 platform. This will make the SDK compatible with existing applications using .NET Framework 4.6.1 and above. The SDK will support .NET Core 2.0 and above. Check [.NET implementation support](/dotnet/standard/net-standard) before porting it to existing applications.   


## Version 1.15.3
[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.15.3) v1.15.3 is now general availability. Updated REST APIs and [GitHub samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) are also available. The following changes are included in this version:

* Partner Agreement
  * Added the ability for indirect providers to [verify Microsoft Partner Agreement status of indirect resellers](verify-indirect-reseller-mpa-status.md).
* Products
  * The following two interfaces were incorrectly placed under the Microsoft.Store.PartnerCenter.Products namespace. Now, they are located under the Microsoft.Store.PartnerCenter.Customers.Products namespace.
    * ICustomerProductByReservationScope
    * ICustomerSkuByReservationScope
