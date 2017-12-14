---
title: Partner Center Managed API Reference
description: The Partner Center SDK includes a managed API and a REST API for partners to use to manage customer, subscription, and order data.
ms.author: v-thpr
ms.date: 12/15/2017
ms.topic: article
ms.prod: partner-center
ms.technology: partner-center-sdk
---
#Partner Center Managed API Reference

The Partner Center managed API helps partners integrate their existing customer relationship management or billing software with the Microsoft systems that manage customer accounts, place orders, manage subscriptions, and handle support requests in Partner Center. 
The Managed API also includes token management so that you don’t have to refresh your Azure AD tokens and authentication each hour, and a simple interface library for network calls with retries.

For more information about what the API can do, including sample code, see developer [scenarios](scenarios.md).
Before you begin coding, read the [Get started](get-started.md) section for information about setting up your test and production accounts, getting authentication working, and finding the sample code. 
The managed API includes the following namespaces: 

[Microsoft.Store.PartnerCenter](https://review.docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter)
[Microsoft.Store.PartnerCenter.Analytics](https://review.docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Analytics)
[Microsoft.Store.PartnerCenter.AuditRecords](https://review.docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.AuditRecords)
[Microsoft.Store.PartnerCenter.CountryValidationRules](https://review.docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.CountryValidationRules)
[Microsoft.Store.PartnerCenter.CustomerDirectoryRoles](https://review.docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.CustomerDirectoryRoles)
[Microsoft.Store.PartnerCenter.Customers](https://review.docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Customers)
[Microsoft.Store.PartnerCenter.Customers.Profiles](https://review.docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Customers.Profiles)
[Microsoft.Store.PartnerCenter.Customers.ServiceCosts](https://review.docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Customers.ServiceCosts)
[Microsoft.Store.PartnerCenter.CustomerUsers](https://review.docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.CustomerUsers)
[Microsoft.Store.PartnerCenter.DevicesDeployment](https://review.docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.DevicesDeployment)
[Microsoft.Store.PartnerCenter.Domains](https://review.docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Domains)
[Microsoft.Store.PartnerCenter.Enumerators](https://review.docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Enumerators)
[Microsoft.Store.PartnerCenter.Exceptions](https://review.docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Exceptions)
[Microsoft.Store.PartnerCenter.Extensions](https://review.docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Extensions)
[Microsoft.Store.PartnerCenter.Factory](https://review.docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Factory)
[Microsoft.Store.PartnerCenter.GenericOperations](https://review.docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.GenericOperations)
[Microsoft.Store.PartnerCenter.Invoices](https://review.docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Invoices)
[Microsoft.Store.PartnerCenter.ManagedServices](https://review.docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.ManagedServices)
[Microsoft.Store.PartnerCenter.Models](https://review.docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Models)
[Microsoft.Store.PartnerCenter.Models.Analytics](https://review.docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Models.Analytics)
[Microsoft.Store.PartnerCenter.Models.Auditing](https://review.docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Models.Auditing)
[Microsoft.Store.PartnerCenter.Models.CountryValidationRules](https://review.docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Models.CountryValidationRules)
[Microsoft.Store.PartnerCenter.Models.Customers](https://review.docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Models.Customers)
[Microsoft.Store.PartnerCenter.Models.DevicesDeployment](https://review.docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Models.DevicesDeployment)
[Microsoft.Store.PartnerCenter.Models.Invoices](https://review.docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Models.Invoices)
[Microsoft.Store.PartnerCenter.Models.Licenses](https://review.docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Models.Licenses)
[Microsoft.Store.PartnerCenter.Models.ManagedServices](https://review.docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Models.ManagedServices)
[Microsoft.Store.PartnerCenter.Models.Offers](https://review.docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Models.Offers)
[Microsoft.Store.PartnerCenter.Models.Orders](https://review.docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Models.Orders)
[Microsoft.Store.PartnerCenter.Models.Partners](https://review.docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Models.Partners)
[Microsoft.Store.PartnerCenter.Models.Query](https://review.docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Models.Query)
[Microsoft.Store.PartnerCenter.Models.RateCards](https://review.docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Models.RateCards)
[Microsoft.Store.PartnerCenter.Models.Relationships](https://review.docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Models.Relationships)
[Microsoft.Store.PartnerCenter.Models.RelationshipRequests](https://review.docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Models.RelationshipRequests)
[Microsoft.Store.PartnerCenter.Models.Roles](https://review.docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Models.Roles)
[Microsoft.Store.PartnerCenter.Models.ServiceCosts](https://review.docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Models.ServiceCosts)
[Microsoft.Store.PartnerCenter.Models.ServiceIncidents](https://review.docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Models.ServiceIncidents)
[Microsoft.Store.PartnerCenter.Models.ServiceRequests](https://review.docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Models.ServiceRequests)
[Microsoft.Store.PartnerCenter.Models.Subscriptions](https://review.docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Models.Subscriptions)
[Microsoft.Store.PartnerCenter.Models.Usage](https://review.docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Models.Usage)
[Microsoft.Store.PartnerCenter.Models.Users](https://review.docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Models.Users)
[Microsoft.Store.PartnerCenter.Models.Utilizations](https://review.docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Models.Utilizations)
[Microsoft.Store.PartnerCenter.Offers](https://review.docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Offers)
[Microsoft.Store.PartnerCenter.Orders](https://review.docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Orders)
[Microsoft.Store.PartnerCenter.Profiles](https://review.docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Profiles)
[Microsoft.Store.PartnerCenter.Qualification](https://review.docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Qualification)
[Microsoft.Store.PartnerCenter.RateCards](https://review.docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.RateCards)
[Microsoft.Store.PartnerCenter.Relationships](https://review.docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Relationships)
[Microsoft.Store.PartnerCenter.RelationshipRequests](https://review.docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.RelationshipRequests)
[Microsoft.Store.PartnerCenter.RequestContext](https://review.docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.RequestContext)
[Microsoft.Store.PartnerCenter.ServiceIncidents](https://review.docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.ServiceIncidents)
[Microsoft.Store.PartnerCenter.ServiceRequests](https://review.docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.ServiceRequests)
[Microsoft.Store.PartnerCenter.SubscribedSkus](https://review.docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.SubscribedSkus)
[Microsoft.Store.PartnerCenter.Subscriptions](https://review.docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Subscriptions)
[Microsoft.Store.PartnerCenter.Usage](https://review.docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Usage)
[Microsoft.Store.PartnerCenter.Utilization](https://review.docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Utilization)
[Microsoft.Store.PartnerCenter.Validations](https://review.docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Validations)
