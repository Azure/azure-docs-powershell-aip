---
external help file: AIP.dll-Help.xml
online version: https://go.microsoft.com/fwlink/?linkid=858203
schema: 2.0.0
---

# Install-AIPScanner

## SYNOPSIS
Installs the Azure Information Protection scanner.

## SYNTAX

```
Install-AIPScanner [-ServiceUserCredentials] <PSCredential> [-SqlServerInstance] <String>
```

## DESCRIPTION
The Install-AIPScanner cmdlet installs and configures the Azure Information Protection Scanner service on a computer running Windows Server 2016 or Windows Server 2012 R2. The Azure Information Protection scanner uses this service to scan files on data stores that use the Common Internet File System (CIFS) protocol, and on SharePoint Server 2016 and SharePoint Server 2013. By using the conditions that you configure for automatic classification in the Azure Information Protection policy, files that this scanner discovers can then be labeled. Labels apply classification, and optionally, apply protection or remove protection.

For more information about how to configure the Azure Information Protection policy, see [Configuring the Azure Information Protection policy](https://docs.microsoft.com/information-protection/deploy-use/configure-policy).

You must run this cmdlet before you run any other cmdlet for the Azure Information Protection scanner.

The command creates a Windows service named Azure Information Protection Scanner. It also creates and configures a database on SQL Server to store configuration and operational information for the scanner. The service that you specify to run the scanner is automatically granted the required rights to read and write to the database that is created.

To run this command, you must have local administrator rights for the Windows Server computer, and Sysadmin rights on the instance of SQL Server that you will use for the scanner.

Note: If you later need to change the account and database that you specified when you ran this cmdlet, you can do so by using the [Set-AIPScanner](./Set-AIPScanner.md) cmdlet.

After you have run this command, specify the data repositories to scan by using the [Add-AIPScannerRepository](./Add-AIPScannerRepository.md) cmdlet. Then check whether you need to change any of the default configuration options that can be set by using the [Set-AIPScannerConfiguration](./Set-AIPScannerConfiguration.md) cmdlet. Before you run the scanner, you must run the [Set-AIPAuthentication](./Set-AIPAuthentication.md) cmdlet one time to sign in to Azure AD for authentication and authorization. 

For step-by-step instructions to install, configure, and use the scanner, see [Deploying the Azure Information Protection scanner to automatically classify and protect files](https://docs.microsoft.com/information-protection/deploy-use/deploy-aip-scanner).

Note: This cmdlet is in preview and requires the current preview version of the Azure Information Protection client.

## EXAMPLES

### Example 1:Install the Azure Information Protection Scanner service by using a SQL Server instance
```
PS C:\> Install-AIPScanner -SqlServerInstance SQLSERVER1\AIPSCANNER

```

This command installs the Azure Information Protection Scanner service by using a SQL Server instance named AIPSCANNER, which runs on the server named SQLSERVER1. You are prompted to provide the Active Directory account details for the scanner service account. It then displays the progress, where the install log is located, and the creation of the new Windows Application event log named Azure Information Protection Scanner. 

At the end of the output, you see **The transacted install has completed**.

### Example 2: Install the Azure Information Protection Scanner service by using the SQL Server default instance
```
PS C:\> Install-AIPScanner -SqlServerInstance SQLSERVER1

```

This command installs the Azure Information Protection Scanner service by using the SQL Server default instance that runs on the server named SQLSERVER1. As with the previous example, you are prompted for credentials, and then the command displays the progress, where the install log is located, and the creation of the new Windows Application event log.


### Example 3: Install the Azure Information Protection Scanner service by using SQL Server Express 
```
PS C:\> Install-AIPScanner -SqlServerInstance SQLSERVER1\SQLEXPRESS

```

This command installs the Azure Information Protection Scanner service by using SQL Server Express that runs on the server named SQLSERVER1. As with the previous examples, you are prompted for credentials, and then the command displays the progress, where the install log is located, and the creation of the new Windows Application event log.

## PARAMETERS

### -ServiceUserCredentials
Specifies a **PSCredential** object for the service account to run the Azure Information Protection Scanner service. For the user name, use the following format: Domain\Username. You are prompted for a password. 

To obtain a PSCredential object, use the [Get-Credential](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.security/get-credential) cmdlet. For more information, type `Get-Help Get-Cmdlet`. 
If you do not specify this parameter, you are prompted for the user name and password.

This account must be an Active Directory account. For additional requirements, see [Prerequisites for the Azure Information Protection scanner](https://docs.microsoft.com/information-protection/deploy-use/deploy-aip-scanner#prerequisites-for-the-azure-information-protection-scanner).

```yaml
Type: PSCredential
Parameter Sets: (All)
Aliases: 

Required: True
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -SqlServerInstance
Specifies the SQL Server instance on which to create a database for the Azure Information Protection scanner. 

For information about the SQL Server requirements, see [Prerequisites for the Azure Information Protection scanner](https://docs.microsoft.com/information-protection/deploy-use/deploy-aip-scanner#prerequisites-for-the-azure-information-protection-scanner).

For the default instance, specify the server name. For example: SQLSERVER1. 

For a named instance, specify the server name and instance name. For example: SQLSERVER1\AIPSCANNER. 

For SQL Server Express, specify the server name and SQLEXPRESS. For example: SQLSERVER1\SQLEXPRESS.


```yaml
Type: String
Parameter Sets: (All)
Aliases: 

Required: True
Position: 2
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

## INPUTS

### None


## OUTPUTS

### System.Object

## NOTES

## RELATED LINKS

[Add-AIPScannerRepository](./Add-AIPScannerRepository.md)

[Get-AIPScannerConfiguration](./Get-AIPScannerConfiguration.md)

[Get-AIPScannerRepository](./Get-AIPScannerRepository.md)

[Remove-AIPScannerRepository](./Remove-AIPScannerRepository.md)

[Set-AIPScanner](./Set-AIPScanner.md)

[Set-AIPScannerConfiguration](./Set-AIPScannerConfiguration.md)

[Uninstall-AIPScanner](./Uninstall-AIPScanner.md)