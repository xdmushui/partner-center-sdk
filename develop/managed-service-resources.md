---
title: Managed service resources
description: Managed services are services to which a partner has delegated admin privileges. Partners can provide support for and file service requests on the behalf of their managed services.
ms.assetid: B05E9585-72E4-4330-8721-A88EC4C193D7
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice:  partnercenter-sdk
ms.localizationpriority: medium
---

# Managed service resources


**Applies To**

- Partner Center
- Partner Center operated by 21Vianet
- Partner Center for Microsoft Cloud Germany
- Partner Center for Microsoft Cloud for US Government

Managed services are services to which a partner has delegated admin
privileges. Partners can provide support for and file service requests
on the behalf of their managed services.

## <span id="ManagedService"/><span id="managedservice"/><span id="MANAGEDSERVICE"/>ManagedService


Describes a managed service.

| Property   | Type                | Description                                              |
|------------|---------------------|----------------------------------------------------------|
| Id         | string              | The managed service id.                                  |
| Name       | string              | The name of the managed service.                         |
| GroupName  | string              | The name of the group to which the service belongs.      |
| Links      | ManagedServiceLinks | The resource links corresponding to the managed service. |
| Attributes | ResourceAttributes  | The metadata attributes corresponding to the agreement.  |



## <span id="ManagedServiceLinks"/><span id="managedservicelinks"/><span id="MANAGEDSERVICELINKS"/>ManagedServiceLinks


Contains the links that allow the partner with delegated admin
permissions to provide support for the service.

| Property      | Type | Description                 |
|---------------|------|-----------------------------|
| AdminService  | Link | The admin service URI.      |
| ServiceHealth | Link | The service health URI.     |
| ServiceTicket | Link | The service ticket URI.     |
| Self          | Link | The self URI.               |
| Next          | Link | The next page of items.     |
| Previous      | Link | The previous page of items. |


