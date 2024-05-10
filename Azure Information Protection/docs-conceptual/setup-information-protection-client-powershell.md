---
title: Set up Microsoft Purview Information Protection client using PowerShell | Microsoft Docs
description: Describes installing and configuring the Microsoft Purview Information Protection client.
services: azure
author: kccross
manager: laurawi
ms.product: information-protection
ms.service: information-protection
ms.devlang: powershell
ms.topic: reference
ms.date: 05/10/2024
ms.author: krowley
---

# Microsoft Purview Information Protection client

Use the following PowerShell modules with Azure Information Protection: 

- **[AIPService](#aipservice)**. Used to administer Azure Information Protection's Azure Rights Management protection service, and replaces the deprecated [AADRM](#aadrm) module.

- **[AzureInformationProtection](#azureinformationprotection)**. Used to support Azure Information Protection client functionality.

## AIPService
    
These cmdlets let you administer the Azure Rights Management protection service for Azure Information Protection. 

The AIPService module replaces the older module, [AADRM](#aadrm).

For more information about when to use these PowerShell cmdlets and to see groupings of cmdlets by administration tasks, see [Administering protection from Azure Information Protection by using PowerShell](/information-protection/deploy-use/administer-powershell).
    
For upgrading and installation instructions, see [Installing the AIPService PowerShell module](/information-protection/deploy-use/install-powershell).
    

## AzureInformationProtection

This module has cmdlets for the Azure Information Protection unified labeling client that are installed together with the client.

For more information, see:

- [About the AIP unified labeling client](/information-protection/rms-client/aip-clientv2)
- [Using PowerShell with the AIP unified labeling client](/information-protection/rms-client/clientv2-admin-guide-powershell)
- [Install the AIP unified labeling client for users](/information-protection/rms-client/clientv2-admin-guide-install)

### Installing the AzureInformationProtection module

- This module requires Windows PowerShell 4.0. This prerequisite is not checked by the installation. 
- The module installs automatically when you install the full version of the Azure Information Protection clients. Alternately, you can install the module only by using the `PowerShellOnly=true` parameter.

## AADRM
    
The cmdlets in this module let you administer the Azure Rights Management protection service for Azure Information Protection.

This module is now deprecated and replaced with the [AIPService](#aipservice) module, which provides the same functionality with renamed cmdlets. 

The renamed cmdlets in the current module have aliases to the old cmdlets. Cmdlets from the AADRM module that were already deprecated and no longer used were not carried forward to the newer AIPService module.

Support for this older module ended **July 15, 2020**.  
