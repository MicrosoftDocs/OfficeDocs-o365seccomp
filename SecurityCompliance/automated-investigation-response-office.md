---
title: "Automated Investigation and Response (AIR) with Office 365"
ms.author: deniseb
author: denisebmsft
manager: dansimp
ms.date: 06/25/2019
audience: ITPro
ms.topic: article
ms.service: O365-seccomp
localization_priority: Normal
search.appverid:
- MET150
- MOE150
ms.collection: M365-security-compliance
description: "Learn about Automated Investigation and Response capabilities in Office 365 Advanced Threat Protection."
---

# Automated Investigation and Response (AIR) with Office 365

Automated Investigation and Response (AIR) (currently in public preview as one of many [Office 365 Threat investigation and response capabilities](office-365-ti.md)) enables you to run automated investigation and remediation to well-known threats that exist today. Read this article to get an overview of AIR and how it can help your organization and security operations teams mitigate threats more effectively and efficiently. 

To learn more about when  AIR features will be available, see the [Microsoft 365 Roadmap](https://www.microsoft.com/microsoft-365/roadmap).

## Alerts

[Alerts](alert-policies.md#viewing-alerts) represent triggers for security operations team workflows for incident response. Prioritizing the right set of alerts for investigation, while making sure no threats are unaddressed is challenging. When investigations into alerts are performed manually, Security Operations teams must hunt and correlate entities (e.g. content, devices and users) at risk from threats. Such tasks and workflows are very time consuming and involve multiple tools and systems. With AIR, investigation and response are automated into key security and threat management alerts that trigger your security response playbooks automatically. 

In the initial release of AIR in April 2019, alerts generated from following single events alert policies will be auto-investigated. 

1. A potentially malicious URL click was detected
2. Email reported by user as phish*
3. Email messages containing malware removed after delivery*
4. Email messages containing phish URLs removed after delivery*

> [!NOTE]
> These alerts have been assigned an "Informational" severity in the respective alert policies within the Security & Compliance Center with email notifications turned off. These can be turned on through the Alert policy configuration.

To view alerts, in the Security & Compliance Center, choose **Alerts** > **View alerts**. Select an alert to view its details, and from there, use the **View investigation** link to go to the corresponding [investigation](#investigation-graph). Note that informational alerts are hidden in the alert view by default. To see them, you need to change the alert filtering to include informational alerts.

If your organization manages your security alerts through a alert management system, service management system, or Security Information and Event Management (SIEM) system, you can send Office 365 alerts to that system via either email notification or via the [Office 365 Management Activity API](https://docs.microsoft.com/office/office-365-management-api/office-365-management-activity-api-reference). The investigation alert notifications via email or API will include links to access the alerts in the Security & Compliance Center, enabling the assigned security administrator to navigate quickly to the investigation.

![Alerts that link to investigations](media/air-alerts-page-details.png) 


## Security playbooks

Security playbooks are back-end policies that are at the heart of automation in Microsoft Threat Protection. The security playbooks provided in AIR are based on common real-world security scenarios. A security playbook is launched automatically when an alert is triggered within your organization. Once the alert triggers, the associated playbook is run automatically. The playbook runs an investigation, looking at all the associated metadata (including email messages, users, subjects, senders, etc.). Based on the playbook's findings, AIR recommends a set of actions that your organization's security team can take to control and mitigate the threat. 

The security playbooks you'll get with AIR are designed to tackle the most frequent threats that organizations face today. They're based on input from Security Operations and Incident Response teams, including those who help defend Microsoft and our customers assets.

### Security playbooks are rolling out in phases

As part of AIR, security playbooks are rolling out in phases

- **Phase 1 (April 2019)**: Playbooks include recommendations for actions that security administrators review and approve. Phase 1 will include the following playbooks:
    - User-reported phish message
    - URL click verdict change 
    - Malware detected post-delivery (Malware ZAP)
    - Phish detected post-delivery ZAP (Phish ZAP)
    - Manual e-mail investigations (using Threat Explorer)

- **Phase 2 (second half of 2019)**: Several new playbooks and playbook improvements, plus the option for security administrators to configure security playbooks to take some actions automatically without administrative interaction. 

### Playbooks include investigation and recommendations

Each playbook includes: 
- a root investigation, 
- steps taken to identify and correlate other potential threats, and 
- recommended threat remediation actions.

Each high-level step includes many sub-steps that are executed to provide a deep, detailed, and exhaustive response to threats.

## Example: A user-reported phish message launches an investigation playbook

When a user in your organization submits an email message and reports it to Microsoft by using the [Report Message add-in for Outlook or Outlook Web Access](enable-the-report-message-add-in.md), the report is also sent to your system and is visible in Explorer in the User-reported view. This user-reported message now triggers a system-based informational alert, which automatically launches the investigation playbook.

During the root investigation phase, various aspects of the email are assessed. These include:
- A determination about what type of threat it might be;
- Who sent it;
- Where the email was sent from (sending infrastructure);
- Whether other instances of the email were delivered or blocked;
- An assessment from our analysts;
- Whether the email is associated with any known campaigns;
- and more.

After the root investigation is complete, the playbook provides a list of recommended actions to take on the original email and entities associated with it.
  
Next, several threat investigation and hunting steps are executed:

- Similar email messages in other email clusters are searched.
- The signal is shared with other platforms, such as [Microsoft Defender ATP](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection).
- A determination is made on whether any users have clicked through any malicious links in suspicious email messages.
- A check is done across Office 365 Exchange Online Protection ([EOP](eop/exchange-online-protection-eop.md)) and Office 365 Advanced Threat Protection ([ATP](office-365-atp.md)) to see if there are any other similar messages reported by users.
- A check is done to see if a user has been compromised. This check leverages signals across [Microsoft Cloud App Security](https://docs.microsoft.com/cloud-app-security) and [Azure Active Directory](https://docs.microsoft.com/azure/active-directory), correlating any related user activity anomalies. 

During the hunting phase, risks and threats are assigned to various hunting steps. 

Remediation is the final phase of the playbook. During this phase, remediation steps are taken, based on the investigation and hunting phases. 

## Example: A security administrator triggers an investigation from Threat Explorer

In addition to automatic investigations that are triggered by an alert, your organization's security operations team can trigger an automatic investigation from a view in [Threat Explorer](use-explorer-in-security-and-compliance.md).

For example, suppose that you are viewing data in Explorer about user-reported messages. You can select an item in the list of results, and then click **Investigate**.

![User-reported messages in Explorer with Investigate button](media/Explorer-UserReported-Investigate.png)

As another example, suppose you are viewing data about email messages detected as containing malware, and there are several email messages detected as containing malware. You can select the **Email** tab, select one or more email messages, and then, on the **Actions** menu, select **Investigate**. 

![Starting an investigation for malware in Explorer](media/Explorer-Malware-Email-ActionsInvestigate.png)

Similar to playbooks triggered by an alert, automatic investigations that are triggered from a view in Explorer include a root investigation, steps to identify and correlate threats, and recommended actions to mitigate those threats.

## Get started

To access your investigations, as an Office 365 global administrator, security administrator, or security reader, go to the Security & Compliance Center ([https://protection.office.com](https://protection.office.com)) and sign in. Then, do one of the following:

- In the left navigation, go to **Alerts** > **View alerts**, open one of the investigation related alerts, then click the **View investigation** link at the bottom of the alert flyout. 

    or

- In the left navigation, go to **Threat management** > **Investigations**.

    or

- Visit the Threat management dashboard (In the Security & Compliance Center, go to **Threat management** > **Dashboard**).

![AIR widgets](media/air-widgets.png)

Your AIR widgets will appear across the top of the [Security Dashboard](security-dashboard.md). Select a widget to get started.

You may also access an investigation directly from the related Alerts.

### Automated investigations

The automated investigations page shows your organization's investigations and their current states.

![Main investigation page for AIR](media/air-maininvestigationpage.png) 
  
You can:
- Navigate directly to an investigation (select an **Investigation ID**).
- Apply filters. Choose from **Investigation Type**, **Time range**, **Status**, or a combination of these.
- Export the data to a CSV file.

The investigation status indicates the progress of the analysis and actions. As the investigation runs, the status will change to indicate whether threats were found, as well as indicate whether actions have been approved. 
- **Starting**: The investigation is queued to begin soon
- **Running**: The investigation has started and is conducting its' analysis
- **No Threats Found**: The investigation has completed its' analysis and no threats were found
- **Terminated By System**: The investigation was not closed and expired after 7 days
- **Pending Action**: The investigation found threats with actions recommended
- **Threats Found**: The investigation found threats, but the threats do not have actions available within AIR
- **Remediated**: The investgation finished and was fully remediated (all actions were approved)
- **Partially Remediated**: The investigation finished and some of the recommended actions were approved
- **Terminated By User**: An admin terminated the investigation
- **Failed**: An error occurred during the investigation that prevented it from reaching a conclusion on threats
- **Queued By Throttling**: The investigation is waiting for analysis due to system processing limitations (to protect service performance)
- **Terminated By Throttling**: The investigation could not be completed in sufficient time due to investigation volume and system processing limitations. You can re-trigger the investigation by selecting the email in Explorer and selecting the Investigate action.

### Investigation graph

When you open a specific investigation, you see the investigation graph page. This page shows all the different entities: email messages, users (and their activities), and devices that were automatically investigated as part of the alert that was triggered.

![AIR investigation graph page](media/air-investigationgraphpage.png)

You can:
- Get a visual overview of the current investigation.
- View a summary of the investigation duration.
- Select a node in the visualization to view details for that node.
- Select a tab across the top to view details for that tab.

### Alert investigation

On the **Alerts** tab for an investigation, you can see alerts relevant to the investigation. Details include the alert that triggered the investigation and other alerts, such as risky sign-in, mass download, etc., that are correlated to the investigation. From this page, a security analyst can also view additional details on individual alerts.

![AIR alerts page](media/air-investigationalertspage.png)

You can:
- Get a visual overview of the current triggering alert and any associated alerts.
- Select an alert in the list to open a fly-out page that shows full alert details.

### Email investigation

On the **Email** tab for an investigation, you can see all the clusters of email identified as part of the investigation. 

Given the sheer volume of email that users in an organization send and receive, the process of 
- clustering email messages based on similar attributes from a message header, body, URL and attachments; 
- separating malicious email from the good email; and 
- taking action on malicious email messages 

can take many hours. AIR now automates this process, saving your organization's security team time and effort. 

Two different types of email clusters may be identified during the email analysis step: similarity clusters, and indicator clusters. 
- Similarity clusters are email messages that contain similar sender and content attributes. These clusters are evaluated for malicious content based on the original detection findings. Email clusters that contain enough malicious detections will be considered malicious.
- Indicator clusters are email messages that contain the same indicator entity (file hash or URL) from the original email. When the original file/URL entity is identified as malicious, AIR will apply the indicator verdict to the entire cluster of email messages containing that entity. As a file identified as malware will mean that the cluster of email messages containing that file will be treated as malware email messages.

The goal of clustering is to find other related email messages that are sent by the same sender as part of an attack or a campaign.

The **Email** tab will also show email items related to the investigation, such as the user-reported email details, the original email reported, the email message(s) zapped due to malware/phish, etc.

The email count identified on the email tab currently represents the sum total of all email messages shown on the **Email** tab. Since email messages will be present in multiple clusters, the actual total count of email messages identified (and affected by remediation actions) will be the count of unique email messages present across all of the clusters and original recipients' email messages. 

Both Explorer and AIR count email messages on a per recipient basis, since the security verdicts, actions, and delivery locations will vary on a per recipient basis. Thus an original email sent to three users will count as a total of three email messages instead of one email. Note there may be cases where an email gets counted two or more times, since the email may have multiple actions on it and there may be multiple copies of the email once all actions occur. For example a malware email that is detected at delivery may result in both a blocked (quarantined) email and a replaced email (threat file replaced with an warning file, then delivered to user's mailbox). Since there are literally two copies of the email in the system - these may both be counted in cluster counts. 

Email counts are calculated at the time of the investigation and some counts are re-calculated when you open investigation flyouts (based on an underlying query). The email counts shown for the email clusters on the email tab and the email quantity value shown on cluster flyout are calculated at the time of investigation. The email count shown at the bottom of the email tab of the cluster flyout, as well as the count of email messages shown in Explorer will reflect email messages received after the investigation's initial analysis. Thus an email cluster that shows an original quantity of 10 email messages would show an email list total of 15 when 5 more email messages arrive between the investigation analysis phase and when the admin reviews the investigation. Showing both counts in different views is done to indicate the email impact at the time of investigation and the current impact up until the time that remediation is run.

As an example, consider the following scenario. The first cluster of three email messages were deemed to be phish. Another cluster of similar messages with the same IP and subject was found and considered malicious, as some of them were identified as phish during initial detection. 

![AIR email investigation page](media/air-investigationemailpage.png)

You can:
- Get a visual overview of the current clustering results and threats found.
- Click a cluster entity or a threat list to open a fly-out page that shows the full alert details.
- Further investigate the email cluster by clicking the 'Open in Explorer' link at the top of the 'Email cluster details' tab

![AIR investigation email with flyout details](media/air-investigationemailpageflyoutdetails.png)

*Note: In the context of email, you may see a volume anomaly threat surface as part of the investigation. A volume anomaly indicates a spike in similar email messages around the investigation event time compared to earlier timeframes. This spike in email traffic with similar characteristics (e.g. subject and sender domain, body similarity and sender IP) is typical of the start of email campaigns or attacks. However, bulk, spam, and legitimate email campaigns commonly share these characteristics. Volume anomalies represent a potential threat, and accordingly could be less severe compared to malware or phish threats that are identified using anti-virus engines, detonation or malicious reputation.

### User investigation

On the **Users** tab, you can see all the users identified as part of the investigation. Users will appear in the investigation when there is an event or indication that the user may be affected or compromised.

For example, in the following image, AIR has identified indicators of compromise and anomalies based on a new inbox rule that was created. Additional details (evidence) of the investigation are available through detailed views within this tab. Indicators of compromise and anomalies may also include anomaly detections from [Microsoft Cloud App Security](https://docs.microsoft.com/cloud-app-security).

![AIR investigation users page](media/air-investigationuserspage.png)

You can:
- Get a visual overview of identified user results and risks found.
- Select a user to open a fly-out page that shows the full alert details.

### Machine investigation

On the **Machines** tab, you can see all the machines identified as part of the investigation. 

![AIR investigation machine page](media/air-investigationmachinepage.png)

As part of the investigation, AIR correlates email threats to devices. For example, an investigation passes a malicious file hash across to [Microsoft Defender ATP](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection
) to investigate. This allows for automated investigation of relevant machines for your users, to help ensure that threats are addressed both in the cloud and across your endpoints. 

You can:
- Get a visual overview of the current machines and threats found.
- Select a machine to open a view that into the related [Microsoft Defender ATP investigations](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/automated-investigations) in the Microsoft Defender Security Center.

### Entity investigation

On the **Entities** tab, you can see all the entities identified as part of the investigation. 

Here, you can see the investigated entities and details of the types of entities, such as email messages, clusters, IP addresses, users, and more. You can also see how many entities were analyzed, and the threats that were associated with each. 

![AIR investigation entities page](media/air-investigationentitiespage.png)

You can:
- Get a visual overview of the investigation entities and threats found.
- Select an entity to open a fly-out page that shows the related entity details.

![AIR investigation entities details](media/air-investigationsentitiespagedetails.png)

### Playbook log

On the **Log** tab, you can see all the playbook steps that have occurred during the investigation. The log captures a complete inventory of all actions completed by Office 365 auto-investigation capabilities as part of AIR. It provides a clear view of all the steps taken, including the action itself, a description, and the duration of the actual from start to finish. 

![AIR investigation log page](media/air-investigationlogpage.png)

You can:
- Get see a visual overview of the playbook steps taken.
- Export the results to a CSV file.
- Filter the view.

### Recommended actions

On the **Actions** tab, you can see all the playbook actions that are recommended for remediation after the investigation has completed. 

Actions capture the steps Microsoft recommends you take at the end of a investigation. You can take remediation actions here by selecting one or more actions. Clicking **Approve** will allow remediation to begin. (Appropriate permissions are needed - the 'Search And Purge' role is required to run actions from Explorer and AIR). For example, a Security Reader can view actions but not approve them. Note - you do not have to approve every action. If you do not agree with the recommended action or your organization does not choose certain types of actions - then you can either choose to **Reject** the actions or simply ignore them and take no action. Approving and/or rejecting all actions will let the investigation fully close, while leaving some actions incomplete will result in the investigation status changing to a partially remediated state.

![AIR investigations action page](media/air-investigationactionspage.png)

You can:
- Get a visual overview of the playbook-recommended actions.
- Select a single action or multiple actions.
- Approve or reject recommended actions with comments.
- Export the results to a CSV file.
- Filter the view.

## How to get AIR

Currently, Office 365 AIR features are in preview. When generally available, Office 365 AIR features will be included in the following subscriptions:

- Microsoft 365 Enterprise E5
- Office 365 Enterprise E5
- Microsoft Threat Protection
- Office 365 Advanced Threat Protection Plan 2

To learn more about feature availability, visit the [Microsoft 365 Roadmap](https://www.microsoft.com/microsoft-365/roadmap).
