---
title: Set up the information protection client using PowerShell
titleSuffix: Microsoft Docs
description: This article describes installing and configuring the Microsoft Purview Information Protection client.
services: azure
author: libarson
manager: aashishr
ms.service: purview-information-protection
ms.devlang: powershell
ms.topic: reference
ms.date: 05/13/2024
ms.author: libarson
---

# Set up the information protection client using PowerShell

## Description

Contains instructions for installing the Microsoft Purview Information Protection client and PowerShell cmdlets using PowerShell.

### Use PowerShell with the Microsoft Purview Information Protection client

The Microsoft Purview Information Protection module is installed with the information protection client. The associated PowerShell module is *PurviewInformationProtection*.

The PurviewInformationProtection module enables you to manage the client with commands and automation scripts; for example:

- [Install-Scanner](/powershell/module/purviewinformationprotection/install-scanner): Installs and configures the Information Protection Scanner service on a computer running Windows Server 2019, Windows Server 2016, or Windows Server 2012 R2.
- [Get-FileStatus](/powershell/module/purviewinformationprotection/get-filestatus): Gets the Information Protection label and protection information for a specified file or files.
- [Start-Scan](/powershell/module/purviewinformationprotection/start-scan): Instructs the information protection scanner to start a one-time scan cycle.
- [Set-FileLabel -Autolabel](/powershell/module/purviewinformationprotection/set-filelabel): Scans a file to automatically set an information protection label for a file, according to conditions that are configured in the policy.

### Install the PurviewInformationProtection PowerShell module

#### Installation prerequisites

- This module requires Windows PowerShell 4.0. This prerequisite isn't checked during installation. Make sure that you have the correct version of PowerShell installed.
- Make sure that you have the most recent version of the PurviewInformationProtection PowerShell module by running `Import-Module PurviewInformationProtection`.

#### Installation details

You install and configure the information protection client and associated cmdlets using PowerShell.

The PurviewInformationProtection PowerShell module installs automatically when you install the full version of the information protection client. Alternatively, you can install the module only by using the *PowerShellOnly=true* parameter.

The module is installed in the **\ProgramFiles (x86)\PurviewInformationProtection** folder, and then adds this folder to the `PSModulePath` system variable.

> [!IMPORTANT]
> The PurviewInformationProtection module doesn't support configuring advanced settings for labels or label policies.

To use cmdlets with path lengths greater than 260 characters, use the following [group policy setting](/archive/blogs/jeremykuhne/net-4-6-2-and-long-paths-on-windows-10) that is available starting with Windows 10, version 1607:

**Local Computer Policy** > **Computer Configuration** > **Administrative Templates** > **All Settings** > **Enable Win32 long paths**

For Windows Server 2016, you can use the same group policy setting when you install the latest Administrative Templates (.admx) for Windows 10.

For more information, see the [Maximum Path Length Limitation](/windows/desktop/FileIO/naming-a-file#maximum-path-length-limitation) section from the Windows 10 developer documentation.

### Understand prerequisites for the PurviewInformationProtection PowerShell module

In addition to the installation prerequisites for the PurviewInformationProtection module, you must also activate the [Azure Rights Management service](/azure/information-protection/what-is-azure-rms).

In some cases, you might want to remove protection from files for others that use your own account. For example, you might want to remove protection for others for the sake of data discovery or recovery. If you're using labels to apply protection, you can remove that protection by setting a new label that doesn't apply protection, or you can remove the label.

For cases like this, the following requirements must also be met:

- The super user feature must be enabled for your organization.
- Your account must be configured as an Azure Rights Management super user.

### Run information protection labeling cmdlets unattended

By default, when you run the cmdlets for labeling, the commands run in your own user context in an interactive PowerShell session. To automatically run sensitivity labeling cmdlets, read the following sections:

- [Understand prerequisites for running labeling cmdlets unattended](#understand-prerequisites-for-running-labeling-cmdlets-unattended)
- [Create and configure Microsoft Entra applications for Set-Authentication](#create-and-configure-microsoft-entra-applications-for-set-authentication)
- [Run the Set-Authentication cmdlet](#run-the-set-authentication-cmdlet)

#### Understand prerequisites for running labeling cmdlets unattended

To run Purview Information Protection labeling cmdlets unattended, use the following access details:

- **A Windows account** that can sign in interactively.

- **A Microsoft Entra account**, for delegated access. For ease of administration, use a single account that synchronizes from Active Directory to Microsoft Entra ID.

    For the delegated user account, configure the following requirements:

    |Requirement  |Details  |
    |---------|---------|
    |**Label policy**     |  Make sure that you have a label policy assigned to this account and that the policy contains the published labels you want to use. <br><br>If you use label policies for different users, you might need to create a new label policy that publishes all your labels, and publish the policy to just this delegated user account.    |
    |**Decrypting content**     |    If this account needs to decrypt content, for example, to reprotect files and inspect files protected by others, make it a super user for Information Protection and make sure the super user feature is enabled.     |
    |**Onboarding controls**     |    If you have implemented onboarding controls for a phased deployment, make sure that this account is included in your onboarding controls you've configured.     |

- **A Microsoft Entra access token**, which sets and stores credentials for the delegated user to authenticate to Microsoft Purview Information Protection. When the token in Microsoft Entra ID expires, you must run the cmdlet again to acquire a new token.

    The parameters for [Set-Authentication](/powershell/module/purviewinformationprotection/set-authentication) use values from an app registration process in Microsoft Entra ID. For more information, see [Create and configure Microsoft Entra applications for Set-Authentication](#create-and-configure-azure-ad-applications-for-set-authentication).

Run the labeling cmdlets non-interactively by first running the [Set-Authentication](/powershell/module/purviewinformationprotection/set-authentication) cmdlet.

The computer running the [Set-Authentication](/powershell/module/purviewinformationprotection/set-authentication) cmdlet downloads the labeling policy that's assigned to your delegated user account in the Microsoft Purview compliance portal.

<a name='create-and-configure-azure-ad-applications-for-set-authentication'></a>

#### Create and configure Microsoft Entra applications for Set-Authentication

The [Set-Authentication](/powershell/module/purviewinformationprotection/set-authentication) cmdlet requires an app registration for the *AppId* and *AppSecret* parameters.

**To create a new app registration for the unified labeling client [Set-Authentication](/powershell/module/purviewinformationprotection/set-authentication) cmdlet**:

1. In a new browser window, sign in the [Azure portal](https://portal.azure.com/) to the Microsoft Entra tenant that you use with Microsoft Purview Information Protection.

1. Navigate to **Microsoft Entra ID** > **Manage** > **App registrations**, and select **New registration**.

1. On the **Register an application** pane, specify the following values, and then select **Register**:

   |Option  |Value  |
   |---------|---------|
   |**Name**     |  `AIP-DelegatedUser` <br>Specify a different name as needed. The name must be unique per tenant.       |
   |**Supported account types**     |   Select **Accounts in this organizational directory only**.      |
   |**Redirect URI (optional)**     |   Select **Web**, and then enter `https://localhost`.    |

1. On the **AIP-DelegatedUser** pane, copy the value for the **Application (client) ID**.

    The value looks similar to the following example: `77c3c1c3-abf9-404e-8b2b-4652836c8c66`.

    This value is used for the *AppId* parameter when you run the [Set-Authentication](/powershell/module/purviewinformationprotection/set-authentication) cmdlet. Paste and save the value for later reference.

1. From the sidebar, select **Manage** > **Certificates & secrets**.

    Then, on the **AIP-DelegatedUser - Certificates & secrets** pane, in the **Client secrets** section, select **New client secret**.

1. For **Add a client secret**, specify the following, and then select **Add**:

   |Field  |Value  |
   |---------|---------|
   |**Description**     |  `Microsoft Purview Information Protection client`       |
   |**Expires**     |   Specify your choice of duration (**1 year**, **2 years**, or **never expires**)     |

1. Back on the **AIP-DelegatedUser - Certificates & secrets** pane, in the **Client secrets** section, copy the string for the **VALUE**.

   This string looks similar to the following example: `OAkk+rnuYc/u+]ah2kNxVbtrDGbS47L4`.

   To make sure you copy all the characters, select the icon to **Copy to clipboard**.

    > [!IMPORTANT]
    > Save this string because it's not displayed again and it can't be retrieved. As with any sensitive information that you use, store the saved value securely and restrict access to it.
    >

1. From the sidebar, select **Manage** > **API permissions**.

   On the **AIP-DelegatedUser - API permissions** pane, select **Add a permission**.

1. On the **Request API permissions** pane, make sure that you're on the **Microsoft APIs** tab, and select **Azure Rights Management Services**.

   When you're prompted for the type of permissions that your application requires, select **Application permissions**.

1. For **Select permissions**, expand **Content** and select the following, and then select **Add permissions**.

   - **Content.DelegatedReader**
   - **Content.DelegatedWriter**

1. Back on the **AIP-DelegatedUser - API permissions** pane, select **Add a permission** again.

   On the **Request AIP permissions** pane, select **APIs my organization uses**, and search for **Microsoft Information Protection Sync Service**.

1. On the **Request API permissions** pane, select **Application permissions**.

   For **Select permissions**, expand **UnifiedPolicy**, select **UnifiedPolicy.Tenant.Read**, and then select **Add permissions**.

1. Back on the **AIP-DelegatedUser - API permissions** pane, select **Grant admin consent for _your tenant_** and select **Yes** for the confirmation prompt.

After this step, the registration of this app with a secret completes. You're ready to run [Set-Authentication](/powershell/module/purviewinformationprotection/set-authentication) with the parameters *AppId*, and *AppSecret*. Additionally, you need your tenant ID.

> [!TIP]
>You can quickly copy your tenant ID by using Azure portal: **Microsoft Entra ID** > **Manage** > **Properties** > **Directory ID**.

### Run the Set-Authentication cmdlet

1. Open Windows PowerShell with the **Run as administrator option**.

1. In your PowerShell session, create a variable to store the credentials of the Windows user account that runs non-interactively. For example, if you created a service account for the scanner:

   ```PowerShell
   $pscreds = Get-Credential "CONTOSO\srv-scanner"
   ```

   You're prompted for this account's password.

1. Run the Set-Authentication cmdlet, with the *OnBeHalfOf* parameter, specifying as its value the variable that you created.

   Also specify your app registration values, your tenant ID, and the name of the delegated user account in Microsoft Entra ID. For example:

   ```PowerShell
   Set-Authentication -AppId "77c3c1c3-abf9-404e-8b2b-4652836c8c66" -AppSecret "OAkk+rnuYc/u+]ah2kNxVbtrDGbS47L4" -TenantId "9c11c87a-ac8b-46a3-8d5c-f4d0b72ee29a" -DelegatedUser scanner@contoso.com -OnBehalfOf $pscreds
   ```
