---
external help file: AipService.dll-Help.xml
Module Name: AIPService
ms.assetid: BE20B1AF-4D47-4182-A46A-2FB0AB504A93
online version: https://go.microsoft.com/fwlink/?linkid=2045520
schema: 2.0.0
---

# New-AipServiceRightsDefinition

## SYNOPSIS
Creates a rights definition object for a protection template for Azure Information Protection.

## SYNTAX

```
New-AipServiceRightsDefinition [-EmailAddress <String>] [-DomainName <String>]
 -Rights <System.Collections.Generic.List`1[System.String]> [<CommonParameters>]
```

## DESCRIPTION
The **New-AipServiceRightsDefinition** cmdlet creates a **rights definition** object that you store as a variable and then use to create or update a protection template for Azure Information Protection when you use the [Add-AipServiceTemplate](./Add-AipServiceTemplate.md) or [Set-AipServiceTemplateProperty](./Set-AipServiceTemplateProperty.md) cmdlet.

A rights definition object expresses the usage rights that users have to content that Azure Information Protection protects. You can specify a user, a group, or all users in an organization. 

Similar configuration can also be done when you create or configure a protection template in the Azure portal, but this cmdlet offers more fine-grained control. However, this cmdlet does not support the [any authenticated users option](/azure/information-protection/deploy-use/configure-policy-protection#more-information-about-add-any-authenticated-users) that you can select in the Azure portal.

Tip: You can this cmdlet to enable secure collaboration with other organizations when they have user accounts in Azure Active Directory and Office 365. For example, provide an external group VIEW and DOCEDIT rights to collaborate on a joint project. Or, provide VIEW rights to all users in a partner organization.

For more information about protection templates, including how to configure them in the Azure portal, see [Configuring and managing templates for Azure Information Protection](/information-protection/deploy-use/configure-policy-templates).

**Using the Azure Information Protection unified labeling client?**

The Azure Information Protection unified labeling client uses protection templates indirectly. If you have the unified labeling client, we recommend that you use label-based cmdlets instead of modifying your protection templates directly.

For more information, see [Create and publish sensitivity labels](/microsoft-365/compliance/create-sensitivity-labels) in the Microsoft 365 documentation.

## EXAMPLES

### Example 1: Create a rights definition object for a user
```
PS C:\>$R1 = New-AipServiceRightsDefinition -EmailAddress "ElisaDaugherty@Contoso.com" -Rights "VIEW","DOCEDIT"
```

This command creates a rights definition object for the specified user and stores this policy in a variable named R1, which can then be used to create or update a protection template. 

The command includes the rights VIEW and DOCEDIT for a user in the Contoso organization.

### Example 2: Create a rights definition object for all users
```
PS C:\>$R2 = New-AipServiceRightsDefinition -DomainName "Contoso.com" -Rights "VIEW"
```

This command creates a rights definition object for the Contoso organization and stores this policy in a variable named R2, which can then be used to create or update a protection template. The command includes the VIEW right for all users in the Contoso organization.

### Example 3: Create a rights definition object for the "Just for me" configuration
```
PS C:\>$R3 = New-AipServiceRightsDefinition -EmailAddress "IPC_USER_ID_OWNER" -Rights "OWNER"
```

This command creates a rights definition object that applies protection such that only the person who applies the protection can open the document or email with no restrictions. This configuration is sometimes referred to as "Just for me" and might be the required outcome so that a user can save a file to any location and be assured that only they can open it. Because only the person who applies the protection can open the content, this configuration is not suitable for content that requires collaboration. 


## PARAMETERS

### -DomainName
Specifies a domain name for your organization or another organization, to be used for granting rights when you create or update a protection template. When an organization has more than one domain, it does not matter which domain name you specify; users from all verified domains for that organization are automatically included. 

Specify one domain name only for all users in an organization; to grant rights to more than one organization, create another rights definition object.

Note that for authentication to be successful for Azure AD, the user must have an account in Azure Active Directory. Office 365 users automatically have an account in Azure Active Directory. 

You can specify domain names from social providers (such as gmail.com) but authentication for accounts that are not in Azure AD are supported for email only, and when Exchange Online is configured for the new capabilities for Office 365 Message Encryption.


```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -EmailAddress
Specifies the email address of a user or group. The user or group can be internal to your organization, or external. For Azure AD authentication to be successful, the user must have an account in Azure Active Directory. Office 365 users automatically have an account in Azure Active Directory.

Other authentication methods include email address from a social provider (for example, a Gmail account) when Exchange Online is configured for the new capabilities for Office 365 Message Encryption. Some applications also support personal email addresses with a Microsoft account. For more information about using Microsoft accounts for authentication, see the [supported scenarios table](/azure/information-protection/get-started/secure-collaboration-documents#supported-scenarios-for-opening-protected-documents). 

The cmdlet associates the rights that the *Rights* parameter specifies to the user or group that the address specifies.

Tip: If you want to specify all users in your organization or all users in another organization, use the **DomainName** parameter. 

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Rights
Specifies a list of rights. The list contains one or more of the following:

- **VIEW:** Interpreted by most applications as allowed to present the data on the screen.

- **EDIT:** Interpreted by most applications as allowed to modify content in the document and save it.

- **DOCEDIT:** Interpreted by most applications as allowed to modify the content of the document.

- **EXTRACT:** Interpreted by most applications as allowed to copy the content to the clipboard or otherwise extract the content in unencrypted form.

- **OBJMODEL:** Interpreted by most applications as allowed to access the document programmatically; for example, by using macros.

- **EXPORT:** Interpreted by most applications as allowed to save the file in unencrypted form. For example, this right allows you to save in a different file format that does not support protection.

- **PRINT:** Interpreted by most applications as allowed to print the document.

- **OWNER:** User has all rights on the document, including the ability to remove protection.

- **FORWARD:** Interpreted by most applications as allowed to forward an email message, and to add recipients to the To and Cc lines.

- **REPLY:** Interpreted by most applications as allowed to select reply to an email message, without allowing changes in the To or Cc lines.

- **REPLYALL:** Interpreted by most applications as allowed to reply to all recipients of an email message, but does not allow the user to add recipients to the To or Cc lines.

Note: For clarity, the documentation and display text from the module shows these rights as all upper-case letters. However, the values are not case-sensitive and you can specify them in lower or upper case.

For more information about the usage rights, see [Configuring usage rights for Azure Information Protection](/information-protection/deploy-use/configure-usage-rights).

```yaml
Type: System.Collections.Generic.List`1[System.String]
Parameter Sets: (All)
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. 

For more information, see [about_CommonParameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters).

## INPUTS

## OUTPUTS

## NOTES

## RELATED LINKS

[Add-AipServiceTemplate](./Add-AipServiceTemplate.md)

[Set-AipServiceTemplateProperty](./Set-AipServiceTemplateProperty.md)