---
title: "Install the Junk Email Reporting Add-in for Microsoft Outlook"
ms.author: MSFTTracyP
author: tracyp
manager: dansimp
ms.date: 12/9/2016
audience: ITPro
ms.topic: article
ms.service: O365-seccomp
localization_priority: Normal
ms.assetid: 8dcc752f-e22e-44ce-a104-4cc4d7e439f3
ms.collection:
- M365-security-compliance
description: "In this articleSupported LanguagesInstall the Junk Email Reporting Add-inUninstall the Junk Email Reporting Add-inFor more information"
---

# Install the Junk Email Reporting Add-in for Microsoft Outlook
  
This topic describes how to install (and uninstall) the Microsoft Junk Email Reporting Add-in for Outlook on client computers in your organization. The current version of the add-in (January 2016) includes support for Outlook 2016, Outlook 2013, Outlook 2010, and Outlook 2007. 
  
The add-in (for all supported languages) allows you to report junk email directly from the Outlook ribbon. The English version of the add-in includes additional options for reporting email issues to Microsoft, directly from the ribbon:
  
-  Report phishing scam emails that you receive 
    
- Report email incorrectly identified as junk mail.
    
## Supported Languages
<a name="sectionSection0"> </a>

The Junk Email Reporting Add-in supports the following languages: 
  
- Simplified Chinese
    
- Traditional Chinese
    
- Dutch
    
- English
    
- French
    
- German
    
- Italian
    
- Japanese
    
- Korean
    
- Portuguese
    
- Portuguese (Brazil)
    
- Spanish
    
## Install the Junk Email Reporting Add-in
<a name="sectionSection1"> </a>

You can install the Junk Email Reporting Add-in:
  
- By running the Windows Installer package as you would any other .msi file. When you install the add-in, a GUI interface opens and prompts you through the installation screens. For more information, see [Install the Junk Email Reporting Add-In using the Setup wizard](install-the-junk-email-reporting-add-in-for-microsoft-outlook.md#BKMK_InstalltheJunkEmailReportingAdd-InUsingtheSetupWizard). OR
    
- By running a silent installation which suppresses the installation user interface. Instead, you specify command-line options which run an installation script. When you install the add-in, additional configuration options are available which are not available through the GUI interface. For more information, see [Install the Junk Email Reporting Add-In using Silent Mode](install-the-junk-email-reporting-add-in-for-microsoft-outlook.md#BKMK_InstalltheJunkEmailReportingAdd-IninSilentMode).
    
### What do you need to know before you begin?

Installation of the Microsoft Junk Email Reporting Add-in for Microsoft Outlook requires:
  
- One of the following operating systems: Windows 10, Windows 8.1, Windows 8, Windows 7 Service Pack 1, Windows 10 Server, Windows Server 2012 R2, Windows Server 2012, or Windows Server 2008 R2
    
- Outlook 2016, Outlook 2013, Outlook 2010, or Outlook 2007 (Service Pack 2 or higher)
    
- Microsoft Office Primary Interop Assemblies: 
    
  - To download the Primary Interop Assemblies for Microsoft Office 2010 or higher, go to the [Microsoft Download Center](https://go.microsoft.com/fwlink/?LinkID=166026).
    
  - To download the Primary Interop Assemblies for Microsoft Office 2007, go to the [Microsoft Download Center](https://go.microsoft.com/fwlink/?LinkId=72637).
    
- Microsoft .NET Framework [Version 2.0](https://go.microsoft.com/fwlink/?LinkID=208706).
    
> [!NOTE]
> You must have administrator privileges on the computer on which you are installing the add-in. 
  
### Install the Junk Email Reporting Add-In using the Setup wizard
<a name="BKMK_InstalltheJunkEmailReportingAdd-InUsingtheSetupWizard"> </a>

1. On your computer, close Outlook.
    
2. Go to the Microsoft Download Center page for the Microsoft Junk E-mail Reporting Add-In for Microsoft Outlook [https://go.microsoft.com/fwlink/?LinkID=147248](https://go.microsoft.com/fwlink/?LinkID=147248) and download the .msi file. 
    
3. Double-click the .msi file. 
    
4. On the **Welcome to Microsoft Junk Email Reporting Add-in Setup** page, click **Next**. 
    
5. Review the license agreement, and then click **I accept the terms in the License Agreement** if you agree to the terms of installation (required to continue installation). Click **Next** to continue. 
    
6. When the wizard is complete, click **Finish**. 
    
7. Start Outlook.
    
8. Look for the **Junk** button on your Outlook ribbon. You can now report junk email messages to Microsoft by selecting the junk email messages in your Inbox and clicking the **Report Junk** button. 
    
9. Choose the down arrow next to **Junk** for more options such as **Report as Phishing** if you want to report phishing scam emails to Microsoft. In your junk mail folder, you can also select, **Report not junk** if an email was incorrectly identified as junk mail. 
    
### Install the Junk Email Reporting Add-In using Silent Mode
<a name="BKMK_InstalltheJunkEmailReportingAdd-IninSilentMode"> </a>

1. On your computer, close Outlook.
    
2. Open a command prompt.
    
3. If you want to perform a straight installation of the add-in, without any optional parameters, specify the following:
    
  - Computers running x86 Outlook:  `msiexec /qn /i JunkReportingAdd-in.x86-en.msi`
    
  - Computers running x64 Outlook:  `msiexec /qn /i JunkReportingAdd-in.x64-en.msi`
    
    You can also specify the optional MaxMessageSelection and BccEmailAddress parameters:
    
  - MaxMessageSelection Allows administrators to define the maximum number of messages that can be selected by users for submission in a single click. The range is 1 to 50 messages, and the default value is 10 messages.
    
    Example: If you want to set the maximum number of messages that can be selected by users for submission in a single click to 16, use the following option as part of the installation command:  `MaxMessageSelection=16`
    
  - BccEmailAddress Allows Administrators to set up a mailbox to receive a copy of all their user submissions by setting a Bcc email address. When the mailbox is set up, a copy of all submitted emails will be sent to the BccEmailAddress. Otherwise, the default setting is no Bcc email address.
    
    Example: If you want to use junkReports@contoso.com as the Bcc email address for all submissions, use the following command:  `BccEmailAddress="junkReports@contoso.com"`
    
    > [!NOTE]
    > You can set multiple Bcc email addresses by entering them with a semicolon delimiter. Example:  `BccEmailAddress="junkReports@contoso.com; hollyd@treyresearch.net"`
  
    To add both of these optional parameters based on the above examples, you would specify the following for a computer running x86 Outlook: 
    
  ```
  msiexec /qn /i JunkReportingAdd-in.x86-en.msi. MaxMessageSelection=16 BccEmailAddress="junkReports@contoso.com; hollyd@treyresearch.net"
  ```

4. After the installation is complete, start Outlook.
    
5. Look for the **Junk** button on your Outlook ribbon. You can now report junk email messages to Microsoft by selecting the junk email messages in your Inbox and clicking the **Report Junk** button. 
    
6. Choose the down arrow next to **Junk** for more options such as **Report as Phishing** if you want to report phishing scam emails to Microsoft. In your junk mail folder, you can also select, **Report not junk** if an email was incorrectly identified as junk mail. 
    
## Uninstall the Junk Email Reporting Add-in
<a name="sectionSection2"> </a>

Use one of these options to uninstall the Junk Email Reporting Add-in:
  
- Remove the add-in using Windows Control Panel. For more information, see [Uninstall the Junk Email Reporting Add-in from Control Panel](install-the-junk-email-reporting-add-in-for-microsoft-outlook.md#BKMK_UninstalltheJunkEmailReportingAdd-infromControlPanel). OR
    
- Run the Windows installer package and select the uninstall option. For more information, see [Uninstall the Junk Email Reporting Add-in by Running the Windows Installer Package](install-the-junk-email-reporting-add-in-for-microsoft-outlook.md#BKMK_UninstalltheJunkEmailReportingAddinbyRunningtheWindowsInstallerPackage).OR
    
- Run a silent installation using the uninstall option. For more information, see [Uninstall the Junk Email Reporting Add-in in Silent Mode](install-the-junk-email-reporting-add-in-for-microsoft-outlook.md#MK_UninstalltheJunkEmailReportingAdd-ininSilentMode).
    
> [!NOTE]
> You must have administrator privileges on the computer on which you are uninstalling the add-in. 
  
### Uninstall the Junk Email Reporting Add-in from Control Panel
<a name="BKMK_UninstalltheJunkEmailReportingAdd-infromControlPanel"> </a>

1. On your computer, close Outlook.
    
2. From the Start menu on your computer, select **Control Panel**.
    
3. Select **Programs and Features**.
    
4. Select **Microsoft Junk E-mail Reporting Add-In for Microsoft Office Outlook**.
    
5. Select **Uninstall**.
    
6. Start Outlook again to confirm that the add-in is no longer displayed on your Outlook ribbon.
    
### Uninstall the Junk Email Reporting Add-in by Running the Windows Installer Package
<a name="BKMK_UninstalltheJunkEmailReportingAddinbyRunningtheWindowsInstallerPackage"> </a>

1. On your computer, close Outlook.
    
    > [!NOTE]
    > If Outlook is running during the uninstall process, it will need to be restarted in order for the add-in to be completely uninstalled. 
  
2. Re-run the .msi file you previously ran to install the add-in. 
    
    (Go to the Microsoft Download Center page for the Microsoft Junk E-mail Reporting Add-In for Microsoft Outlook [https://go.microsoft.com/fwlink/?LinkId=147248](https://go.microsoft.com/fwlink/?LinkId=147248), download the .msi file, and then double-click the .msi file.) 
    
3. Follow the prompts to uninstall the add-in.
    
4. Start Outlook again to confirm that the add-in is no longer displayed on your Outlook ribbon.
    
### Uninstall the Junk Email Reporting Add-in in Silent Mode
<a name="MK_UninstalltheJunkEmailReportingAdd-ininSilentMode"> </a>

1. On your computer, close Outlook.
    
    > [!NOTE]
    > If Outlook is running during the uninstall process, it will need to be restarted in order for the add-in to be completely uninstalled. 
  
2. Open a command prompt.
    
3. Specify the following command line parameter:
    
    Computers running x86 Outlook:  `msiexec /x JunkReportingAdd-in.x86-en.msi /qn MSIRESTARTMANAGERCONTROL="DisableShutdown"`
    
    Computers running x64 Outlook:  `msiexec /x JunkReportingAdd-in.x64-en.msi /qn MSIRESTARTMANAGERCONTROL="DisableShutdown"`
    
4. Start Outlook again to confirm that the add-in is no longer displayed on your Outlook ribbon.
    
## For more information
<a name="sectionSection3"> </a>

[Report junk email messages to Microsoft](report-junk-email-messages-to-microsoft.md)
  
[Troubleshooting and support information](troubleshooting-and-support-information.md)
  

