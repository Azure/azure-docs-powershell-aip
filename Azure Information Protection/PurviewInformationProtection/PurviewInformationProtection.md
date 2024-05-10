---
Module Name: PurviewInformationProtection
Module Guid: NA
Download Help Link: NA
Help Version: NA
ms.topic: reference
Locale: en-US
---

# PurviewInformationProtection Module
## Description

The Microsoft Purview Information Protection client helps you classify and label data in your organization at the time of creation, as well as apply protection, based on encryption and usage rights for sensitive data. Labels, and protection are persistent, traveling with the data throughout its lifecycle, so that it’s detectable and controlled at all times – regardless of where it’s stored or with whom it’s shared – internally or externally. Use the PurviewInformationProtection module to configure and manage the client.

The PurviewInformationProtection module is installed with the Microsoft Purview Information Protection unified labeling client. For installation instructions, see [Microsoft Purview Information Protection client](../docs-conceptual/setup-information-protection-client-powershell.md).

## PurviewInformationProtection Cmdlets

- [Add-ScannerRepository](Add-ScannerRepository.md)
Adds a repository to an information protection scanner content scan job.

- [Clear-Authentication](Clear-Authentication.md)
Clears the user settings and Rights Management Service (RMS) templates for the current user.

- [Export-DebugLogs](Export-DebugLogs.md)
Gathers and exports information protection client and scanner log files to a compressed file.

- [Get-FileStatus](Get-FileStatus.md)
Gets the sensitivity label and protection information for a specified file or files.

- [Get-ScannerConfiguration](Get-ScannerConfiguration.md)
Gets the configuration settings for the information protection scanner.

- [Get-ScannerContentScan](Get-ScannerContentScan.md)
Gets details about your content scan job.

- [Get-ScannerDiagnostics](Get-ScannerDiagnostics.md)
Starts a series of health checks for a locally installed information protection scanner service.

- [Get-ScannerRepository](Get-ScannerRepository.md)
Gets repository data for an information protection scanner content scan job.

- [Get-ScanStatus](Get-ScanStatus.md)
Gets the current status of the service for the information protection scanner.

- [Import-ScannerConfiguration](Import-ScannerConfiguration.md)
Imports a local configuration for the information protection scanner.

- [Install-Scanner](Install-Scanner.md)
Installs the information protection scanner.

- [New-CustomPermissions](New-CustomPermissions.md)
Creates an ad-hoc protection policy for custom permissions.

- [Remove-FileLabel](Remove-FileLabel.md)
Removes the sensitivity label from a file.

- [Remove-ScannerContentScan](Remove-ScannerContentScan.md)
Deletes the entire information protection scanner content scan job.

- [Remove-ScannerRepository](Remove-ScannerRepository.md)
Removes a repository from an information protection scanner content scan job.

- [Set-Authentication](Set-Authentication.md)
Sets the authentication credentials for the information protection client.

- [Set-FileLabel](Set-FileLabel.md)
Sets or removes an Azure Information Protection label for a file manually or automatically, and sets or removes the protection according to the label configuration or custom permissions.

- [Set-ScannerDatabase](Set-ScannerDatabase.md)
Sets the service account and database for the information protection scanner.

- [Set-ScannerConfiguration](Set-ScannerConfiguration.md)
Sets optional configuration for the information protection scanner.

- [Set-ScannerContentScan](Set-ScannerContentScan.md)
Defines settings for an Information Protection content scan job.

- [Set-ScannerRepository](Set-ScannerRepository.md)
Updates an existing repository in an information protection scanner content scan job.

- [Start-Scan](Start-Scan.md)
Instructs the information protection scanner to start a one time scan cycle.

- [Stop-Scan](Stop-Scan.md)
Instructs the information protection scanner to immediately stop the currently running scan cycle.

- [Uninstall-Scanner](Uninstall-Scanner.md)
Uninstalls the Windows Server service for the information protection scanner.

- [Update-ScannerDatabase](Update-ScannerDatabase.md)
Updates the database schema for the information protection scanner.
