---
external help file: AIP.dll-Help.xml
Module Name: AzureInformationProtection
online version: https://go.microsoft.com/fwlink/?linkid=866449
schema: 2.0.0
---

# Set-AIPScannerRepository

## SYNOPSIS
Updates a profile of configuration settings for a data repository to be scanned by the Azure Information Protection scanner. 

## SYNTAX

```
Set-AIPScannerRepository [-Path] <String> [-OverrideLabel <OverrideLabel>]
 [-PreserveFileDetails <PreserveFileDetails>] [-DefaultOwner <String>] [-SetDefaultLabel <DefaultLabel>]
 [-DefaultLabelId <Guid>] [<CommonParameters>]
```

## DESCRIPTION
The Set-AIPScannerRepository cmdlet updates a profile of configuration settings for a data repository that you have specified to be scanned by the Azure Information Protection scanner.

For example, for each data repository that you specified by running [Add-AIPScannerRepository](./Add-AIPScannerRepository.md), you can change the default label for unlabeled files, and whether to override an existing label.

## EXAMPLES

### Example 1: For unlabeled files in a local folder, change the default label that is specified in the Azure Information Protection policy
```
PS C:\> Set-AIPScannerRepository -Path D:\Data\Finance -SetDefaultLabel UsePolicyDefault

The settings were updated successfully.
```

This command updates the profile for the D:\Data\Finance repository, which specifies that unlabeled files will be labeled with the default label from the Azure Information Protection policy.

### Example 2: For files in a network-attached storage (NAS) file share repository, change the default label to a specific label, change the override behavior to always relabel files, and set the Owner custom property and Rights Management owner
```
PS C:\> Set-AIPScannerRepository -Path \\NAS\HR -SetDefaultLabel On -DefaultLabelId -SetDefaultLabel f018e9e7-0cfc-4c69-b27a-ac3cb7df43cc -OverrideLabel On -DefaultOwner "admin@contoso.com"

The settings were updated successfully.
```

This command sets the following configuration for the \\NAS\HR data repository:

- For unlabeled files, apply the label that has an ID of f018e9e7-0cfc-4c69-b27a-ac3cb7df43cc.

- For files that are already labeled, override that label with the new label.

- Set the Owner custom property and Rights Management owner to the administrator's account.

### Example 3: Stop applying a default label to unlabeled files in a SharePoint library
```
PS C:\> Set-AIPScannerRepository -Path "http://sp2013/Shared Documents" -SetDefaultLabel Off

The settings were updated successfully.
```

This command updates the default label behavior so that unlabeled files in the specified data repository remain unlabeled.

## PARAMETERS

### -Path
Specifies a local path, network path, or SharePoint Server URL for the data repository that you want to scan. Wildcards are not supported.

For SharePoint paths: SharePoint Server 2016 and SharePoint Server 2013 are supported.

Examples include C:\Folder\, C:\Folder\Filename, \\\Server\Folder, http://sharepoint.contoso.com/Shared%20Documents/Folder. Paths can include spaces when you enclose the path value with quotes.

```yaml
Type: String
Parameter Sets: (All)
Aliases: FullName

Required: True
Position: 0
Default value: None
Accept pipeline input: True (ByPropertyName, ByValue)
Accept wildcard characters: False
```

### -DefaultLabelId
Specifies the label ID to use as the default label for this data repository. This default label is applied to unlabeled files if no conditions are matched and the *SetDefaultLabel* parameter is set to On.  

This parameter is ignored if *SetDefaultLabel* is set to Off. 

When a label has sublabels, always specify the ID of just a sublabel and not the parent label.

The label ID value is displayed in the Azure portal, on the Label blade, when you view or configure the Azure Information Protection policy. For files that have labels applied, you can also run the Get-AIPFileStatus cmdlet to identify the label ID (MainLabelId or SubLabelId).

```yaml
Type: Guid
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -DefaultOwner
Specifies the email address for the Owner custom property when a file is classified, and for the Rights Management owner when a file is protected. For more information about the Rights Management owner, see [Rights Management issuer and Rights Management owner](https://docs.microsoft.com/information-protection/deploy-use/configure-usage-rights#rights-management-issuer-and-rights-management-owner).

If you do not specify this parameter, default values are used for the Owner custom property and the Rights Management owner:

- For files on SharePoint Server, the SharePoint author is used.

- For files on SharePoint Server that do not have the author property set and for files that are stored on file shares or local folders, the scanner's account is
used.

To remove the currently set Owner custom property and Rights Management owner, specify "".

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

### -OverrideLabel
Specify whether to apply a different label to a file that's already labeled. By default, the scanner doesn't relabel the files, unless the new label has higher sensitivity than current label, and the initial label was not manually applied by an end user.

If set to On, the scanner replaces an existing label when the configured conditions apply.

```yaml
Type: OverrideLabel
Parameter Sets: (All)
Aliases:
Accepted values: Off, On

Required: False
Position: Named
Default value: Off
Accept pipeline input: False
Accept wildcard characters: False
```

### -PreserveFileDetails
Specify this parameter to leave the date unchanged for documents that you label.

For local or network files, the Last Modified date remains unchanged.

For SharePoint files, the Modified date and Modified By date remains unchanged.

```yaml
Type: PreserveFileDetails
Parameter Sets: (All)
Aliases:
Accepted values: Off, On

Required: False
Position: Named
Default value: On
Accept pipeline input: False
Accept wildcard characters: False
```

### -SetDefaultLabel
Specifies whether the scanner sets a default label on unlabeled files for this data repository. You can apply the default label from the Azure Information Protection policy, or another label.

- UsePolicyDefault: For unlabeled files, apply the default label that is specified in the Azure Information Protection policy.

- Off: For unlabeled files, do not apply a default label.

- On: For unlabeled files, apply the label that is specified by its label ID.

```yaml
Type: DefaultLabel
Parameter Sets: (All)
Aliases:
Accepted values: UsePolicyDefault, Off, On

Required: False
Position: Named
Default value: UsePolicyDefault
Accept pipeline input: False
Accept wildcard characters: False
```

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

### System.String

## OUTPUTS

### System.Object

## NOTES

## RELATED LINKS

[Add-AIPScannerRepository](./Add-AIPScannerRepository.md)

[Get-AIPScannerConfiguration](./Get-AIPScannerConfiguration.md)

[Install-AIPScanner](./Install-AIPScanner.md)

[Remove-AIPScannerRepository](./Remove-AIPScannerRepository.md)

[Set-AIPScanner](./Set-AIPScanner.md)

[Set-AIPScannerConfiguration](./Set-AIPScannerConfiguration.md)

[Set-AIPScannerRepository](./Set-AIPScannerRepository.md)

[Uninstall-AIPScanner](./Uninstall-AIPScanner.md)
