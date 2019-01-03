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

- You must utilize multi-factor authentication when accessing the Partner Center API using app + user authentication. To find more information regarding this change, see [Enable secure application model](enable-secure-app-model.md)
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

## App + User Authentication

Historically the [resource owner password credentials grant](https://tools.ietf.org/html/rfc6749#section-4.3) has been used to request an access token for use with the Partner Center API, SDK, or PowerShell module. This is where you request an access token from Azure Active Directory using a client identifier and user credentials. This approach will no longer work because to access the Partner Center Dashboard or the Partner Center API, when using app + user authentication, multi-factor authentication is required. To comply with this requirement Microsoft has introduced a secure, scalable framework for authenticating Cloud Solution Provider (CSP) partners and control panel vendors (CPV) using multi-factor authentication. This framework is known as the Secure Application Model, and it is comprised of a consent process and a request for an access token using a refresh token.

### Partner Consent

The partner consent process is an interactive process where the partner authenticates using multi-factor authentication, consents to the application, and a refresh token is stored in a secure repository such as Azure Key Vault. It is recommended that a dedicated account for integration purposes be used for this process.

> [!IMPORTANT]  
> The appropriate multi-factor authentication solution should be enabled for the service account used in the partner consent process. If it is not then the resulting refresh token will not be complaint with security requirements.

#### Samples

The partner consent process can be performing in a number of ways. To help partners understand how to perform each operation required in this process the following samples have been developed. Please note that these are samples, so it is important when you implement the appropriate solution in your environment you develop a solution that is complaint with your code standard and security policies.

# [.NET](#tab/dotnet-partner-consent)

The [partner consent](https://github.com/Microsoft/Partner-Center-DotNet-Samples/tree/master/secure-app-model/keyvault) sample project demonstrates how to utilize a website developed using ASP.NET to capture consent, request a refresh token, and secure store in Azure Key Vault. Perform the following to create the required prerequisites for this sample

1. Create an instance of Azure Key Vault using the Azure management portal or the following PowerShell commands. Before executing the command be sure to modify the parameter values accordingly. The vault name must be unique.

    ```azurepowershell-interactive
    Login-AzureRmAccount

    # Create a new resource group
    New-AzureRmResourceGroup -Name ContosoResourceGroup -Location EastUS

    New-AzureRmKeyVault -Name 'Contoso-Vault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East US'
    ```

    If you need help creating the instance of Azure Key Vault see [Quickstart: Set and retrieve a secret from Azure Key Vault using the Azure portal](https://docs.microsoft.com/azure/key-vault/quick-create-portal) or [Quickstart: Set and retrieve a secret from Azure Key Vault using PowerShell](https://docs.microsoft.com/azure/key-vault/quick-create-powershell) for step by step direction on how to create an instance of Azure Key Vault and set and retrieve a secret.

2. Create an Azure AD Application and a key using the Azure management portal or the following commands.

    ```azurepowershell-interactive
    Connect-AzureAD

    $SessionInfo = Get-AzureADCurrentSessionInfo

    $app = New-AzureADApplication -DisplayName 'My Vault Access App' -IdentifierUris 'https://$($SessionInfo.TenantDomain)/$((New-Guid).ToString())'
    $password = New-AzureADApplicationPasswordCredential -ObjectId $app.ObjectId

    Write-Host "ApplicationId       = $($app.AppId)"
    Write-Host "ApplicationSecret   = $($password.Value)"
    ```

    Be sure to document the application identifier and secret values because they will be used in the steps below.

3. Grant the newly create Azure AD application the read secrets permissions using the Azure management portal or the following commands.

    ```azurepowershell-interactive
    $app = Get-AzureADApplication -Filter {AppId -eq 'ENTER-APP-ID-HERE'}

    Set-AzureRmKeyVaultAccessPolicy –VaultName ContosoVault –ObjectId $app.ObjectId –PermissionsToSecrets get
    ```

4. Create an Azure AD application that is configured for Partner Center. Preform the following to complete this step

    - Browse to the [App management](https://partner.microsoft.com/pcv/apiintegration/appmanagement) feature of the Partner Center Dashboard
    - Click *Add new web app* to create a new Azure AD application.

    Be sure to document the *App ID*, *Account ID**, and *Key* values because they will be used in the steps below.

5. Clone the [Partner-Center-DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) repository using Visual Studio or the following command

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-DotNet-Samples.git
    ```

6. Open the *PartnerConsent* project found in the `Partner-Center-DotNet-Samples\secure-app-model\keyvault` directory.
7. Populate the application settings found in the `web.config`

    ```xml
    <!-- AppID that represents CSP application -->
    <add key="ida:CSPApplicationId" value="" />
    <!-- 
        Please use certificate as your client secret and deploy the certificate to your environment.
        The following application secret is for sample application only. please do not use secret directly from the config file.    
    -->
    <add key="ida:CSPApplicationSecret" value="" />

    <!-- 
        Endpoint address for the instance of Azure KeyVault. This is
        the DNS Name for the instance of Key Vault that you provisioned.
     -->
    <add key="KeyVaultEndpoint" value="" />

    <!-- App ID that is given access for KeyVault to store refresh tokens -->
    <add key="ida:KeyVaultClientId" value="" />

    <!-- 
        Please use certificate as your client secret and deploy the certificate
        to your environment. The following application secret is for sample
        application only. please do not use secret directly from the config file.    
    -->
    <add key="ida:KeyVaultClientSecret" value="" />
    ```

    > [!IMPORTANT]  
    > Sensitive information such as application secrets should not be stored in configurations files. It was done so above because this is a sample application. With your production application it strongly recommended that you use certificate based authenticate. See [Authenticate with a certificate instead of a client secret](https://docs.microsoft.com/azure/key-vault/key-vault-use-from-web-application#authenticate-with-a-certificate-instead-of-a-client-secret) for more information.

8. When you run this sample project it will prompt you for authentication. After successfully authenticating an access token will be request from Azure AD. The information returned from Azure AD will include a refresh token that will be stored in the configured instance of Azure Key Vault.  

# [Java](#tab/java-partner-consent)

The [partner consent](https://github.com/Microsoft/Partner-Center-Java-Samples/tree/master/secure-app-model/keyvault) sample project demonstrates how to utilize a website developed using JSP to capture consent, request a refresh token, and secure store in Azure Key Vault. Perform the following to create the required prerequisites for this sample

1. Create an instance of Azure Key Vault using the Azure management portal or the following PowerShell commands. Before executing the command be sure to modify the parameter values accordingly. The vault name must be unique.

    ```azurepowershell-interactive
    Login-AzureRmAccount

    # Create a new resource group
    New-AzureRmResourceGroup -Name ContosoResourceGroup -Location EastUS

    New-AzureRmKeyVault -Name 'Contoso-Vault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East US'
    ```

    If you need help creating the instance of Azure Key Vault see [Quickstart: Set and retrieve a secret from Azure Key Vault using the Azure portal](https://docs.microsoft.com/azure/key-vault/quick-create-portal) or [Quickstart: Set and retrieve a secret from Azure Key Vault using PowerShell](https://docs.microsoft.com/azure/key-vault/quick-create-powershell) for step by step direction on how to create an instance of Azure Key Vault and set and retrieve a secret.

2. Create an Azure AD Application and a key using the Azure management portal or the following commands.

    ```azurepowershell-interactive
    Connect-AzureAD

    $SessionInfo = Get-AzureADCurrentSessionInfo

    $app = New-AzureADApplication -DisplayName 'My Vault Access App' -IdentifierUris 'https://$($SessionInfo.TenantDomain)/$((New-Guid).ToString())'
    $password = New-AzureADApplicationPasswordCredential -ObjectId $app.ObjectId

    Write-Host "ApplicationId       = $($app.AppId)"
    Write-Host "ApplicationSecret   = $($password.Value)"
    ```

    Be sure to document the application identifier and secret values because they will be used in the steps below.

3. Grant the newly create Azure AD application the read secrets permissions using the Azure management portal or the following commands.

    ```azurepowershell-interactive
    $app = Get-AzureADApplication -Filter {AppId -eq 'ENTER-APP-ID-HERE'}

    Set-AzureRmKeyVaultAccessPolicy –VaultName ContosoVault –ObjectId $app.ObjectId –PermissionsToSecrets get
    ```

4. Create an Azure AD application that is configured for Partner Center. Preform the following to complete this step

    - Browse to the [App management](https://partner.microsoft.com/pcv/apiintegration/appmanagement) feature of the Partner Center Dashboard
    - Click *Add new web app* to create a new Azure AD application.

    Be sure to document the *App ID*, *Account ID**, and *Key* values because they will be used in the steps below.

5. Clone the [Partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) repository using the following command

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-Java-Samples.git
    ```

6. Open the *PartnerConsent* project found in the `Partner-Center-Java-Samples\secure-app-model\keyvault` directory.
7. Populate the application settings found in the [web.xml](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/partnerconsent/src/main/webapp/WEB-INF/web.xml) file

    ```xml
    <filter>
        <filter-name>AuthenticationFilter</filter-name>
        <filter-class>com.microsoft.store.samples.partnerconsent.security.AuthenticationFilter</filter-class>
        <init-param>
            <param-name>client_id</param-name>
            <param-value></param-value>
        </init-param>
        <init-param>
            <param-name>client_secret</param-name>
            <param-value></param-value>
        </init-param>
        <init-param>
            <param-name>keyvault_base_url</param-name>
            <param-value></param-value>
        </init-param>
        <init-param>
            <param-name>keyvault_client_id</param-name>
            <param-value></param-value>
        </init-param>
        <init-param>
            <param-name>keyvault_client_secret</param-name>
            <param-value></param-value>
        </init-param>
        <init-param>
            <param-name>keyvault_certifcate_path</param-name>
            <param-value></param-value>
        </init-param>
    </filter>
    ```

    > [!IMPORTANT]  
    > Sensitive information such as application secrets should not be stored in configurations files. It was done so above because this is a sample application. With your production application it strongly recommended that you use certificate based authenticate. See [Key Vault Certificate authentication](https://github.com/Azure-Samples/key-vault-java-certificate-authentication) for more information.

8. When you run this sample project it will prompt you for authentication. After successfully authenticating an access token will be request from Azure AD. The information returned from Azure AD will include a refresh token that will be stored in the configured instance of Azure Key Vault.  

# [PowerShell](#tab/powershell-partner-consent)

Cloud Solution Provider partners can utilize the [Partner Center PowerShell](https://www.powershellgallery.com/packages/PartnerCenter) module to perform the partner consent process. The following demonstrates how consent can be provided and the refresh token can be obtained. Please note that you will need to manually store the refresh token in a secure repository such as Azure Key Vault.

```powershell
$credential = Get-Credential
$token = New-PartnerAccessToken -Consent -Credential $credential -Resource https://api.partnercenter.microsoft.com -ServicePrincipal
```

See [Partner Center PowerShell - Secure App Model](https://docs.microsoft.com/en-us/powershell/partnercenter/secure-app-model) for more information.

---

### Cloud Solution Provider Authentication

Cloud Solution Provider partners can use the refresh token obtained through the [partner consent](#partner-consent) process.

#### Samples

To help partners understand how to perform each operation required in this process the following samples have been developed. Please note that these are samples, so it is important when you implement the appropriate solution in your environment you develop a solution that is complaint with your code standard and security policies.

# [.NET](#tab/dotnet-csp-auth)

1. Perform the partner consent process. If you have not done this, the follow the step documented [here](#tab/dotnet-partner-consent).
2. Clone the [Partner-Center-DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) repository using Visual Studio or the following command

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-DotNet-Samples.git
    ```

3. Open the `CSPApplication` project found in the `Partner-Center-DotNet-Samples\secure-app-model\keyvault` directory.
4. Update the application settings found in the [App.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CSPApplication/App.config) file.

    ```xml
    <!-- AppID that represents CSP application -->
    <add key="ida:CSPApplicationId" value="" />
    <!-- 
        Please use certificate as your client secret and deploy the certificate to your environment.
        The following application secret is for sample application only. please do not use secret directly from the config file.    
    -->
    <add key="ida:CSPApplicationSecret" value="" />

    <!-- Endpoint address for the instance of Azure KeyVault -->
    <add key="KeyVaultEndpoint" value="" />

    <!-- AppID that is given access for keyvault to store the refresh tokens -->
    <add key="ida:KeyVaultClientId" value="" />

    <!-- 
        Please use certificate as your client secret and deploy the certificate to your environment.
        The following application secret is for sample application only. please do not use secret directly from the config file.    
    -->
    <add key="ida:KeyVaultClientSecret" value="" />
    ```

5. Set the appropriate values for the **PartnerId** and **CustomerId** variables found in the [Program.cs](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CSPApplication/Program.cs) file.

    ```csharp
    // The following properties indicate which partner and customer context the calls are going to be made.
    string PartnerId = "<Partner tenant id>";
    string CustomerId = "<Customer tenant id>";
    ```

6. When you run this sample project it will obtain the refresh token obtained during the partner consent process. Then it will request an access token on the partner's behalf to interact with the Partner Center SDK. Finally, it will request an access token on behalf of the specified customer to interact with Microsoft Graph in the context of the customer.

# [Java](#tab/java-csp-auth)

1. Perform the partner consent process. If you have not done this, the follow the step documented [here](#tab/java-partner-consent).
2. Clone the [Partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) repository using Visual Studio or the following command

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-Java-Samples.git
    ```

3. Open the `cspsample` project found in the `Partner-Center-Java-Samples\secure-app-model\keyvault` directory.
4. Update the application settings found in the [application.properties](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cspsample/src/main/resources/application.properties) file.

    ```
    azuread.authority=https://login.microsoftonline.com
    keyvault.baseurl=
    keyvault.clientId=
    keyvault.clientSecret=
    partnercenter.accountId=
    partnercenter.clientId=
    partnercenter.clientSecret=
    ```

5. By default when  you run this sample project it will obtain the refresh token obtained during the partner consent process. Then it will request an access token on the partner's behalf to interact with the Partner Center SDK.
6. Optional - un-comment the *RunAzureTask* and *RunGraphTask* function calls if you want to see how to interact with with Azure Resource Manager and Microsoft Graph on behalf of the customer.

# [PowerShell](#tab/powershell-csp-auth)

1. Perform the partner consent process. If you have not done this, the follow the step documented [here](#tab/powershell-partner-consent).
2. Obtain the refresh token value from the secure repository.
3. Run the following commands to request a new access token and connect to Partner Center

    ```powershell
    $refreshToken = 'Enter the refresh token value here'

    $credential = Get-Credential
    $pcToken = New-PartnerAccessToken -RefreshToken $refreshToken -Resource https://api.partnercenter.microsoft.com -Credential $credential -ServicePrincipal

    Connect-PartnerCenter -AccessToken $pcToken.AccessToken -AccessTokenExpiresOn $pcToken.ExpiresOn -ApplicationId $appId
    ```

    See [Partner Center PowerShell - Secure App Model](https://docs.microsoft.com/en-us/powershell/partnercenter/secure-app-model) for more information.

---

### Control Panel Provider Authentication

Intentionally left blank

## Frequently Asked Questions

### Can the trusted location conditional access policy be used to bypass the requirement for multi-factor authentication?

### Due to the regional authorization model I have more than one Azure AD tenant. Do I need purchase multiple licenses for the same employee?

Each identity that will be used to access the Partner Center API or Partner Center Dashboard will require multi-factor authentication. If you are planning to utilize Microsoft Azure multi-factor authentication then you will need to purchase the appropriate license for each identity. The result of this could mean you will be purchasing multiple licenses for the same employee since they might have multiple identities within Azure AD.

No, this will not work because of how the requirement is being enforced. Each time you connecting to Partner Center you must be authenticated using multi-factor authentication.

### How will the requirement for multi-factor authentication be enforced?

This requirement will be enforced by ensuring the
<http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod> claim is set to <https://schemas.microsoft.com/claims/multipleauthn>. If this claim contains a different value then authentication will be denied.

### Will indirect reseller require multi-factor authentication?

Yes, partners with an enrollment into the Cloud Solution Provider program, this include direct, indirect providers, and indirect resellers will need to implement the appropriate multi-factor authentication solution.