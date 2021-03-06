---
external help file: AipService.dll-Help.xml
Module Name: AIPService
ms.assetid: 0AB1207B-C468-4C1A-ACED-DD1B182701B2
online version: https://go.microsoft.com/fwlink/?linkid=2044846
schema: 2.0.0
---

# Disable-AipServiceIPCv3

## SYNOPSIS
Disables the MSIPC v3 platform for Azure Information Protection.

## SYNTAX

```
Disable-AipServiceIPCv3 [<CommonParameters>]
```

## DESCRIPTION
The **Disable-AipServiceIPCv3** cmdlets disables the MSIPC v3 platform on mobile devices such as iOS and Android. This platform must be enabled to support the protection service from Azure Information Protection.

You must use PowerShell to do this configuration; you cannot do this configuration by using a management portal.

## EXAMPLES

### Example1: Disable the MSIPC v3 platform for iOS and Android devices
```
PS C:\>Disable-AipServiceIPCv3
```

This command disables the MSIPC v3 platform so that iOS and Android mobile devices cannot use the protection service.

## PARAMETERS

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. 

For more information, see [about_CommonParameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters).

## INPUTS

## OUTPUTS

## NOTES

## RELATED LINKS

[Enable-AipServiceIPCv3](./Enable-AipServiceIPCv3.md)

[Get-AipServiceIPCv3](./Get-AipServiceIPCv3.md)