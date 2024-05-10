---
external help file: AIP.dll-Help.xml
Module Name: PurviewInformationProtection
online version: https://go.microsoft.com/fwlink/?linkid=2258855
ms.topic: reference
schema: 1.0.0
---

# Start-Scan

## SYNOPSIS

Instructs the Microsoft Purview Information Protection scanner to start a one-time scan cycle. 

## SYNTAX

```powershell
Start-Scan [-Reset] [-Force] [<CommonParameters>]
```

## DESCRIPTION
The **Start-Scan** cmdlet instructs the Microsoft Purview Information Protection scanner to immediately start a one-time scan cycle. The scanner service must be started already and the scanner schedule must be configured for a manual schedule. 

To configure the schedule, use the [Microsoft Purview portal or the Microsoft Purview compliance portal to configure the scanner](/azure/information-protection/deploy-aip-scanner).

By default, all files are scanned the first time the scanner runs and then, unless the information protection policy is changed, only new or changed files are scanned. However, you can change this behavior when you use the *-Reset* parameter with this cmdlet, which forces the scanner to scan all files.
  
> [!NOTE]
> If the scanner schedule is set to **Always**, this cmdlet is ignored.
>
## EXAMPLES

### Example 1: Initiate immediate one-time scan for new and changed files
```powershell
PS C:\> Start-Scan
```

Because the scanner ran before, and the information protection scanner policy wasn't changed since the last scanning cycle, the scanner initiates an incremental scan for all new or changed files since the last scanning cycle.

### Example 2: Initiate immediate one time scan for all files
```powershell
PS C:\> Start-Scan -Reset
```

The scanner initiates a full scan of all the files, even if they were scanned before and the information protection scanner policy wasn't changed.

## PARAMETERS

### -Force

Forces the command to run without asking for user confirmation.

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

### -Reset

Resets the scanner cache so that the scanner initiates a full scan of all the files, even if they were scanned before and the information protection scanner policy wasn't changed.

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

## INPUTS

### None

## OUTPUTS

### System.Object

## NOTES

## RELATED LINKS

[Get-ScannerConfiguration](Get-ScannerConfiguration.md)

[Get-ScanStatus](Get-ScanStatus.md)

[Install-Scanner](Install-Scanner.md)

[Set-ScannerConfiguration](Set-ScannerConfiguration.md)

[Uninstall-Scanner](Uninstall-Scanner.md)

[Update-ScannerDatabase](Update-ScannerDatabase.md)