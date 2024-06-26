---
title: Overview of PowerShell for information protection
titleSuffix: Microsoft Docs
description: An introduction to the PowerShell modules that you can use with Azure Information Protection and Purview Information Protection.
services: azure
author: libarson
manager: aashishr
ms.product: purview
ms.service: purview-information-protection
ms.devlang: powershell
ms.topic: reference
ms.date: 05/13/2024
ms.author: libarson
---

# Information protection

Use the following PowerShell modules with Azure Information Protection and Purview Information Protection:

- **[AIPService](#aipservice)**. Used to administer Azure Information Protection's Azure Rights Management protection service, and replaces the deprecated AADRM module.

- **[PurviewInformationProtection](#purviewinformationprotection)**. Used to support information protection client functionality, and replaces the deprecated AzureInformationProtection module.

## AIPService

These cmdlets let you administer the Azure Rights Management protection service for Azure Information Protection.

The AIPService module replaces the older module, [AADRM](#deprecated-modules), which is deprecated.

For more information about when to use these PowerShell cmdlets and to see groupings of cmdlets by administration tasks, see [Administering protection from Azure Information Protection by using PowerShell](/information-protection/deploy-use/administer-powershell).

For upgrading and installation instructions, see [Installing the AIPService PowerShell module](/information-protection/deploy-use/install-powershell).

## PurviewInformationProtection

This module has cmdlets for the information protection client that are installed together with the client.

The PurviewInformationProtection module replaces the older module, [AzureInformationProtection](#deprecated-modules), which is deprecated.

For installation instructions, see [Set up the information protection client using PowerShell](setup-information-protection-client-powershell.md).

- This module requires Windows PowerShell 4.0. The installation doesn't check for this prerequisite.
- The module installs automatically when you install the Purview Information Protection client.

## Deprecated modules

The AzureInformationProtection and AADRM modules are now deprecated and was replaced with newer modules. The newer modules provide the same functionality with renamed cmdlets.

The renamed cmdlets in the current modules have aliases to the old cmdlets. Cmdlets from the old modules that were already deprecated and no longer used weren't carried forward to the newer modules.

- The AzureInformationProtection module was replaced with the [PurviewInformationProtection](#purviewinformationprotection) module. Support for this older module ended **May 13, 2024**.

- The AADRM module was replaced with the [AIPService](#aipservice) module. Support for this older module ended **July 15, 2020**.  
