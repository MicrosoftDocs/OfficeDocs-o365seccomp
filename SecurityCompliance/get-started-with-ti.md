---
title: "Get started with Office 365 Threat Investigation and Response"
ms.reviewer: 
ms.author: deniseb
author: denisebmsft
manager: laurawi
ms.date: 03/19/2019
audience: ITPro
ms.topic: article
ms.service: O365-seccomp
localization_priority: Normal
search.appverid:
- MET150
- MOE150
ms.assetid: 38e9b67f-d188-490f-bc91-a1ae4b270441
ms.collection:
- M365-security-compliance
description: "Learn about Office 365 Threat investigation and response and how to get started."
---

# Get started with Threat Investigation and Response (Office 365 Advanced Threat Protection Plan 2)

If you are part of your organization's security team, you can use Office 365 Threat Investigation and Response capabilities to protect your users from attacks. Office 365 Advanced Threat Protection Plan 2 (formerly Office 365 Threat Intelligence) helps security analysts and administrators keep users safe by bubbling up insights and identifying action based on what is happening in their your Office 365 environment. These insights are based on a comprehensive repository of threat intelligence data and systems to spot patterns that correspond to attack behaviors and suspicious activity.
  
Read this article to learn more about threat investigation and response, and how to get started.
  
## What are the Threat Investigation and Response capabilities included in Office 365?

Threat investigation and response capabilities help drive insights into threats and related response actions that are available in the Office 365 Security &amp; Compliance Center. These insights can help your organization's security team protect Office 365 users from email or file based attacks. The capabilities help monitor signals and gathers data from multiple sources, such as user activity, authentication, email, compromised PCs, and security incidents. Business decision makers and Office 365 global administrators, security administrators, and security analysts can all use this information to understand and respond to threats against Office 365 users and protect their intellectual property.

> [!IMPORTANT]
> Office 365 Threat Intelligence is now Office 365 Advanced Threat Protection Plan 2, along with additional threat protection capabilities. To learn more, see [Office 365 Advanced Threat Protection plans and pricing](https://products.office.com/exchange/advance-threat-protection) and the [Office 365 Advanced Threat Protection Service Description](https://docs.microsoft.com/office365/servicedescriptions/office-365-advanced-threat-protection-service-description).
  
## Get acquainted with the Threat dashboard, Explorer, and Incidents

These threat investigation and response capabilities surface in the Security &amp; Compliance Center, as a set of tools and response workflows, including the [threat dashboard](#threat-dashboard), [Threat Explorer](#threat-explorer), [Incidents](get-started-with-ti.md#incidents), [Attack Simulator](attack-simulator.md), and Automated Investigations & Response.
  
### Threat dashboard

Use the Threat dashboard (this is also referred to as the [Security dashboard](security-dashboard.md)) to quickly see what threats have been addressed, and as a visual way to report to business decision makers how Office 365 services are securing your business.
  
![Threat Dashboard](media/ce013a31-3f80-4d09-bb95-bfb7623b8bc4.png)
  
To view and use this dashboard, in the Security &amp; Compliance Center, go to **Threat management** \> **Dashboard**.
  
### Threat Explorer

Use the [Threat Explorer (and real-time detections)](threat-explorer.md) to analyze threats, see the volume of attacks over time, and analyze data by threat families, attacker infrastructure, and more. Threat Explorer (also referred to as Explorer) is the starting place for any security analyst's investigation workflow.
  
![Threat explorer](media/7a7cecee-17f0-4134-bcb8-7cee3f3c3890.png)
  
To view and use this report, in the Security &amp; Compliance Center, go to **Threat management** \> **Explorer**.
  
 ### Incidents

Use the Incidents list (this is also called Investigations) to see a list of in flight security incidents. Incidents are used to track threats such as suspicious email messages, and to conduct further investigation and remediation.
  
![List of current Threat Incidents in Office 365](media/acadd4c7-d2de-4146-aeb8-90cfad805a9c.png)
  
To view the list of current incidents for your organization, in the Security &amp; Compliance Center, go to **Threat management** \> **Review** \> **Incidents**.
  
![In the Security &amp; Compliance Center, choose Threat management \> Review](media/e0f46454-fa38-40f0-a120-b595614d1d22.png)
  
## Learn more about Malware &amp; Threats

As part of the Office 365 Advanced Threat Protection Plan 2 offering, security analysts can review details about a known threat. This is useful to determine whether there are additional preventative measures/steps that can be taken to keep users safe.
  
![Security Trends showing information about recent threats](media/11e7d40d-139b-4c56-8d52-c091c8654151.png) 
  
## How do we get these Threat investigation and response capabilities?

Office 365 Threat Invesigation and Response capabilities are included in Office 365 Advanced Threat Protection Plan 2 and Enterprise E5. 

> [!TIP]
> If your organization has an Office 365 subscription that does not include these threat investigation and response capabilities, you can purchase these as an add-on along with Office 365 Advanced Threat Protection. For more information about plan options, see [Office 365 Platform Service Description: Office 365 Security &amp; Compliance Center](https://docs.microsoft.com/office365/servicedescriptions/office-365-platform-service-description/office-365-securitycompliance-center) and [Buy or edit an add-on for Office 365 for business](https://docs.microsoft.com/office365/admin/subscriptions-and-billing/buy-or-edit-an-add-on).
  
1. As an Office 365 global administrator, go to [https://admin.microsoft.com](https://admin.microsoft.com) and sign in using your work or school account for Office 365. 
    
2. Choose **Admin** \> **Billing** to see what your current subscription includes. 
    - If you see **Office 365 Enterprise E5**, then your organization has Office 365 Advanced Threat Protection Plan 2 (which includes threat investigation and response capabilities). 
    - If you see a different subscription, such as **Office 365 Enterprise E3** or **Office 365 Enterprise E1**, consider adding Office 365 Advanced Threat Protection Plan 2. (To do that, choose **+ Add subscription**.)
    
3. In the Microsoft 365 admin center, choose **Users** \> **Active users**.
    
5. Assign Office 365 Advanced Threat Protection Plan 2 licenses to all active users. (Only users who have a license for this will show up in reports, such as Explorer.)
    
6. Assign roles to people in your organization who will be working with the Office 365 Advanced Threat Protection. See [Give users access to the Office 365 Security &amp; Compliance Center](grant-access-to-the-security-and-compliance-center.md), and refer to the following table:<br/>

  |**To do this activity...** <br/> |**You must have one of these roles** <br/> |  
  |:-----|:-----|
  |Use the Threat dashboard (or the new [Security dashboard](security-dashboard.md))<br/> View information about recent or current threats  <br/> |Office 365 Global Administrator  <br/> Security Administrator (assigned in the Security &amp; Compliance Center)  <br/> Security Reader (assigned in the Security &amp; Compliance Center)  <br/> |
  |Use [Threat Explorer (and real-time detections)](threat-explorer.md) to analyze threats  <br/> |Office 365 Global Administrator  <br/> Security Administrator (assigned in the Security &amp; Compliance Center)  <br/> Security Reader (assigned in the Security &amp; Compliance Center)  <br/> |
  |View Incidents (also referred to as Investigations) <br/> Add email messages to an incident  <br/> |Office 365 Global Administrator  <br/> Security Administrator (assigned in the Security &amp; Compliance Center)  <br/> Security Reader (assigned in the Security &amp; Compliance Center)  <br/> |
  |Trigger email actions in an incident  <br/> Find and delete suspicious email messages  <br/> |Office 365 Global Administrator or Security Administrator  <br/> One of the roles above and Search and Purge (assigned in the Security &amp; Compliance Center)  <br/> |
  |Integrate Office 365 Advanced Threat Protection Plan 2 with Microsoft Defender ATP  <br/> Integrate Office 365 Advanced Threat Protection Plan 2 with a SIEM server  <br/> |Office 365 Global Administrator  <br/> Security Administrator (assigned in the Security &amp; Compliance Center)  <br/> Appropriate role assigned in additional applications (such as Microsoft Defender Security Center or a SIEM server)  <br/> |
   
For information about roles, role groups, and permissions, see [Permissions in the Office 365 Security &amp; Compliance Center](permissions-in-the-security-and-compliance-center.md).
    
## Next steps

- [Learn about Threat Trackers - New and Noteworthy](threat-trackers.md)
    
- [Find and investigate malicious email that was delivered (Office 365 Threat Investigation and Response)](investigate-malicious-email-that-was-delivered.md)
    
- [Integrate Office 365 Threat Investigation and Response with Microsoft Defender Advanced Threat Protection](integrate-office-365-ti-with-wdatp.md)
    
- [Learn about Attack Simulator](attack-simulator.md)
  

