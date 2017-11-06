---
title: ManagedService
description: Managed services are services to which a partner has delegated admin privileges. Partners can provide support for and file service requests on the behalf of their managed services.
MSHAttr:
- 'PreferredSiteName:MSDN'
- 'PreferredLib:/library/PartnerCenter'
ms.assetid: B05E9585-72E4-4330-8721-A88EC4C193D7
---

# ManagedService


**Applies To**

-   Partner Center
-   Partner Center operated by 21Vianet
-   Partner Center for Microsoft Cloud Germany
-   Partner Center for Microsoft Cloud for US Government

Managed services are services to which a partner has delegated admin privileges. Partners can provide support for and file service requests on the behalf of their managed services.

## <span id="ManagedService"></span><span id="managedservice"></span><span id="MANAGEDSERVICE"></span>ManagedService


Describes a managed service.

| Property   | Type                | Description                                              |
|------------|---------------------|----------------------------------------------------------|
| Id         | string              | The managed service id.                                  |
| Name       | string              | The name of the managed service.                         |
| GroupName  | string              | The name of the group to which the service belongs.      |
| Links      | ManagedServiceLinks | The resource links corresponding to the managed service. |
| Attributes | ResourceAttributes  | The metadata attributes corresponding to the agreement.  |

 

## <span id="ManagedServiceLinks"></span><span id="managedservicelinks"></span><span id="MANAGEDSERVICELINKS"></span>ManagedServiceLinks


Contains the links that allow the partner with delegated admin permissions to provide support for the service.

| Property      | Type | Description                 |
|---------------|------|-----------------------------|
| AdminService  | Link | The admin service URI.      |
| ServiceHealth | Link | The service health URI.     |
| ServiceTicket | Link | The service ticket URI.     |
| Self          | Link | The self URI.               |
| Next          | Link | The next page of items.     |
| Previous      | Link | The previous page of items. |

 

 

 




