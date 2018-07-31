---
external help file: AIP.dll-Help.xml
Module Name: AzureInformationProtection
online version: https://go.microsoft.com/fwlink/?linkid=2004364
schema: 2.0.0
---

# Start-AIPScan

## SYNOPSIS
Instructs the Azure Information Protection scanner to start a one time scan cycle. 

## SYNTAX

```
Start-AIPScan [-Reset] [<CommonParameters>]
```

## DESCRIPTION
The Start-AIPScan instructs the Azure Information Protection scanner to immediately start a one time scan cycle. The scanner service must be started already and the scanner schedule must be configured for a manual schedule. You configure the schedule by using the *Schedule* parameter with [Set-AIPScannerConfiguration](./Set-AIPScannerConfiguration.md).

By default, all files are scanned the first time the scanner runs and then, unless the Azure Information Protection policy is changed, only new or changed files are scanned. However, you can change this behavior when you use the *-Reset* parameter with this cmdlet, which forces the scanner to scan all files.
  
If the scanner schedule is set to Always, this cmdlet is ignored.

Note: This cmdlet requires the preview version of the scanner that is included with the current preview version of the Azure Information Protection client.

## EXAMPLES

### Example 1: Initiate immediate one time scan for new and changed files
```powershell
PS C:\> Start-AIPScan
```

Because this is not the first time that the scanner has run and the Azure Information Protection policy has not changed since the last scanning cycle, the scanner initiates an incremental scan for all new or changed files since the last scanning cycle.

### Example 2: Initiate immediate one time scan for all files
```powershell
PS C:\> Start-AIPScan -Reset
```

The scanner initiates a full scan of all the files, even if they have been scanned before and the Azure Information Protection policy has not changed.

## PARAMETERS

### -Reset
Resets the scanner cache so that the scanner initiates a full scan of all the files, even if they have been scanned before and the Azure Information Protection policy has not changed.

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

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.
For more information, see [about_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

### None


## OUTPUTS

### System.Object

## NOTES

## RELATED LINKS

[Add-AIPScannerRepository](./Add-AIPScannerRepository.md)

[Add-AIPScannerScannedFileTypes](Add-AIPScannerScannedFileTypes.md)

[Get-AIPScannerConfiguration](./Get-AIPScannerConfiguration.md)

[Get-AIPScannerRepository](./Get-AIPScannerRepository.md)

[Get-AIPScannerStatus](./Get-AIPScannerStatus.md)

[Install-AIPScanner](./Install-AIPScanner.md)

[Remove-AIPScannerRepository](./Remove-AIPScannerRepository.md)

[Remove-AIPScannerScannedFileTypes](./Remove-AIPScannerScannedFileTypes )

[Set-AIPScanner](./Set-AIPScanner.md)

[Set-AIPScannerConfiguration](./Set-AIPScannerConfiguration)

[Set-AIPScannerRepository](./Set-AIPScannerRepository.md)

[Set-AIPScannerScannedFileTypes](./Set-AIPScannerRepository.md)

[Uninstall-AIPScanner](./Uninstall-AIPScanner.md)

[Update-AIPScanner](./Update-AIPScanner)