---
title: Partner Center .NET SDK release notes
description: Release notes for the latest version of the Partner Center .NET SDK.
ms.date: 12/09/2019
ms.service: partner-dashboard
ms.subservice:  partnercenter-sdk
---

# .NET SDK release notes

The following release notes are available for new versions of [Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter). You can find [.NET SDK samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) on GitHub. You can find the [Partner Center .NET API reference](https://docs.microsoft.com/dotnet/api/?view=partnercenter-dotnet-latest) in the .NET API Browser.

## Version 1.15.3

[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/) v1.15.3 is now general availability. Updated REST APIs and [GitHub samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) are also available. The following changes are included in this version:

* Partner Agreement
  * Added the ability for indirect providers to [verify Microsoft Partner Agreement status of indirect resellers](verify-indirect-reseller-mpa-status.md).
* Products
  * The following two interfaces were incorrectly placed under the Microsoft.Store.PartnerCenter.Products namespace. Now, they are located under the Microsoft.Store.PartnerCenter.Customers.Products namespace.
    * ICustomerProductByReservationScope
    * ICustomerSkuByReservationScope
