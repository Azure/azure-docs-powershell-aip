---
external help file: AIP.dll-Help.xml
Module Name: AzureInformationProtection
ms.assetid: 031B84B2-E380-4989-8FD9-45CC777FE017
online version: https://go.microsoft.com/fwlink/?linkid=841547
schema: 2.0.0
---

# New-RMSProtectionLicense

## SYNOPSIS
Creates an ad-hoc rights policy for RMS protection.

## SYNTAX

```
New-RMSProtectionLicense [-RmsServer <String>] [-OwnerEmail <String>] [-UserEmail <String[]>]
 [-Permission <String[]>] [-ValidForDays <String>] [-Name <String>] [-Description <String>]
 [<CommonParameters>]
```

## DESCRIPTION
The **New-RMSProtectionLicense** cmdlet creates an ad-hoc rights policy that you store as a variable and then use to protect a file or files when you run the [Protect-RMSFile](./Protect-RMSFile.md) cmdlet.

Create an ad-hoc rights policy (also known as a publishing license) when you cannot use a previously created rights policy template.


## EXAMPLES

### Example 1: Create an ad-hoc policy that has a different owner and grants another user Edit rights
```
PS C:\>$License = New-RMSProtectionLicense -OwnerEmail "user1@contoso.com" -UserEmail "user2@contoso.com" -Permission "EDIT"
```

This command creates an ad-hoc rights policy that sets user1@contoso.com as the owner and grants user2@contoso.com EDIT rights, and stores this policy in a variable named License. This ad-hoc policy can then be used to apply protection to a file or files.

There is no output displayed for this command.

### Example 2: Create an ad-hoc policy with an expiry period that grants a group View and Extract rights
```
PS C:\>$License = New-RMSProtectionLicense -UserEmail "marketing@contoso.com" -Permission "VIEW", "EXTRACT" -ValidForDays 100
```

This command creates an ad-hoc rights policy with an expiry period of 100 days that grants the marketing group marketing@contoso.com VIEW and EXTRACT rights, and stores this policy in a variable named License.

There is no output displayed for this command.

### Example 3: Create an ad-hoc rights policy for a user and then protect a file using the policy
```
PS C:\>$License = New-RMSProtectionLicense -OwnerEmail 'user1@contoso.com' -UserEmail 'user2@contoso.com','user3@contoso.com' -Permission 'VIEW','PRINT'
PS C:\> Protect-RMSFile -License $License -File "C:\Test.txt"
InputFile             EncryptedFile
---------             -------------
C:\Test.txt           C:\Test.ptxt
```

The first command creates an ad-hoc rights policy that sets user1@contoso.com as the owner and grants user2@contoso.com and user3@contoso.com VIEW and PRINT rights, and stores this policy in a variable named License.

The second command then uses the created ad-hoc policy to protect the file **C:\Test.txt**.

## PARAMETERS

### -Description
Specifies the description of the rights policy.

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

### -Name
Specifies the name of this  rights policy.

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

### -OwnerEmail
Specifies the Rights Management owner of the rights policy by email address. You can use this parameter to set a Rights Management owner other than yourself.

By default, the account running this cmdlet is both the Rights Management issuer and the Rights Management owner of the protected file. This parameter lets you assign a different Rights Management owner to the protected file so that the specified account has all usage rights (Full Control) for the file and can always access it. The Rights Management owner is independent from the Windows file system owner. For more information, see [Rights Management issuer and Rights Management owner](/information-protection/configure-usage-rights#rights-management-issuer-and-rights-management-owner).

If you do not specify a value, the cmdlet will use your email address to identify you as the Rights Management owner of this ad-hoc rights policy.

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

### -Permission
Specifies the usage rights for the ad-hoc policy. Use this parameter and the *UserEmail* parameter to grant rights to specified users.

The acceptable values for this parameter:
- VIEW
- EDIT
- PRINT
- EXPORT
- COMMENT
- VIEWRIGHTSDATA
- EDITRIGHTSDATA
- EXTRACT
- OWNER
- DOCEDIT
- OBJMODEL

Warning: If you later want to remove this rights policy from a file, you must have the EXTRACT or OWNER right to use the [Unprotect-RMSFile](./Unprotect-RMSFile.md) cmdlet to unprotect a file, or be a Rights Management super user for your organization.

For more information about these rights, see [Configuring usage rights for Azure Information Protection](/information-protection/configure-usage-rights) on the Microsoft documentation site.

```yaml
Type: String[]
Parameter Sets: (All)
Aliases:
Accepted values: VIEW, EDIT, PRINT, EXPORT, COMMENT, VIEWRIGHTSDATA, EDITRIGHTSDATA, EXTRACT, OWNER, DOCEDIT, OBJMODEL

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -RmsServer
Specifies the name of an AD RMS server (or cluster) to use when creating this ad-hoc rights policy.

This parameter is not applicable for Azure RMS or if your computer knows the right AD RMS server to use by using service discovery.

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

### -UserEmail
Specifies users who will have rights to use the file or files that is protected by this ad-hoc policy. Use this parameter and the *Permission* parameter to grant rights to specified users or groups. 

These users or groups can be internal to your organization, or external. For Azure AD authentication to be successful, the user must have an account in Azure Active Directory. Office 365 users automatically have an account in Azure Active Directory.

Some applications also support personal email addresses with a Microsoft account. For more information about using Microsoft accounts for authentication, see the [supported scenarios table](/azure/information-protection/get-started/secure-collaboration-documents#supported-scenarios-for-opening-protected-documents).


```yaml
Type: String[]
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -ValidForDays
Specifies an expiry period in number of days, which starts when the ad-hoc policy is applied to a file or files.

After this expiry period, the specified users will no longer be able to access the file or files. However, the owner and a super user can always access the file, even after the expiry period is reached.

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

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. 

For more information, see about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

## OUTPUTS

## NOTES

## RELATED LINKS

[Protect-RMSFile](./Protect-RMSFile.md)

[Unprotect-RMSFile](./Unprotect-RMSFile.md)