---
external help file: AIP.dll-Help.xml
Module Name: AzureInformationProtection
online version: https://go.microsoft.com/fwlink/?linkid=858205
schema: 2.0.0
---

# Set-AIPScannerConfiguration

## SYNOPSIS
**Relevant for:** AIP unified labeling and classic clients

Sets optional configuration for the Azure Information Protection scanner.

## SYNTAX

```
Set-AIPScannerConfiguration [-ReportLevel <ReportLevel>] [-OnlineConfiguration <OnlineConfiguration>] [<CommonParameters>]
```

## DESCRIPTION
The **Set-AIPScannerConfiguration** cmdlet sets local configuration settings for the Azure Information Protection scanner. 

You configure most of the scanner configuration settings in the Azure portal, but must use this cmdlet if you need to import configuration settings from a file because the scanner cannot support online configuration, or if you need to change the report level for the locally created reports.

Any changes will be used the next time the scanner runs. If you need the changes to take effect immediately, restart the Azure Information Protection Scanner service on the Windows server computer.

> [!NOTE]
> To provide a unified and streamlined customer experience, the **Azure Information Protection classic client** and **Label Management** in the Azure Portal are being **deprecated** as of **March 31, 2021**. 
> 
> This time-frame allows all current Azure Information Protection customers to transition to our unified labeling solution using the Microsoft Information Protection Unified Labeling platform. Learn more in the official [deprecation notice](https://aka.ms/aipclassicsunset).


## EXAMPLES

### Example 1: Set the Azure Information Protection scanner to use online configuration

```
PS C:\> Set-AIPScannerConfiguration -OnlineConfiguration On

Configuration was set successfully.
```

This command sets the scanner to get its configuration directly from the Azure Information Protection service.


## PARAMETERS

### -ReportLevel
Define the level of logging for the scanner reports. When the scanner is first installed, by default, only files that are successfully labeled by the scanner are included in the log file.

Log files are stored in the **%localappdata%\Microsoft\MSIP\Scanner\Reports** folder. A summary report **(.txt)** includes the time taken to scan, the number of scanned files, and statistics of how many files were classified and protected. Detailed reports **(.csv)** has details for each file. The folder stores up to 60 reports for each scanning cycle and all but the latest report is compressed to help minimize the required disk space.

|Log level |Description  |
|---------|---------|
|**Debug**     | Logs every file that was discovered and the resulting action. This level of logging is useful for troubleshooting but slows down the Azure Information Protection scanner. This category includes files that don't meet any of the conditions and files that are skipped because of an unsupported file type. </br></br>For example, trying to label a file for classification-only when the file type doesn't support this action, and trying to label files that are automatically excluded. </br></br>For more information, see the following information from the admin guides: </br>- [Classic client](/information-protection/rms-client/client-admin-guide-file-types)   </br>- [Unified labeling client](/information-protection/rms-client/clientv2-admin-guide-file-types)    |
|**Info**     |  Logs only the files that were successfully labeled by the scanner, or would be labeled when the scanner is in discovery mode.       |
|**Error**     |  Logs only the files that the scanner attempted to label but could not. For example, a file was in use, or the scanner service did not have write access to the file.       |
|**Off**     |  Disables reporting, which results in the best performance for the scanner.       |

The local Windows **Applications and Services** event log, **Azure Information Protection** contains additional logging information. The events include the start and end times for each scanning cycle, when a scanned file has a label applied, and when protection is applied or removed. For more information, see [Event log IDs and descriptions for the scanner](/information-protection/deploy-aip-scanner#event-log-ids-and-descriptions-for-the-scanner).


```yaml
Type: ReportLevel
Parameter Sets: (All)
Aliases:
Accepted values: Off, Debug, Info, Error

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -OnlineConfiguration 
Specifies whether the scanner gets its configuration settings directly from the Azure Information Protection service (the default), or uses an offline configuration file.

- **On:** The default setting. The scanner gets its configuration settings directly from the Azure Information Protection service.

- **Off:** Supported by the AIP classic client only. The scanner is prevented from getting its configuration settings directly from the Azure Information Protection service. Instead, the scanner is configured by settings that you import from a file. 

If the scanner cannot support online configuration, you must still configure the scanner in the Azure portal. Then, export the scanner configuration from the portal to a .json file and import this file by using the [Import-AIPScannerConfiguration](./Import-AIPScannerConfiguration.md) cmdlet.

```yaml
Type: OnlineConfiguration
Parameter Sets: (All)
Aliases:
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

[Start-AIPScan](./Start-AIPScan.md)

[Uninstall-AIPScanner](./Uninstall-AIPScanner.md)

[Update-AIPScanner](./Update-AIPScanner.md)