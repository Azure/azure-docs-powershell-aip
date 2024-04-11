---
external help file: AipService.dll-Help.xml
Module Name: AIPService
ms.assetid: 857D8EFC-9D6E-4756-A9A2-B90FF8E02A1F
online version: https://go.microsoft.com/fwlink/?linkid=2045019
schema: 2.0.0
---

# Connect-AipService

## SYNOPSIS
Connects to Azure Information Protection.

## SYNTAX

### Credential (Default)
```
Connect-AipService [-Credential <PSCredential>] [-TenantId <Guid>] [<CommonParameters>]
```

### AccessToken
```
Connect-AipService [-AccessToken <String>] [-TenantId <Guid>] [<CommonParameters>]
```

### Environment
```
Connect-AipService [-EnvironmentName <AzureRmEnvironment>] [<CommonParameters>]
```

## DESCRIPTION
The **Connect-AipService** cmdlet connects you to Azure Information Protection so that you can then run administrative commands for the protection service for your tenant. This cmdlet can also be used by a partner company that manages your tenant.

You must run this cmdlet before you can run the other cmdlets in this module.

To connect to Azure Information Protection, use an account that is one of the following:
- A global admin for your Office 365 tenant.
- A global administrator for your Azure AD tenant. However, this account cannot be a Microsoft account (MSA) or from another Azure tenant.
- A user account from your tenant that has been granted administrative rights to Azure Information Protection by using the [Add-AipServiceRoleBasedAdministrator](./Add-AipServiceRoleBasedAdministrator.md) cmdlet. 
- An Azure AD admin role of Azure Information Protection administrator, Compliance administrator, or Compliance data administrator.

> [!TIP]
> If you are not prompted for your credentials, and you see an error message such as **Cannot use this feature without credentials**, verify that Internet Explorer is configured to use Windows integrated authentication. 
>
> If this setting is not enabled, enable it, restart Internet Explorer, and then retry authentication to the Information Protection service.
> 
## EXAMPLES

### Example 1: Connect to Azure Information Protection and be prompted for your user name and other credentials
```
PS C:\> Connect-AipService
```

This command connects to the protection service from Azure Information Protection. This is the simplest way to connect to the service, by running the cmdlet with no parameters.

You are prompted for your user name and password. If your account is configured to use multi-factor authentication, you are then prompted for your alternative method of authentication, and then connected to the service.

If your account is configured to use multi-factor authentication, you must use this method to connect to Azure Information Protection.

### Example 2: Connect to Azure Information Protection with stored credentials
```
PS C:\>$AdminCredentials = Get-Credential "Admin@aadrm.contoso.com"
PS C:\> Connect-AipService -Credential $AdminCredentials
```

The first command creates a **PSCredential** object and stores your specified user name and password in the **$AdminCredentials** variable. When you run this command, you are prompted for the password for the user name that you specified.

The second command connects to Azure Information Protection by using the credentials stored in **$AdminCredentials**. If you disconnect from the service and reconnect while the variable is still in use, simply rerun the second command.

### Example 3: Connect to Azure Information Protection with a token
```
PS C:\ > Add-Type -Path "C:\Program Files\WindowsPowerShell\Modules\AIPService\1.0.0.1\Microsoft.IdentityModel.Clients.ActiveDirectory.dll"
PS C:\ > $clientId='90f610bf-206d-4950-b61d-37fa6fd1b224';
PS C:\ > $resourceId = 'https://api.aadrm.com/';
PS C:\ > $userName='admin@contoso.com';
PS C:\ > $password='Passw0rd!';
PS C:\ > $authority = "https://login.microsoftonline.com/common";
PS C:\ > $authContext = New-Object Microsoft.IdentityModel.Clients.ActiveDirectory.AuthenticationContext($authority);
PS C:\ > $userCreds = New-Object Microsoft.IdentityModel.Clients.ActiveDirectory.UserPasswordCredential($userName, $password);
PS C:\ > $authResult = [Microsoft.IdentityModel.Clients.ActiveDirectory.AuthenticationContextIntegratedAuthExtensions]::AcquireTokenAsync($authContext, $resourceId, $clientId, $userCreds).Result;
PS C:\ > Import-Module AIPService
PS C:\> Connect-AipService -AccessToken $authResult.AccessToken

```

This example shows how you could connect to Azure Information Protection by using the *AccessToken* parameter, which lets you authenticate without a prompt. This connection method requires you to specify the client ID *90f610bf-206d-4950-b61d-37fa6fd1b224* and the resource ID `*https://api.aadrm.com/*`. After the connection is open, you can then run the administrative commands from this module that you need.

After you confirm that these commands result in successfully connecting to Azure Information Protection, you could run them non-interactively, for example, from a script.

Note that for illustration purposes, this example uses the user name of **admin@contoso.com** with the password of **Passw0rd!** In a production environment when you use this connection method non-interactively, use additional methods to secure the password so that it is not stored in clear text. For example, use the **ConvertTo-SecureString** command or use Key Vault to store the password as a secret.

### Example 4: Connect to Azure Information Protection with client certificate via Service Principal Authentication
```
PS C:\ > $Thumbprint = 'XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX'
PS C:\ > $TenantId = 'yyyyyyyy-yyyy-yyyy-yyyy-yyyyyyy'
PS C:\ > $ApplicationId = '00000000-0000-0000-0000-00000000'
PS C:\> Connect-AipService -CertificateThumbprint $Thumbprint -ApplicationId $ApplicationId -TenantId $TenantId -ServicePrincipal

```

This example connects to an Azure account using certificate-based service principal authentication. The service principal used for authentication must be created with the specified certificate. 

Prerequisites for this example:

- You must update the AIPService PowerShell Module to version 1.0.05 or later.
- To enable Service Principal authentication, you must add read API permissions (**Application.Read.All**) to the service principal.

For more information, see [Required API permissions - Microsoft Information Protection SDK](/information-protection/develop/concept-api-permissions) and [Use Azure PowerShell to create a service principal with a certificate](/azure/active-directory/develop/howto-authenticate-service-principal-powershell).

### Example 5: Connect to Azure Information Protection with client secret via Service Principal Authentication
```
PS C:\ > $TenantId = 'yyyyyyyy-yyyy-yyyy-yyyy-yyyyyyy'
PS C:\ > $ApplicationId = '00000000-0000-0000-0000-00000000'
PS C:\ > $Credential = New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $ApplicationId, $SecuredPassword
PS C:\ > Connect-AipService -Credential $Credential -TenantId $TenantId -ServicePrincipal

```

In this example:

- The first command prompts for service principal credentials and stores them in the `$Credential` variable. When promoted, enter your application ID for the username value and the service principal secret as the password.
- The second command connects to the specified Azure tenant using the service principal credentials stored in the `$Credential` variable. The `ServicePrincipal` switch parameter indicates that the account authenticates as a service principal.

To enable Service Principal authentication, you must add read API permissions (**Application.Read.All**) to the service principal. For more information, see [Required API permissions - Microsoft Information Protection SDK](/information-protection/develop/concept-api-permissions).

## PARAMETERS

### -AccessToken
Use this parameter to connect to Azure Information Protection by using a token that you acquire from Azure Active Directory, using the client ID **90f610bf-206d-4950-b61d-37fa6fd1b224** and the resource ID **https://api.aadrm.com/**. This connection method lets you sign in to Azure Information Protection non-interactively.

To get the access token, make sure that the account that you use from your tenant is not using multi-factor authentication (MFA). See Example 3 for how you might do this.

You cannot use this parameter with the *Credential* parameter.

```yaml
Type: String
Parameter Sets: AccessToken
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -ApplicationID
Specifies the service principal's application ID.

```yaml
Type: String

Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### CertificateThumbprint

Specifies the certificate thumbprint of a digital public key X.509 certificate for a service principal that has permissions to perform the given action.

```yaml
Type: String

Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Credential
Specifies a **PSCredential** object. To obtain a **PSCredential** object, use the [Get-Credential](/powershell/module/Microsoft.PowerShell.Security/Get-Credential?viewFallbackFrom=powershell-4.0) cmdlet. For more information, type `Get-Help Get-Cmdlet`.

The cmdlet prompts you for a password.

You cannot use this parameter with the *AccessToken* parameter and do not use it if your account is configured to use multi-factor authentication (MFA).

```yaml
Type: PSCredential
Parameter Sets: Credential
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -EnvironmentName
Specifies the Azure instance for sovereign clouds. Valid values are:

- **AzureCloud:** Commercial offering of Azure
- **AzureChinaCloud:** Azure Operated by 21Vianet
- **AzureUSGovernment:** Azure Government 

For more information about using Azure Information Protection with Azure Government, see [Azure Information Protection Premium Government Service Description](/enterprise-mobility-security/solutions/ems-aip-premium-govt-service-description).

```yaml
Type: AzureRmEnvironment
Parameter Sets: Environment
Aliases:
Accepted values: AzureCloud, AzureChinaCloud, AzureUSGovernment

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -ServicePrincipal
Indicates that the cmdlet specifies service principal authentication.

The service principal must be created with the specified secret.

```yaml
Type: SwitchParameter

Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```


### -TenantId
Specifies the tenant GUID. The cmdlet connects to Azure Information Protection for the tenant that you specify by GUID.

If you do not specify this parameter, the cmdlet connects to the tenant that your account belongs to.

```yaml
Type: Guid
Parameter Sets: Credential, AccessToken
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. 

For more information, see [about_CommonParameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters).

## INPUTS

## OUTPUTS

## NOTES

## RELATED LINKS

[Get-Credential](/powershell/module/Microsoft.PowerShell.Security/Get-Credential?viewFallbackFrom=powershell-4.0)

[Disconnect-AipService](./Disconnect-AipService.md)
