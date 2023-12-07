---
external help file: AipService.dll-Help.xml
Module Name: AIPService
ms.assetid: 60B3F42C-4FEF-435B-AE28-771932FA6251
online version: https://go.microsoft.com/fwlink/?linkid=2044863
schema: 2.0.0
---

# Enable-AipService

## SYNOPSIS
Activates the protection service for Azure Information Protection.

## SYNTAX

```
Enable-AipService [<CommonParameters>]
```

## DESCRIPTION
The **Enable-AipService** cmdlet activates the protection service from Azure Information Protection so that all users in your tenant can protect documents and emails. For more information, see [Activating the protection service from Azure Information Protection](/information-protection/deploy-use/activate-service). 

When you activate the protection service, you turn on this service for all rights-enabled applications and services for your tenant, but some applications and services and might need further configuration before they can use the protection capabilities from Azure Information Protection.

For information about other deployment steps that might be needed, see the [deployment roadmap](/information-protection/plan-design/deployment-roadmap).

## EXAMPLES

### Example 1: Enable the protection service
```
PS C:\>Enable-AipService
```

This command activates the protection service for Azure Information Protection.

## PARAMETERS

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. 

For more information, see [about_CommonParameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters).

## INPUTS

## OUTPUTS

## NOTES

## RELATED LINKS

[Disable-AipService](./Disable-AipService.md)

[Get-AipService](./Get-AipService.md)

[Activating the protection service from Azure Information Protection](/information-protection/deploy-use/activate-service)
