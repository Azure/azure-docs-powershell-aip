---
external help file: Microsoft.RightsManagementServices.Online.Admin.PowerShell.dll-Help.xml
online version: http://go.microsoft.com/fwlink/?LinkId=623037
schema: 2.0.0
ms.assetid: 3F0BC472-41CC-41CA-A1B5-ACB84B1C2DA9
---

# Get-AadrmDocumentTrackingFeature

## SYNOPSIS
Indicates whether document tracking is enabled or disabled for Azure Information Protection.

## SYNTAX

```
Get-AadrmDocumentTrackingFeature [<CommonParameters>]
```

## DESCRIPTION
[!INCLUDE [AADRM is deprecated](../includes/aadrm-deprecated.md)]

The **Get-AadrmDocumentTrackingFeature** cmdlet indicates whether the Azure Information Protection document tracking feature is enabled or disabled.

You must use PowerShell to get this information about document tracking; you cannot get this information by using a management portal.

For additional information about the document tracking site, see [Configuring and using document tracking for Azure Information Protection](/information-protection/rms-client/client-admin-guide-document-tracking) from the Azure Information Protection client administrator guide.

## EXAMPLES

### Example: Determine whether the document tracking site is enabled
```
PS C:\>Get-AadrmDocumentTrackingFeature
```

This command determines whether the Azure Information Protection document tracking feature is enabled.

## PARAMETERS

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

## OUTPUTS

## NOTES

## RELATED LINKS

[Disable-AadrmDocumentTrackingFeature](./Disable-AadrmDocumentTrackingFeature.md)

[Enable-AadrmDocumentTrackingFeature](./Enable-AadrmDocumentTrackingFeature.md)