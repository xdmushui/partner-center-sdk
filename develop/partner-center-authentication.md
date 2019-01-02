---
title: Partner Center authentication
description: Partner Center uses Azure AD for authentication, and to use the Partner Center APIs you must configure your authentication settings correctly.
ms.assetid: 2307F2A8-7BD4-4442-BEF7-F065F16DA0B2
ms.date: 01/02/2019
ms.localizationpriority: medium
---

# Partner Center Authentication

**Applies To**

- Partner Center
- Partner Center operated by 21Vianet
- Partner Center for Microsoft Cloud Germany
- Partner Center for Microsoft Cloud for US Government

Partner Center utilizes Azure Active Directory for authentication. When interacting with the Partner Center API, SDK, or PowerShell module you must correctly configure an Azure AD application and then request an access token. Access tokens obtained using app only or app + user authentication can be used with the Partner Center. However, there are two important items that need to be considered

- Effective February 4, 2019 you must utilize multi-factor authentication when accessing the Partner Center API using app + user authentication. To find more information regarding this change, see [Enable secure application model](enable-secure-app-model.md)
- Not all of the operations the Partner Center API support app only authentication. This means there certain scenarios where you will be required to use app + user authentication. Under the *Prerequisites* heading, each [Scenario](https://docs.microsoft.com/partner-center/develop/scenarios) you will find documentation that states whether app only, app + user, app only, or both are supported.

## App Only Authentication

If you would like to use app only authentication to access the Partner Center API, SDK, or PowerShell module then you can do so by leveraging the following

# [.NET](#tab/dotnet-app-only)

```csharp
public static IAggregatePartner GetPartnerCenterTokenUsingAppCredentials()
{
    IPartnerCredentials partnerCredentials = 
        PartnerCredentials.Instance.GenerateByApplicationCredentials(
            PartnerApplicationConfiguration.ApplicationId, 
            PartnerApplicationConfiguration.ApplicationSecret, 
            PartnerApplicationConfiguration.ApplicationDomain);

    // Create operations instance with partnerCredentials.
    return PartnerService.Instance.CreatePartnerOperations(partnerCredentials);
}
```

# [Java](#tab/java-app-only)

```java
public IAggregatePartner getAppPartnerOperations()
{
    IPartnerCredentials appCredentials =
        PartnerCredentials.getInstance().generateByApplicationCredentials(
        PartnerApplicationConfiguration.getApplicationId(), 
        PartnerApplicationConfiguration.getApplicationSecret(), 
        PartnerApplicationConfiguration.getApplicationDomain());

    return PartnerService.getInstance().createPartnerOperations( appCredentials );
}
```

# [PowerShell](#tab/powershell-app-only)

```powershell
$credential = Get-Credential
Connect-PartnerCenter -Credential $credential -ServicePrincipal -TenantId '<TenantId>'
```

> [!NOTE]  
> When you are prompted for credentials specify the client identifier as the username and the client secret as the password.

# [REST](#tab/rest-app-only)

**Request**

```http
POST https://login.microsoftonline.com/{tenanId}/oauth2/token HTTP/1.1
Accept: application/json
return-client-request-id: true
Content-Type: application/x-www-form-urlencoded; charset=utf-8
Host: login.microsoftonline.com
Content-Length: 194
Expect: 100-continue

resource=https%3A%2F%2Fgraph.windows.net&client_id={client-id-here}&client_secret={client-secret-here}&grant_type=client_credentials
```

**Response**

```http
HTTP/1.1 200 OK
Cache-Control: no-cache, no-store
Pragma: no-cache
Content-Type: application/json; charset=utf-8
Expires: -1
Content-Length: 1406

{"token_type":"Bearer","expires_in":"3600","ext_expires_in":"3600","expires_on":"1546469802","not_before":"1546465902","resource":"https://graph.windows.net","access_token":"value-has-been-removed"}
```

---