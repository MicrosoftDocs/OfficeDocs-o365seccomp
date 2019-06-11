---
title: "Threat Explorer (and real-time detections)"
ms.reviewer: 
ms.author: deniseb
author: denisebmsft
manager: laurawi
ms.date: 05/22/2019
audience: ITPro
ms.topic: article
ms.service: O365-seccomp
localization_priority: Normal
search.appverid:
- MET150
- MOE150
ms.assetid: 82ac9922-939c-41be-9c8a-7c75b0a4e27d
ms.collection: 
- M365-security-compliance
description: "Learn about Explorer (and real-time detections) in the Security &amp; Compliance Center."
---

# Threat Explorer (and real-time detections)

If your organization has [Office 365 Advanced Threat Protection](office-365-atp.md) (Office 365 ATP), and you have the [necessary permissions](#required-licenses-and-permissions), you have either **Explorer** or **real-time detections** (formerly *real-time reports* — [see what's new](#new-features-in-real-time-detections)!). In the Security & Compliance Center, go to **Threat management**, and then choose **Explorer** OR **Real-time detections**. 

|With ATP Plan 2, you see:  |With ATP Plan 1, you see:  |
|---------|---------|
|![Threat explorer](media/threatmgmt-explorer.png)      |![Real-time detections](media/threatmgmt-realtimedetections.png)         |

With Explorer (or real-time detections), you have a powerful report that enables your Security Operations team to investigate and respond to threats effectively and efficiently, and it resembles the following image: 

![Go to Threat management \> Explorer](media/cab32fa2-66f1-4ad5-bc1d-2bac4dbeb48c.png)

With this report, you can:
- [See malware detected by Office 365 security features](#see-malware-detected-in-email-by-technology)
- [View data about phishing URLs and click verdict](#view-data-about-phishing-urls-and-click-verdict)
- [Start an automated investigation and response process from a view in Explorer](#start-automated-investigation-and-response) (ATP Plan 2 only)
- ... [Investigate malicious email, and more](#more-ways-to-use-explorer-or-real-time-detections)!

## New features in real-time detections

For Office 365 ATP Plan 1 customers, the *real-time detections* report was previously referred to as *real-time reports*. In addition to the name change, several new features and enhancements are rolling out:

- In the Phish view, you can see more details about detected URLs through [ATP Safe Links](atp-safe-links.md). New details and capabilities include:
  - URLs in email messages
  - Filtering based on URL information
  - URL information displayed in data graphs
  - Time-of-click data about clicks in messages

- Whenever there's a change in a URL click verdict, you'll see an alert. URL click verdicts can change when a URL’s reputation changes post-detonation, or when a user who's protected by ATP Safe Links overrides an [ATP Safe Links warning](atp-safe-links-warning-pages.md).  
 
These enhancements enable your organization's security administrators to view more details than before. Security administrators can view information about URL domains, missed URLs, click verdicts, and more, and then adjust Office 365 ATP policies appropriately.

> [!NOTE]
> While these features are in preview, URL data will be available for a limited number of days. 

## See malware detected in email by technology

Suppose you want to see malware detected in email, by Office 365 technology. To do this, use the [Email > Malware](threat-explorer-views.md#email--malware) view of Explorer (or real-time detections).

1. In the Security & Compliance Center ([https://protection.office.com](https://protection.office.com)), choose **Threat management** > **Explorer** (or **Real-time detections**). (This example uses Explorer.)

2. In the **View** menu, choose **Email** > **Malware**.<br/>![View menu for Explorer](media/ExplorerViewEmailMalwareMenu.png)<br/>

3. Click **Sender**, and then choose **Basic** > **Detection technology**.<br/>Your detection technologies are now available as filters for the report.<br/>![Malware detection technologies](media/ExplorerEmailMalwareDetectionTech.png)<br/> 

4. Select an option, and then click the **Refresh** button to apply that filter.<br/>![Selected detection technology](media/ExplorerEmailMalwareDetectionTechATP.png)<br/> 

The report refreshes to show the results malware detected in email, using the technology option you selected. From here, you can conduct further analysis.

## View data about phishing URLs and click verdict

Suppose that you want to see phishing attempts through URLs in email, including a list of URLs that were allowed, blocked, and overridden. Identifying URLs that were clicked requires [ATP Safe links](atp-safe-links.md) to be configured. Make sure that you have set up [ATP Safe Links policies](set-up-atp-safe-links-policies.md) for time-of-click protection and logging of click verdicts by ATP Safe Links. 

To review phish URLs in messages and clicks on URLs in phish messages, use the [Email > Phish](threat-explorer-views.md#email--phish) view of Explorer (or real-time detections).

1. In the Security & Compliance Center ([https://protection.office.com](https://protection.office.com)), choose **Threat management** > **Explorer** (or **Real-time detections**). (This example uses Explorer.)

2. In the **View** menu, choose **Email** > **Phish**.<br/>![View menu for Explorer](media/ExplorerViewEmailPhishMenu.png)<br/>

3. Click **Sender**, and then choose **URLs** > **Click verdict**.

4. Select one or more options, such as **Blocked** and **Block overridden**, and then click the **Refresh** button that is on the same line as the options to apply that filter. (Don't refresh your browser window.)<br/>![URLs and click verdicts](media/ThreatExplorerEmailPhishClickVerdictOptions.png)<br/>

    The report refreshes to show two different URL tables on the URL tab under the report:

   1. **Top URLs** are the URLs contained in the messages you have filtered down to, and the email delivery action counts for each URL. In the phish email view, this list typically will contain legitimate URLs. Attackers include a mix of good and bad URLs in their messages to try to get them delivered, but they will make the malicious links more interesting for the user to click. The table of URLs is sorted by total email count (NOTE: This column is not shown to simplify the view).

   2. **Top clicks** are the Safe Links wrapped URLs that were clicked, sorted by total click count (this column is also not shown to simplify the view). Total counts by column indicate the Safe Links click verdict count for each clicked URL. In the phish email view, these are more often suspicious or malicious URLs, but could include clean URLs that are in phish messages. URL clicks on unwrapped links will not show up here.
   
   The two URLs tables show top URLs in phishing emails by delivery action and location, and they show URL clicks that were blocked (or visited despite a warning) so that you can understand what potential bad links were received by users and interacted with by users. From here, you can conduct further analysis. For example, below the chart, you can see the top URLs in emails that were blocked in your organization's environment.
   
   ![Explorer URLs that were blocked](media/ExplorerPhishClickVerdictURLs.png)
   
   Select a URL to view more detailed information. Note that in the URL flyout dialog, the filtering on emails is removed to show you the full view of the URL's exposure in your environment. This lets you filter down emails in Explorer to ones you are concerned about, find specific URLs that are potential threats, then expand your understanding of the URL exposure in your environment (via the URL details dialog) without having to add URL filters to the Explorer view itself.

## Review email messages reported by users

Suppose that you want to see email messages that users in your organization have reported as Junk, Not Junk, or Phishing by using the [Report Message add-in for Outlook and Outlook on the web](enable-the-report-message-add-in.md). To do this, use the [Email > User-reported](threat-explorer-views.md#email--user-reported) view of Explorer (or real-time detections).

1. In the Security & Compliance Center ([https://protection.office.com](https://protection.office.com)), choose **Threat management** > **Explorer** (or **Real-time detections**). (This example uses Explorer.)

2. In the **View** menu, choose **Email** > **User-reported**.<br/>![View menu for Explorer](media/ExplorerViewMenuEmailUserReported.png)<br/>

3. Click **Sender**, and then choose **Basic** > **Report type**.

4. Select an option, such as **Phish**, and then click the **Refresh** button. <br/>![User-reported phish](media/EmailUserReportedReportType.png)<br/> 

The report refreshes to show data about email messages that people in your organization have reported as a phishing attempt. You can use this information to conduct further analysis, and if necessary, adjust your [ATP anti-phishing policies](set-up-anti-phishing-policies.md).

## Start automated investigation and response

> [!NOTE]
> Automated investigation and response capabilities are available in **Office 365 ATP Plan 2** and **Office 365 E5**.

(NEW!) [Automated investigation and response](automated-investigation-response-office.md) can save your security operations team much time and effort in investigating and mitigating cyber attacks. In addition to configuring alerts that can trigger a security playbook, you can start an automated investigation and response process from a view in Explorer. 

For details on this, see [Example: A security administrator triggers an investigation from Explorer](automated-investigation-response-office.md#example-a-security-administrator-triggers-an-investigation-from-threat-explorer).

## More ways to use Explorer (or real-time detections)

In addition to the scenarios outlined in this article, you have many more reporting options available with Explorer (or real-time detections). 
- [Find and investigate malicious email that was delivered](investigate-malicious-email-that-was-delivered.md)
- [View malicious files detected in SharePoint Online, OneDrive, and Microsoft Teams](malicious-files-detected-in-spo-odb-or-teams.md)
- [Get an overview of the views in Threat Explorer (and real-time detections)](threat-explorer-views.md)

## Required licenses and permissions

You must have [Office 365 ATP](office-365-atp.md) to get Explorer or real-time detections.
- Explorer is included in Office 365 ATP Plan 2. 
- The real-time detections report is included in Office 365 ATP Plan 1.

To view and use Explorer or real-time detections, you must have appropriate permissions, such as those granted to a security administrator or security reader. 

- For the Security &amp; Compliance Center, you must have one of the following roles assigned:
    - Organization Management
    - Security Administrator (this can be assigned in the Azure Active Directory admin center ([https://aad.portal.azure.com](https://aad.portal.azure.com)))
    - Security Reader

- For Exchange Online, you must have one of the following roles assigned in either the Exchange admin center ([https://outlook.office365.com/ecp](https://outlook.office365.com/ecp)) or with PowerShell cmdlets (See [Exchange Online PowerShell](https://docs.microsoft.com/powershell/exchange/exchange-online/exchange-online-powershell?view=exchange-ps)):
    - Organization Management
    - View-only Organization Management
    - View-Only Recipients role
    - Compliance Management

To learn more about roles and permissions, see the following resources:

- [Permissions in the Office 365 Security &amp; Compliance Center](permissions-in-the-security-and-compliance-center.md)
- [Feature permissions in Exchange Online](https://docs.microsoft.com/exchange/permissions-exo/feature-permissions)
  
