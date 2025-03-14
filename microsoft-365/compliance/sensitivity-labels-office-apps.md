---
title: "Manage sensitivity labels in Office apps"
f1.keywords:
- NOCSH
ms.author: cabailey
author: cabailey
manager: laurawi
ms.date: 
audience: Admin
ms.topic: conceptual
ms.service: O365-seccomp
ms.localizationpriority: high
ms.collection: M365-security-compliance
search.appverid: 
- MOE150
- MET150
description: Information for IT administrators to manage sensitivity labels in Office apps for desktop, mobile, and the web.
ms.custom: seo-marvel-apr2020
---

# Manage sensitivity labels in Office apps

>*[Microsoft 365 licensing guidance for security & compliance](/office365/servicedescriptions/microsoft-365-service-descriptions/microsoft-365-tenantlevel-services-licensing-guidance/microsoft-365-security-compliance-licensing-guidance).*

When you have [published](create-sensitivity-labels.md#publish-sensitivity-labels-by-creating-a-label-policy) sensitivity labels from the Microsoft 365 compliance center or equivalent labeling center, they start to appear in Office apps for users to classify and protect data as it's created or edited.

Use the information in this article to help you successfully manage sensitivity labels in Office apps. For example, identify the minimum versions of apps you need to support built-in labeling, and understand interactions with the Azure Information Protection unified labeling client and compatibility with other apps and services.

## Labeling client for desktop apps

To use sensitivity labels that are built into Office desktop apps for Windows and Mac, you must use a subscription edition of Office. This labeling client doesn't support standalone editions of Office, such as Office 2016 or Office 2019.

To use sensitivity labels with these standalone editions of Office on Windows computers, install the [Azure Information Protection unified labeling client](/azure/information-protection/rms-client/aip-clientv2).

## Support for sensitivity label capabilities in apps

For each capability, the following tables list the minimum Office version that you need to support sensitivity labels using built-in labeling. Or, if the label capability is in public preview or under review for a future release. Use the [Microsoft 365 roadmap](https://aka.ms/MIPC/Roadmap) for details about new capabilities that are planned for future releases.

New versions of Office apps are made available at different times for different update channels. For Windows, you'll get the new capabilities earlier when you are on the Current Channel or Monthly Enterprise Channel, rather than Semi-Annual Enterprise Channel. The minimum version numbers can also be different from one update channel to the next. For more information, see [Overview of update channels for Microsoft 365 Apps](/deployoffice/overview-update-channels) and [Update history for Microsoft 365 Apps](/officeupdates/update-history-microsoft365-apps-by-date).

New capabilities that are in private preview are not included in the table but you might be able to join these previews by nominating your organization for the [Microsoft Information Protection private preview program](https://aka.ms/mip-preview).

Office for iOS and Office for Android: Sensitivity labels are built into the [Office app](https://www.microsoft.com/en-us/microsoft-365/blog/2020/02/19/new-office-app-android-ios-available/).

Additional capabilities are available when you install the Azure Information Protection unified labeling client, which runs on Windows computers only. For these details, see [Compare the labeling clients for Windows computers](/azure/information-protection/rms-client/use-client#compare-the-labeling-clients-for-windows-computers).

> [!TIP]
> When you compare the minimum versions in the tables with the versions you have, remember the common practice of release versions to omit leading zeros.
> 
> For example, you have version 4.2128.0 and read that 4.7.1+ is the minimum version. For easier comparison, read 4.7.1 (no leading zeros) as 4.**0007**.1 (and not 4.**7000**.1). Your version of 4.2128.0 is higher than 4.0007.1, so your version is supported.

### Sensitivity label capabilities in Word, Excel, and PowerPoint

The numbers listed are the minimum Office application versions required for each capability. 

> [!NOTE]
> For Windows and the Semi-Annual Enterprise Channel, the minimum supported version numbers might not yet be released. [Learn more](/officeupdates/update-history-microsoft365-apps-by-date#supported-versions)
 
|Capability |Windows |Mac |iOS |Android |Web |
|-----------|-------:|----|----|--------|----|
|[Manually apply, change, or remove label](https://support.microsoft.com/en-us/office/apply-sensitivity-labels-to-your-files-and-email-in-office-2f96e7cd-d5a4-403b-8bd7-4cc636bae0f9)| Current Channel: 1910+ <br /><br> Monthly Enterprise Channel: 1910+ <br /><br> Semi-Annual Enterprise Channel: 2002+ | 16.21+     | 2.21+ | 16.0.11231+ | [Yes - opt-in](sensitivity-labels-sharepoint-onedrive-files.md) |
|[Apply a default label](sensitivity-labels.md#what-label-policies-can-do) to new documents                                         | Current Channel: 1910+ <br /><br> Monthly Enterprise Channel: 1910+ <br /><br> Semi-Annual Enterprise Channel: 2002+ | 16.21+     | 2.21+ | 16.0.11231+ | [Yes - opt-in](sensitivity-labels-sharepoint-onedrive-files.md)                                                        |
|[Apply a default label](sensitivity-labels.md#what-label-policies-can-do) to existing documents | Preview: Rolling out to [Beta Channel](https://office.com/insider) | Preview: Rolling out to [Beta Channel](https://office.com/insider) | Under review | Under review | Rolling out: [Yes - opt-in](sensitivity-labels-sharepoint-onedrive-files.md) |
|[Require a justification to change a label](sensitivity-labels.md#what-label-policies-can-do)                     | Current Channel: 1910+ <br /><br> Monthly Enterprise Channel: 1910+  <br /><br> Semi-Annual Enterprise Channel: 2002+ | 16.21+     | 2.21+ | 16.0.11231+ | [Yes - opt-in](sensitivity-labels-sharepoint-onedrive-files.md) |
|[Provide help link to a custom help page](sensitivity-labels.md#what-label-policies-can-do)                       | Current Channel: 1910+ <br /><br> Monthly Enterprise Channel: 1910+ <br /><br> Semi-Annual Enterprise Channel: 2002+ | 16.21+     | 2.21+ | 16.0.11231+ | [Yes - opt-in](sensitivity-labels-sharepoint-onedrive-files.md) |
|[Mark the content](sensitivity-labels.md#what-sensitivity-labels-can-do)                                              | Current Channel: 1910+ <br /><br> Monthly Enterprise Channel: 1910+ <br /><br> Semi-Annual Enterprise Channel: 2002+ | 16.21+     | 2.21+ | 16.0.11231+ | [Yes - opt-in](sensitivity-labels-sharepoint-onedrive-files.md) |
|[Dynamic markings with variables](#dynamic-markings-with-variables)                                              | Current Channel: 2010+ <br /><br> Monthly Enterprise Channel: 2010+ <br /><br> Semi-Annual Enterprise Channel: 2102+ | 16.42+     | 2.42+ | 16.0.13328+ | [Yes - opt-in](sensitivity-labels-sharepoint-onedrive-files.md) |
|[Assign permissions now](encryption-sensitivity-labels.md#assign-permissions-now)                                 | Current Channel: 1910+ <br /><br> Monthly Enterprise Channel: 1910+ <br /><br> Semi-Annual Enterprise Channel: 2002+ | 16.21+     | 2.21+ | 16.0.11231+ | [Yes - opt-in](sensitivity-labels-sharepoint-onedrive-files.md) |
|[Let users assign permissions: <br /> - Prompt users](encryption-sensitivity-labels.md#let-users-assign-permissions)                     |Current Channel: 2004+ <br /><br> Monthly Enterprise Channel: 2004+ <br /><br> Semi-Annual Enterprise Channel: 2008+ | 16.35+   | Under review   | Under review         | Under review                                                        |
|[Audit label-related user activity](data-classification-activity-explorer.md)                      | Current Channel: 2011+ <br /><br> Monthly Enterprise Channel: 2011+ <br /><br> Semi-Annual Enterprise Channel: 2108+ | 16.43+ | 2.46+ | 16.0.13628+ | Yes <sup>\*</sup>                                                        |
|[Require users to apply a label to their email and documents](#require-users-to-apply-a-label-to-their-email-and-documents)   | Current Channel: 2101+ <br /><br> Monthly Enterprise Channel: 2101+ <br /><br> Semi-Annual Enterprise Channel: 2108+ | 16.45+         | 2.47+ | 16.0.13628+ | [Yes - opt-in](sensitivity-labels-sharepoint-onedrive-files.md)                                            
|[Apply a sensitivity label to content automatically](apply-sensitivity-label-automatically.md) <br /> - Using sensitive info types                    | Current Channel: 2009+ <br /><br> Monthly Enterprise Channel: 2009+ <br /><br> Semi-Annual Enterprise Channel: 2102+ | 16.44+ | Under review | Under review | [Yes - opt-in](sensitivity-labels-sharepoint-onedrive-files.md) |
|[Apply a sensitivity label to content automatically](apply-sensitivity-label-automatically.md) <br /> - Using trainable classifiers                    | Current Channel: 2105+ <br /><br> Monthly Enterprise Channel: 2105+ <br /><br> Semi-Annual Enterprise Channel: 2018+ | Under review | Under review | Under review | [Yes - opt-in](sensitivity-labels-sharepoint-onedrive-files.md) |
|[Support co-authoring and AutoSave](sensitivity-labels-coauthoring.md) for labeled and encrypted documents | Current Channel: 2107+ <br /><br> Monthly Enterprise Channel: 2107+ <br /><br> Semi-Annual Enterprise Channel: Under review |  16.51+ | Under review | Under review | [Yes - opt-in](sensitivity-labels-sharepoint-onedrive-files.md) |
|

**Footnotes:**

<sup>\*</sup>
Currently, doesn't include justification text to remove a label or lower the classification level

### Sensitivity label capabilities in Outlook

The numbers listed are the minimum Office application versions required for each capability. 

> [!NOTE]
> For Windows and the Semi-Annual Enterprise Channel, the minimum supported version numbers might not yet be released. [Learn more](/officeupdates/update-history-microsoft365-apps-by-date#supported-versions)

|Capability |Outlook for Windows |Outlook for Mac |Outlook on iOS |Outlook on Android |Outlook on the web |
|-----------|-------------------:|----------------|---------------|-------------------|-------------------|
|[Manually apply, change, or remove label](https://support.microsoft.com/en-us/office/apply-sensitivity-labels-to-your-files-and-email-in-office-2f96e7cd-d5a4-403b-8bd7-4cc636bae0f9)| Current Channel: 1910+ <br /><br> Monthly Enterprise Channel: 1910+ <br /><br> Semi-Annual Enterprise Channel: 2002+ | 16.21+                 | 4.7.1+         | 4.0.39+           | Yes               |
|[Apply a default label](sensitivity-labels.md#what-label-policies-can-do)                                         | Current Channel: 1910+ <br /><br> Monthly Enterprise Channel: 1910+ <br /><br> Semi-Annual Enterprise Channel: 2002+ | 16.21+                 | 4.7.1+         | 4.0.39+           | Yes               |
|[Require a justification to change a label](sensitivity-labels.md#what-label-policies-can-do)                     | Current Channel: 1910+ <br /><br> Monthly Enterprise Channel: 1910+ <br /><br> Semi-Annual Enterprise Channel: 2002+ | 16.21+                 | 4.7.1+         | 4.0.39+           | Yes               |
|[Provide help link to a custom help page](sensitivity-labels.md#what-label-policies-can-do)                       | Current Channel: 1910+ <br /><br> Monthly Enterprise Channel: 1910+ <br /><br> Semi-Annual Enterprise Channel: 2002+ | 16.21+                 | 4.7.1+         | 4.0.39+           | Yes               |
|[Mark the content](sensitivity-labels.md#what-sensitivity-labels-can-do)                                              | Current Channel: 1910+ <br /><br> Monthly Enterprise Channel: 1910+ <br /><br> Semi-Annual Enterprise Channel: 2002+ | 16.21+                 | 4.7.1+         | 4.0.39+           | Yes               |
|[Dynamic markings with variables](#dynamic-markings-with-variables)                                              | Current Channel: 1910+ <br /><br> Monthly Enterprise Channel: 1910+ <br /><br> Semi-Annual Enterprise Channel: 2002+ | 16.21+                 | 4.7.1+         | 4.0.39+           | Yes               |
|[Assign permissions now](encryption-sensitivity-labels.md#assign-permissions-now)                                 | Current Channel: 1910+ <br /><br> Monthly Enterprise Channel: 1910+ <br /><br> Semi-Annual Enterprise Channel: 2002+ | 16.21+                 | 4.7.1+         | 4.0.39+           | Yes               |
|[Let users assign permissions: <br /> - Do Not Forward](encryption-sensitivity-labels.md#let-users-assign-permissions)                     | Current Channel: 1910+ <br /><br> Monthly Enterprise Channel: 1910+ <br /><br> Semi-Annual Enterprise Channel: 2002+ | 16.21+                 | 4.7.1+         | 4.0.39+           | Yes               |
|[Let users assign permissions: <br /> - Encrypt-Only](encryption-sensitivity-labels.md#let-users-assign-permissions)  | Current Channel: 2011+ <br /><br> Monthly Enterprise Channel: 2011+ <br /><br> Semi-Annual Enterprise Channel: 2108+ | 16.48+ <sup>\*</sup> | 4.2112.0+  | 4.2112.0+ | Yes |
|[Require users to apply a label to their email and documents](#require-users-to-apply-a-label-to-their-email-and-documents)   | Current Channel: 2101+ <br /><br> Monthly Enterprise Channel: 2101+ <br /><br> Semi-Annual Enterprise Channel: 2108+ | 16.43+ <sup>\*</sup>                    | 4.2111+            | 4.2111+                | Yes                |
|[Audit label-related user activity](data-classification-activity-explorer.md) | Current Channel: 2011+ <br /><br> Monthly Enterprise Channel: 2011+ <br /><br> Semi-Annual Enterprise Channel: Under review | 16.51+ <sup>\*</sup> | 4.2126+ | 4.2126+ | Yes |
|[Apply a sensitivity label to content automatically](apply-sensitivity-label-automatically.md) <br /> - Using sensitive info types                    | Current Channel: 2009+ <br /><br> Monthly Enterprise Channel: 2009+ <br /><br> Semi-Annual Enterprise Channel: 2102+ | 16.44+ <sup>\*</sup>                    | Under review           | Under review               | Yes |
|[Apply a sensitivity label to content automatically](apply-sensitivity-label-automatically.md) <br /> - Using trainable classifiers                    | Current Channel: 2105+ <br /><br> Monthly Enterprise Channel: 2105+ <br /><br> Semi-Annual Enterprise Channel: 2108+ | Under review                    | Under review           | Under review               | Yes |
|[Different settings for default label and mandatory labeling](#outlook-specific-options-for-default-label-and-mandatory-labeling)                    | Current Channel: 2105+ <br /><br> Monthly Enterprise Channel: 2105+ <br /><br> Semi-Annual Enterprise Channel: 2108+ | 16.43+ <sup>\*</sup>                   | 4.2111+           | 4.2111+               | Yes |
|

**Footnotes:**

<sup>\*</sup>
Requires the [new Outlook for Mac](https://support.microsoft.com/office/the-new-outlook-for-mac-6283be54-e74d-434e-babb-b70cefc77439)


## Office built-in labeling client and other labeling solutions

The Office built-in labeling client downloads sensitivity labels and sensitivity label policy settings from the Microsoft 365 compliance center. 

To use the Office built-in labeling client, you must have one or more [label policies published](create-sensitivity-labels.md#publish-sensitivity-labels-by-creating-a-label-policy) to users from the compliance center, and a [supported version of Office](#support-for-sensitivity-label-capabilities-in-apps).

If both of these conditions are met but you need to turn off the built-in labels in Office apps, use the following Group Policy setting:

1. Navigate to **User Configuration/Administrative Templates/Microsoft Office 2016/Security Settings**.

2. Set **Use the Sensitivity feature in Office to apply and view sensitivity labels** to **0**. 
 
Deploy this setting by using Group Policy, or by using the [Office cloud policy service](/DeployOffice/overview-office-cloud-policy-service). The setting takes effect when Office apps restart.

### Office built-in labeling client and the Azure Information Protection client

If users have the [Azure Information Protection client](/azure/information-protection/rms-client/aip-clientv2) installed on their Windows computers, by default, built-in labels are turned off in [Office apps that support them](#labeling-client-for-desktop-apps). Because built-in labels don't use an Office add-in, as used by the Azure Information Protection client, they have the benefit of more stability and better performance. They also support the latest features, such as advanced classifiers.

Rather than uninstalling the Azure Information Protection client, we recommend you prevent the Azure Information Protection add-in from loading in Office apps. Then, you get the benefits of built-in labeling in Office apps, and the benefits of the Azure Information Protection client labeling files outside Office apps. For example, the Azure Information Protection client can label all file types by using File Explorer and PowerShell. For more information about the labeling features supported outside Office apps, see [Sensitivity labels and Azure Information Protection](sensitivity-labels.md#sensitivity-labels-and-azure-information-protection).

To prevent the Azure Information Protection client add-in loading in Office apps, use the Group Policy setting **List of managed add-ins** as documented in [No Add-ins loaded due to group policy settings for Office 2013 and Office 2016 programs](https://support.microsoft.com/help/2733070/no-add-ins-loaded-due-to-group-policy-settings-for-office-2013-and-off).

For your Office apps that support built-in labeling, use the configuration for Microsoft Word 2016, Excel 2016, PowerPoint 2016, and Outlook 2016, specify the following programmatic identifiers (ProgID) for the Azure Information Protection client, and set the option to **0: The add-in is always disabled (blocked)**

|Application  |ProgID  |
|---------|---------|
|Word     |     `MSIP.WordAddin`    |
|Excel     |  `MSIP.ExcelAddin`       |
|PowerPoint     |   `MSIP.PowerPointAddin`      |
|Outlook | `MSIP.OutlookAddin` |
| | | 

Deploy this setting by using Group Policy, or by using the [Office cloud policy service](/DeployOffice/overview-office-cloud-policy-service).

> [!IMPORTANT]
> If you use the Group Policy setting **Use the Sensitivity feature in Office to apply and view sensitivity labels** and set this to **1**, there are some situations where the Azure Information Protection client might still load in Office apps. Blocking the add-in from loading in each app prevents this happening.

Alternatively, you can interactively disable or remove the **Microsoft Azure Information Protection** Office add-in from Word, Excel, PowerPoint, and Outlook. This method is suitable for a single computer, and ad-hoc testing. For instructions, see [View, manage, and install add-ins in Office programs](https://support.office.com/article/16278816-1948-4028-91e5-76dca5380f8d). 

Whichever method you choose, the changes take effect when Office apps restart.

For detailed information about which features are supported by the Azure Information Protection client and the Office built-in labeling client, see [Choose your Windows labeling solution](/azure/information-protection/rms-client/use-client#choose-your-windows-labeling-solution) from the Azure Information Protection documentation.

## Office file types supported

Office apps that have built-in labeling for Word, Excel, and PowerPoint files support the Open XML format (such as .docx and .xlsx) but not the Microsoft Office 97-2003 format (such as .doc and .xls), Open Document Format (such as .odt and .ods), or other formats. When a file type is not supported for built-in labeling, the **Sensitivity** button is not available in the Office app.

The Azure Information Protection unified labeling client supports both the Open XML format and the Microsoft Office 97-2003 format. For more information, see [File types supported by the Azure Information Protection unified labeling client](/azure/information-protection/rms-client/clientv2-admin-guide-file-types) from that client's admin guide.

For other labeling solutions, check their documentation for file types supported.

## Protection templates and sensitivity labels

Administrator-defined [protection templates](/azure/information-protection/configure-policy-templates), such as those you define for Office 365 Message Encryption, aren't visible in Office apps when you're using built-in labeling. This simplified experience reflects that there's no need to select a protection template, because the same settings are included with sensitivity labels that have encryption enabled.

You can convert an existing template into a sensitivity label when you use the [New-Label](/powershell/module/exchange/new-label) cmdlet with the *EncryptionTemplateId* parameter.

## Information Rights Management (IRM) options and sensitivity labels

Sensitivity labels that you configure to apply encryption remove the complexity from users to specify their own encryption settings. In many Office apps, these individual encryption settings can still be manually configured by users by using Information Rights Management (IRM) options. For example, for Windows apps:

- For a document:  **File** > **Info** > **Protect Document** > **Restrict Access**
- for an email: From the **Options** tab > **Encrypt** 
  
When users initially label a document or email, they can override your label configuration settings with their own encryption settings. For example:

- A user applies the **Confidential \ All Employees** label to a document and this label is configured to apply encryption settings for all users in the organization. This user then manually configures the IRM settings to restrict access to a user outside your organization. The end result is a document that's labeled **Confidential \ All Employees** and encrypted, but users in your organization can't open it as expected.

- A user applies the **Confidential \ Recipients Only** label to an email and this email is configured to apply the encryption setting of **Do Not Forward**. In the Outlook app, this user then manually selects the IRM setting for Encrypt-Only. The end result is that while the email does remain encrypted, it can be forwarded by recipients, despite having the **Confidential \ Recipients Only** label.
    
    As an exception, for Outlook on the web, the options from the **Encrypt** menu aren't available for a user to select when the currently selected label applies encryption.

- A user applies the **General** label to a document, and this label isn't configured to apply encryption. This user then manually configures the IRM settings to restrict access to the document. The end result is a document that's labeled **General** but that also applies encryption so that some users can't open it as expected.

If the document or email is already labeled, a user can do any of these actions if the content isn't already encrypted, or they have the [usage right](/azure/information-protection/configure-usage-rights#usage-rights-and-descriptions) Export or Full Control. 

For a more consistent label experience with meaningful reporting, provide appropriate labels and guidance for users to apply only labels to protect documents and emails. For example:

- For exception cases where users must assign their own permissions, provide labels that [let users assign their own permissions](encryption-sensitivity-labels.md#let-users-assign-permissions). 

- Instead of users manually removing encryption after selecting a label that applies encryption, provide a sublabel alternative when users need a label with the same classification, but no encryption. Such as:
    - **Confidential \ All Employees**
    - **Confidential \ Anyone (no encryption)**

- Consider disabling IRM settings to prevent users from selecting them:
    - Outlook for Windows: 
        - Registry keys (DWORD:00000001) *DisableDNF* and *DisableEO* from HKEY_CURRENT_USER\Software\Microsoft\Office\16.0\Common\DRM
        - Make sure that the Group Policy setting **Configure default encryption option for the Encrypt button** isn't configured
    - Outlook for Mac: 
        - Keys *DisableEncryptOnly* and *DisableDoNotForward* security settings documented in [Set preferences for Outlook for Mac](/DeployOffice/mac/preferences-outlook)
    - Outlook on the web: 
        - Parameters *SimplifiedClientAccessDoNotForwardDisabled* and *SimplifiedClientAccessEncryptOnlyDisabled* documented for [Set-IRMConfiguration](/powershell/module/exchange/set-irmconfiguration)
    - Outlook for iOS and Android: These apps don't support users applying encryption without labels, so nothing to disable.

> [!NOTE]
> If users manually remove encryption from a labeled document that's stored in SharePoint or OneDrive and you've [enabled sensitivity labels for Office files in SharePoint and OneDrive](sensitivity-labels-sharepoint-onedrive-files.md), the label encryption will be automatically restored the next time the document is accessed or downloaded. 


## Apply sensitivity labels to files, emails, and attachments

Users can apply just one label at a time for each document or email.

When you label an email message that has attachments, the attachments inherit the label only if the label that you apply to the email message applies encryption and the attachment is an Office document isn't already encrypted. Because the inherited label applies encryption, the attachment becomes newly encrypted.

An attachment doesn't inherit the labels from the email message when the label applied to the email message doesn't apply encryption or the attachment is already encrypted.

Examples of label inheritance, where the label **Confidential** applies encryption and the label **General** doesn't apply encryption:

- A user creates a new email message and applies the **Confidential** label to this message. They then add a Word document that isn't labeled or encrypted. As a result of inheritance, the document is newly labeled **Confidential** and now has encryption applied from that label.

- A user creates a new email message and applies the **Confidential** label to this message. They then add a Word document that is labeled **General** and this file isn't encrypted. As a result of inheritance, the document gets relabeled as **Confidential** and now has encryption applied from that label.

## Sensitivity label compatibility

**With RMS-enlightened apps**: If you open a labeled and encrypted document or email in an [RMS-enlightened application](/azure/information-protection/requirements-applications#rms-enlightened-applications) that doesn't support sensitivity labels, the app still enforces encryption and rights management.

**With the Azure Information Protection client**: You can view and change sensitivity labels that you apply to documents and emails with the Office built-in labeling client by using the Azure Information Protection client, and the other way around.

**With other versions of Office**: Any authorized user can open labeled documents and emails in other versions of Office. However, you can only view or change the label in supported Office versions or by using the Azure Information Protection client. Supported Office app versions are listed in the [previous section](#support-for-sensitivity-label-capabilities-in-apps).

## Support for SharePoint and OneDrive files protected by sensitivity labels

To use the Office built-in labeling client with Office on the web for documents in SharePoint or OneDrive, make sure you've [enabled sensitivity labels for Office files in SharePoint and OneDrive](sensitivity-labels-sharepoint-onedrive-files.md).

## Support for external users and labeled content

When you label a document or email, the label is stored as metadata that includes your tenant and a label GUID. When a labeled document or email is opened by an Office app that supports sensitivity labels, this metadata is read and only if the user belongs to the same tenant, the label displays in their app. For example, for built-in labeling for Word, PowerPoint, and Excel, the label name displays on the status bar. 

This means that if you share documents with another organization that uses different label names, each organization can apply and see their own label applied to the document. However, the following elements from an applied label are visible to users outside your organization:

- Content markings. When a label applies a header, footer, or watermark, these are added directly to the content and remain visible until somebody modifies or deletes them.

- The name and description of the underlying protection template from a label that applied encryption. This information displays in a message bar at the top of the document, to provide information about who is authorized to open the document, and their usage rights for that document.

### Sharing encrypted documents with external users

In addition to restricting access to users in your own organization, you can extend access to any other user who has an account in Azure Active Directory. However, if your organization uses Conditional Access policies, see the [next section](#conditional-access-policies) for additional considerations.

All Office apps and other [RMS-enlightened application](/azure/information-protection/requirements-applications#rms-enlightened-applications) can open encrypted documents after the user has successfully authenticated. 

If external users do not have an account in Azure Active Directory, they can authenticate by using guest accounts in your tenant. These guest accounts can also be used to access shared documents in SharePoint or OneDrive when you have [enabled sensitivity labels for Office files in SharePoint and OneDrive](sensitivity-labels-sharepoint-onedrive-files.md):

- One option is to create these guest accounts yourself. You can specify any email address that these users already use. For example, their Gmail address.
    
    The advantage of this option is that you can restrict access and rights to specific users by specifying their email address in the encryption settings. The downside is the administration overhead for the account creation and coordination with the label configuration.

- Another option is to use [SharePoint and OneDrive integration with Azure AD B2B](/sharepoint/sharepoint-azureb2b-integration) so that guest accounts are automatically created when your users share links.
    
    The advantage of this option is minimum administrative overhead because the accounts are created automatically, and simpler label configuration. For this scenario, you must select the encryption option [Add any authenticated user](encryption-sensitivity-labels.md#requirements-and-limitations-for-add-any-authenticated-users) because you won't know the email addresses in advance. The downside is that this setting doesn't let you restrict access and usage rights to specific users.

External users can also use a Microsoft account to open encrypted documents when they use Windows and Microsoft 365 Apps ([formerly Office 365 apps](/deployoffice/name-change)) or the standalone edition of Office 2019. More recently supported for other platforms, Microsoft accounts are also supported for opening encrypted documents on macOS (Microsoft 365 Apps, version 16.42+), Android (version 16.0.13029+), and iOS (version 2.42+). For example, a user in your organization shares an encrypted document with a user outside your organization, and the encryption settings specify a Gmail email address for the external user. This external user can create their own Microsoft account that uses their Gmail email address. Then, after signing in with this account, they can open the document and edit it, according to the usage restrictions specified for them. For a walkthrough example of this scenario, see [Opening and editing the protected document](/azure/information-protection/secure-collaboration-documents#opening-and-editing-the-protected-document).

> [!NOTE]
> The email address for the Microsoft account must match the email address that's specified to restrict access for the encryption settings.

When a user with a Microsoft account opens an encrypted document in this way, it automatically creates a guest account for the tenant if a guest account with the same name doesn't already exist. When the guest account exists, it can then be used to open documents in SharePoint and OneDrive by using Office on the web, in addition to opening encrypted documents from the supported desktop and mobile Office apps.

However, the automatic guest account is not created immediately in this scenario, because of replication latency. If you specify personal email addresses as part of your label encryption settings, we recommend that you create corresponding guest accounts in Azure Active Directory. Then let these users know that they must use this account to open an encrypted document from your organization.

> [!TIP]
> Because you can't be sure that external users will be using a supported Office client app, sharing links from SharePoint and OneDrive after creating guest accounts (for specific users) or when you use [SharePoint and OneDrive integration with Azure AD B2B](/sharepoint/sharepoint-azureb2b-integration-preview) (for any authenticated user) is a more reliable method to support secure collaboration with external users.

### Conditional Access policies

If your organization has implemented [Azure Active Directory Conditional Access policies](/azure/active-directory/conditional-access/overview), check the configuration of those policies. If the policies include **Microsoft Azure Information Protection** and the policy extends to external users, those external users must have a guest account in your tenant even if they have an Azure AD account in their own tenant.

Without this guest account, they can't open the encrypted document and see an error message. The message text might inform them that their account needs to be added as an external user in the tenant, with the incorrect instruction for this scenario to **Sign out and sign in again with a different Azure Active Directory user account**.

If you can't create and configure guest accounts in your tenant for external users who need to open documents that are encrypted by your labels, you must either remove Azure Information Protection from the Conditional Access policies, or exclude external users from the policies.

For more information about Conditional Access and Azure Information Protection, the encryption service used by sensitivity labels, see the frequently asked question, [I see Azure Information Protection is listed as an available cloud app for conditional access—how does this work?](/azure/information-protection/faqs#i-see-azure-information-protection-is-listed-as-an-available-cloud-app-for-conditional-accesshow-does-this-work)

## When Office apps apply content marking and encryption

Office apps apply content marking and encryption with a sensitivity label differently, depending on the app you use.

| App | Content marking | Encryption |
| --- | --- | --- |
| Word, Excel, PowerPoint on all platforms | Immediately | Immediately |
| Outlook for PC and Mac | After Exchange Online sends the email | Immediately |
| Outlook on the web, iOS, and Android | After Exchange Online sends the email | After Exchange Online sends the email |
|

Solutions that apply sensitivity labels to files outside Office apps do so by applying labeling metadata to the file. In this scenario, content marking from the label's configuration isn't inserted into the file but encryption is applied. 

When those files are opened in an Office desktop app, the content markings are automatically applied by the Azure Information Protection unified labeling client when the file is first saved. The content markings are not automatically applied when you use built-in labeling for desktop, mobile, or web apps.

Scenarios that include applying a sensitivity label outside Office apps include:

- The scanner, File Explorer, and PowerShell from the Azure Information Protection unified labeling client 

- Auto-labeling policies for SharePoint and OneDrive

- Exported labeled and encrypted data from Power BI

- Microsoft Defender for Cloud Apps

For these scenarios, using their Office apps, a user with built-in labeling can apply the label's content markings by temporarily removing or replacing the current label and then reapplying the original label.

### Dynamic markings with variables

> [!IMPORTANT]
> Currently, not all apps on all platforms support dynamic content markings that you can specify for your headers, footers, and watermarks. For apps that don't support this capability, they apply the markings as the original text specified in the label configuration, rather than resolving the variables.
> 
> The Azure Information Protection unified labeling client supports dynamic markings. For labeling built in to Office, see the tables in the [capabilities](#support-for-sensitivity-label-capabilities-in-apps) section on this page for minimum versions supported.

When you configure a sensitivity label for content markings, you can use the following variables in the text string for your header, footer, or watermark:

| Variable | Description | Example when label applied |
| -------- | ----------- | ------- |
| `${Item.Label}` | Label display name of the label applied | **General**|
| `${Item.Name}` | File name or email subject of the content being labeled | **Sales.docx** |
| `${Item.Location}` | Path and file name of the document being labeled, or the email subject for an email being labeled | **\\\Sales\2020\Q3\Report.docx**|
| `${User.Name}` | Display name of the user applying the label | **Richard Simone** |
| `${User.PrincipalName}` | Azure AD user principal name (UPN) of the user applying the label | **rsimone\@contoso.com** |
| `${Event.DateTime}` | Date and time when the content is labeled, in the local time zone of the user applying the label in Microsoft 365 apps, or UTC (Coordinated Universal Time) for Office Online and auto-labeling policies | **8/10/2020 1:30 PM** |

> [!NOTE]
> The syntax for these variables is case-sensitive.

#### Setting different visual markings for Word, Excel, PowerPoint, and Outlook

As an additional variable, you can configure visual markings per Office application type by using an "If.App" variable statement in the text string, and identify the application type by using the values **Word**, **Excel**, **PowerPoint**, or **Outlook**. You can also abbreviate these values, which is necessary if you want to specify more than one in the same If.App statement.

Use the following syntax:

```
${If.App.<application type>}<your visual markings text> ${If.End}
```

As with the other dynamic visual markings, the syntax is case-sensitive, which includes the abbreviations for each application type (WEPO).

Examples:

- **Set header text for Word documents only:**

    `${If.App.Word}This Word document is sensitive ${If.End}`

    In Word document headers only, the label applies the header text "This Word document is sensitive". No header text is applied to other Office applications.

- **Set footer text for Word, Excel, and Outlook, and different footer text for PowerPoint:**

    `${If.App.WXO}This content is confidential. ${If.End}${If.App.PowerPoint}This presentation is confidential. ${If.End}`

    In Word, Excel, and Outlook, the label applies the footer text "This content is confidential." In PowerPoint, the label applies the footer text "This presentation is confidential."

- **Set specific watermark text for Word and PowerPoint, and then watermark text for Word, Excel, and PowerPoint:**

    `${If.App.WP}This content is ${If.End}Confidential`

    In Word and PowerPoint, the label applies the watermark text "This content is Confidential". In Excel, the label applies the watermark text "Confidential". In Outlook, the label doesn't apply any watermark text because watermarks as visual markings are not supported for Outlook.

## Require users to apply a label to their email and documents

> [!IMPORTANT]
> 
> The [Azure Information Protection unified labeling client](/azure/information-protection/rms-client/install-unifiedlabelingclient-app) supports this configuration that's also known as mandatory labeling. For labeling built in to Office apps, see the tables in the [capabilities](#support-for-sensitivity-label-capabilities-in-apps) section on this page for minimum versions.
>
> To use mandatory labeling for documents but not emails, see the instructions in the next section that explains how to configure Outlook-specific options.
> 
> To use mandatory labeling for Power BI, see [Mandatory label policy for Power BI](/power-bi/admin/service-security-sensitivity-label-mandatory-label-policy).

When the policy setting **Require users to apply a label to their email and documents** is selected, users assigned the policy must select and apply a sensitivity label under the following scenarios:

- For the Azure Information Protection unified labeling client:
    - For documents (Word, Excel, PowerPoint): When an unlabeled document is saved or users close the document.
    - For emails (Outlook): At the time users send an unlabeled message.

- For labeling built in to Office apps:
    - For documents (Word, Excel, PowerPoint): When an unlabeled document is opened or saved.
    - For emails (Outlook): At the time users send an unlabeled email message.

Additional information for built-in labeling:

- When users are prompted to add a sensitivity label because they open an unlabeled document, they can add a label or choose to open the document in read-only mode.

- When mandatory labeling is in effect, users can't remove sensitivity labels from documents, but can change an existing label.

For guidance about when to use this setting, see the information about [policy settings](sensitivity-labels.md#what-label-policies-can-do).

> [!NOTE]
> If you use the default label policy setting for documents and emails in addition to mandatory labeling: 
>
> The default label always takes priority over mandatory labeling. However, for documents, the Azure Information Protection unified labeling client applies the default label to all unlabeled documents whereas built-in labeling applies the default label to new documents and not to existing documents that are unlabeled. This difference in behavior means that when you use mandatory labeling with the default label setting, users will probably be prompted to apply a sensitivity label more often when they use built-in labeling than when they use the Azure Information Protection unified labeling client.
> 
> Now rolling out: Office apps that use built-in labeling and support a default label for existing documents. For details, see the [capabilities table](sensitivity-labels-office-apps.md#sensitivity-label-capabilities-in-word-excel-and-powerpoint) for Word, Excel, and PowerPoint.

## Outlook-specific options for default label and mandatory labeling

For built-in labeling, identify the minimum versions of Outlook that support these features by using the [capabilities table for Outlook](#sensitivity-label-capabilities-in-outlook) on this page, and the row **Different settings for default label and mandatory labeling**. All versions of the Azure Information Protection unified labeling client support these Outlook-specific options.

When the Outlook app supports a default label setting that's different from the default label setting for documents:

- In the label policy wizard, on the **Apply a default label to emails** page, you can specify your choice of sensitivity label that will be applied to all unlabeled emails, or no default label. This setting is independent from the **Apply this label by default to documents** setting on the previous **Policy settings for documents** page of the wizard.

When the Outlook app doesn't support a default label setting that's different from the default label setting for documents: Outlook will always use the value you specify for **Apply this label by default to documents** on the **Policy settings for documents** page of the label policy wizard.

When the Outlook app supports turning off mandatory labeling:

- In the label policy wizard, on the **Policy settings** page, select **Require users to apply a label to their email or documents**. Then select **Next** > **Next** and clear the checkbox **Require users to apply a label to their emails**. Keep the checkbox selected if you want mandatory labeling to apply to emails as well as to documents.

When the Outlook app doesn't support turning off mandatory labeling: If you select **Require users to apply a label to their email or documents** as a policy setting, Outlook will always prompt users to select a label for unlabeled emails.

> [!NOTE]
> If you have configured the PowerShell advanced settings **OutlookDefaultLabel** and **DisableMandatoryInOutlook** by using the [Set-LabelPolicy](/powershell/module/exchange/set-labelpolicy) or [New-LabelPolicy](/powershell/module/exchange/new-labelpolicy) cmdlets:
> 
> Your chosen values for these PowerShell settings are reflected in the label policy wizard and automatically work for Outlook apps that support these settings. The other PowerShell advanced settings remain supported for the Azure Information Protection unified labeling client only.

## End-user documentation

- [Apply sensitivity labels to your files and email in Office](https://support.microsoft.com/en-us/office/apply-sensitivity-labels-to-your-files-and-email-in-office-2f96e7cd-d5a4-403b-8bd7-4cc636bae0f9)
    - [Known issues with sensitivity labels in Office](https://support.microsoft.com/en-us/office/known-issues-with-sensitivity-labels-in-office-b169d687-2bbd-4e21-a440-7da1b2743edc)

- [Automatically apply or recommend sensitivity labels to your files and emails in Office](https://support.office.com/article/automatically-apply-or-recommend-sensitivity-labels-to-your-files-and-emails-in-office-622e0d9c-f38c-470a-bcdb-9e90b24d71a1)
    - [Known issues with automatically applying or recommending sensitivity labels](https://support.office.com/article/known-issues-with-automatically-applying-or-recommending-sensitivity-labels-451698ae-311b-4d28-83aa-a839a66f6efc)
