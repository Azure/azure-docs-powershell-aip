---
external help file: Microsoft.RightsManagementServices.Online.Admin.PowerShell.dll-Help.xml
online version: http://go.microsoft.com/fwlink/?LinkId=400600
schema: 2.0.0
ms.assetid: 469B8EE7-0EE9-4BD7-BC24-A3AD74111FB0
---

# Disable-AadrmUsageLogFeature

## SYNOPSIS
Disables the usage log for Rights Management.

## SYNTAX

```
Disable-AadrmUsageLogFeature [<CommonParameters>]
```

## DESCRIPTION
[!INCLUDE [AADRM is deprecated](../includes/aadrm-deprecated.md)]

The **Disable-AadrmUsageLogFeature** cmdlet disables usage logging for the Azure Rights Management service. If you disable this logging, the cmdlet does not delete existing logs. If you enable usage logging again, logging begins at the point in the log where logging previously stopped.

Note: This cmdlet is not needed and will not run successfully after the usage logging change in February 2016. After this date, usage logging is automatically enabled and cannot be disabled; the only PowerShell cmdlet that you need for Azure Rights Management usage logging is [Get-AadrmUserLog](./Get-AadrmUserLog.md).

For more information about usage logging, see [Logging and analyzing usage of the Azure Rights Management service](/information-protection/deploy-use/log-analyze-usage).

## EXAMPLES

### Example 1: Disable usage logging
```
PS C:\>Disable-AadrmUsageLogFeature
```

This command disables the usage log for your organization.

## PARAMETERS

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

## OUTPUTS

## NOTES

## RELATED LINKS

[Enable-AadrmUsageLogFeature](./Enable-AadrmUsageLogFeature.md)

[Get-AadrmUsageLogFeature](./Get-AadrmUsageLogFeature.md)

[Logging and analyzing usage of the Azure Rights Management service](/information-protection/deploy-use/log-analyze-usage)