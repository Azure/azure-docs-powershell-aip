---
external help file: AIP.dll-Help.xml
Module Name: AzureInformationProtection
online version: https://go.microsoft.com/fwlink/?linkid=2004271
schema: 2.0.0
---

# Update-AIPScanner

## SYNOPSIS
Updates the database schema for the Azure Information Protection scanner.

## SYNTAX

```
Update-AIPScanner [-Cluster | -Profile <String>] [-Force] [<CommonParameters>]
```

## DESCRIPTION
The **Update-AIPScanner** cmdlet updates the database schema for the Azure Information Protection scanner and if required, the scanner service account is also granted delete permissions for the scanner database. 

Run this cmdlet after upgrading your Azure Information Protection client.
   
For more information, see [Installing the Azure Information Protection scanner](/azure/information-protection/rms-client/clientv2-admin-guide#installing-the-azure-information-protection-scanner.md) from the admin guide for the unified labeling client.
    
Run this cmdlet with an account that has the database-level role of **db_owner** for the configuration database that the scanner is using, named **AIPScannerUL_\<cluster_name>**.


## EXAMPLES

### Example 1: Update the scanner after the Azure Information Protection client has been upgraded, and set a scanner cluster  name
```
PS C:\> Update-AIPScanner –cluster USWEST
```

This command updates the database schema for the Azure Information Protection scanner, and sets the cluster name to **USWEST** rather than use the default name of the computer. 

You are prompted to continue and if you confirm, the scanner then gets is configuration from the **USWEST** scanner cluster that you configure by using the Azure portal.

The Azure Information Protection scanner is updated successfully, the scanner database is renamed to **AIPScanner_USWEST**, and the scanner now gets its configuration from the Azure Information Protection service. 

For reference purposes, a backup of your old configuration is stored in **%localappdata%\Microsoft\MSIP\ScannerConfiguration.bak**. 


## PARAMETERS


### -Cluster
Specifies the configured name of the scanner's database, used to identify the scanner you want to update.

Use the following syntax: **AIPScannerUL_<cluster_name>**. 

Using either this parameter or the **Profile** parameter is mandatory. Starting in version 2.7.0.0 of the unified labeling client, we recommend using this parameter instead of the **Profile** parameter.


```yaml 
Type: String 
Parameter Sets: (All) 
Position: Named 
Default value: None 
Accept pipeline input: False 
Accept wildcard characters: False 
```

### -Force
Forces the command to run without asking for user confirmation.

When used, the command first verifies that all nodes under the same cluster are offline. If any nodes are found to be online, a warning is displayed with the node details.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Profile
Specifies the configured name of the scanner's database, used to identify the scanner you want to update.

Using either this parameter or the **Cluster** parameter is mandatory. Starting in version 2.7.0.0 of the unified labeling client, we recommend using the **Cluster** parameter instead of the this parameter.

The database name for the scanner is **AIPScannerUL_\<profile_name>**. 


```yaml 
Type: String 
Parameter Sets: (All) 
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

### None

## OUTPUTS

### System.Object

## NOTES

## RELATED LINKS

[Get-AIPScannerConfiguration](./Get-AIPScannerConfiguration.md)

[Get-AIPScannerStatus](./Get-AIPScannerStatus.md)

[Install-AIPScanner](./Install-AIPScanner.md)

[Set-AIPScanner](./Set-AIPScanner.md)

[Set-AIPScannerConfiguration](./Set-AIPScannerConfiguration.md)

[Start-AIPScan](./Start-AIPScan.md)

[Uninstall-AIPScanner](./Uninstall-AIPScanner.md)