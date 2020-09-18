---
title: Partner Center .NET SDK release notes
description: Release notes for the latest version of the Partner Center .NET SDK.
ms.date: 07/21/2020
ms.service: partner-dashboard
ms.subservice:  partnercenter-sdk
---

# .NET SDK release notes

The following release notes are available for new versions of [Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter). You can find [.NET SDK samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) on GitHub. You can find the [Partner Center .NET API reference](https://docs.microsoft.com/dotnet/api/?view=partnercenter-dotnet-latest) in the .NET API Browser.

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
