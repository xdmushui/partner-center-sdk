---
title: Partner Center Managed API Reference
description: The Partner Center SDK includes a managed API and a REST API for partners to use to manage customer, subscription, and order data.
ms.date: 12/15/2017
ms.localizationpriority: medium
---
#Partner Center Managed API Reference

The Partner Center managed API helps partners integrate their existing customer relationship management or billing software with the Microsoft systems that manage customer accounts, place orders, manage subscriptions, and handle support requests in Partner Center. 
The Managed API also includes token management so that you don’t have to refresh your Azure AD tokens and authentication each hour, and a simple interface library for network calls with retries.

For more information about what the API can do, including sample code, see developer [scenarios](scenarios.md).
Before you begin coding, read the [Get started](get-started.md) section for information about setting up your test and production accounts, getting authentication working, and finding the sample code. 
The managed API includes the following namespaces: 

 - [Microsoft.Store.PartnerCenter](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter)
 - [Microsoft.Store.PartnerCenter.Analytics](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Analytics)
 - [Microsoft.Store.PartnerCenter.AuditRecords](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.AuditRecords)
 - [Microsoft.Store.PartnerCenter.CountryValidationRules](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.CountryValidationRules)
 - [Microsoft.Store.PartnerCenter.CustomerDirectoryRoles](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.CustomerDirectoryRoles)
 - [Microsoft.Store.PartnerCenter.Customers](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Customers)
 - [Microsoft.Store.PartnerCenter.Customers.Profiles](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Customers.Profiles)
 - [Microsoft.Store.PartnerCenter.Customers.ServiceCosts](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Customers.ServiceCosts)
 - [Microsoft.Store.PartnerCenter.CustomerUsers](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.CustomerUsers)
 - [Microsoft.Store.PartnerCenter.DevicesDeployment](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.DevicesDeployment)
 - [Microsoft.Store.PartnerCenter.Domains](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Domains)
 - [Microsoft.Store.PartnerCenter.Enumerators](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Enumerators)
 - [Microsoft.Store.PartnerCenter.Exceptions](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Exceptions)
 - [Microsoft.Store.PartnerCenter.Extensions](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Extensions)
 - [Microsoft.Store.PartnerCenter.Factory](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Factory)
 - [Microsoft.Store.PartnerCenter.GenericOperations](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.GenericOperations)
 - [Microsoft.Store.PartnerCenter.Invoices](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Invoices)
 - [Microsoft.Store.PartnerCenter.ManagedServices](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.ManagedServices)
 - [Microsoft.Store.PartnerCenter.Models](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Models)
 - [Microsoft.Store.PartnerCenter.Models.Analytics](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Models.Analytics)
 - [Microsoft.Store.PartnerCenter.Models.Auditing](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Models.Auditing)
 - [Microsoft.Store.PartnerCenter.Models.CountryValidationRules](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Models.CountryValidationRules)
 - [Microsoft.Store.PartnerCenter.Models.Customers](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Models.Customers)
 - [Microsoft.Store.PartnerCenter.Models.DevicesDeployment](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Models.DevicesDeployment)
 - [Microsoft.Store.PartnerCenter.Models.Invoices](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Models.Invoices)
 - [Microsoft.Store.PartnerCenter.Models.Licenses](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Models.Licenses)
 - [Microsoft.Store.PartnerCenter.Models.ManagedServices](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Models.ManagedServices)
 - [Microsoft.Store.PartnerCenter.Models.Offers](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Models.Offers)
 - [Microsoft.Store.PartnerCenter.Models.Orders](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Models.Orders)
 - [Microsoft.Store.PartnerCenter.Models.Partners](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Models.Partners)
 - [Microsoft.Store.PartnerCenter.Models.Query](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Models.Query)
 - [Microsoft.Store.PartnerCenter.Models.RateCards](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Models.RateCards)
 - [Microsoft.Store.PartnerCenter.Models.Relationships](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Models.Relationships)
 - [Microsoft.Store.PartnerCenter.Models.RelationshipRequests](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Models.RelationshipRequests)
 - [Microsoft.Store.PartnerCenter.Models.Roles](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Models.Roles)
 - [Microsoft.Store.PartnerCenter.Models.ServiceCosts](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Models.ServiceCosts)
 - [Microsoft.Store.PartnerCenter.Models.ServiceIncidents](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Models.ServiceIncidents)
 - [Microsoft.Store.PartnerCenter.Models.ServiceRequests](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Models.ServiceRequests)
 - [Microsoft.Store.PartnerCenter.Models.Subscriptions](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Models.Subscriptions)
 - [Microsoft.Store.PartnerCenter.Models.Usage](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Models.Usage)
 - [Microsoft.Store.PartnerCenter.Models.Users](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Models.Users)
 - [Microsoft.Store.PartnerCenter.Models.Utilizations](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Models.Utilizations)
 - [Microsoft.Store.PartnerCenter.Offers](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Offers)
 - [Microsoft.Store.PartnerCenter.Orders](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Orders)
 - [Microsoft.Store.PartnerCenter.Profiles](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Profiles)
 - [Microsoft.Store.PartnerCenter.Qualification](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Qualification)
 - [Microsoft.Store.PartnerCenter.RateCards](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.RateCards)
 - [Microsoft.Store.PartnerCenter.Relationships](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Relationships)
 - [Microsoft.Store.PartnerCenter.RelationshipRequests](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.RelationshipRequests)
 - [Microsoft.Store.PartnerCenter.RequestContext](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.RequestContext)
 - [Microsoft.Store.PartnerCenter.ServiceIncidents](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.ServiceIncidents)
 - [Microsoft.Store.PartnerCenter.ServiceRequests](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.ServiceRequests)
 - [Microsoft.Store.PartnerCenter.SubscribedSkus](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.SubscribedSkus)
 - [Microsoft.Store.PartnerCenter.Subscriptions](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Subscriptions)
 - [Microsoft.Store.PartnerCenter.Usage](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Usage)
 - [Microsoft.Store.PartnerCenter.Utilization](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Utilization)
 - [Microsoft.Store.PartnerCenter.Validations](https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Store.PartnerCenter.Validations)
