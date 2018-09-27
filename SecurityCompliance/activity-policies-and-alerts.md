---
title: "Activity policies and alerts in Office 365 Cloud App Security"
ms.author: deniseb
author: denisebmsft
manager: laurawi
ms.date: 2/26/2018
ms.audience: ITPro
ms.topic: article
ms.service: o365-administration
localization_priority: Normal
search.appverid:
- MET150
- MOE150
ms.assetid: 367f25d3-10a0-4a91-bdae-70ebb7a79c98
description: "Define activity policies with Office 365 Cloud App Security to set up alerts to trigger when specific activities happen or happen too frequently. By setting up policies to trigger alerts, you can be notified about and monitor specific activities."
---

# Activity policies and alerts in Office 365 Cloud App Security

Office 365 Advanced Security Management is now Office 365 Cloud App Security. 
  
|****Evaluation** \>**|****Planning** \>**|****Deployment** \>**|****Utilization****|
|:-----|:-----|:-----|:-----|
|[Start evaluating](office-365-cas-overview.md) <br/> |[Start planning](get-ready-for-office-365-cas.md) <br/> |You are here!  <br/> [Next step](anomaly-detection-policies-in-ocas.md) <br/> |[Start utilizing](utilization-activities-for-ocas.md) <br/> |
   
With Office 365 Cloud App Security, advanced cloud management policies trigger alerts for specific activities that happen or happen too frequently. For example, suppose a user tries to sign in to Office 365 and fails 70 times in one minute. Suppose that another user downloads 7,000 files, or appears to be signed in from Canada, when that user is supposed to be in another location. Or worse, suppose that someone's account has been compromised, and an attacker is using that account to access your organization's cloud apps and sensitive data.
  
If you are a [global administrator or security administrator](permissions-in-the-security-and-compliance-center.md), activity alerts notify you when events like these occur. You can then take specific actions, such as suspending a user account until you can investigate what happened.
  
> [!NOTE]
> Office 365 Cloud App Security policies are different from [alert policies in the Office 365 Security &amp; Compliance Center](alert-policies.md). The activity policies described in this article are defined in the Office 365 Cloud App Security portal, and can help you better manage your organization's cloud environment. 
  
## Before you begin

Make sure that:
  
- Your organization has [Office 365 Cloud App Security](office-365-cas-overview.md), and the service is [turned on](turn-on-office-365-cas.md).
    
- [Audit logging](turn-audit-log-search-on-or-off.md) is turned on for your Office 365 environment. 
    
- You are a global administrator or security administrator for Office 365.
    
## Create a new activity policy

1. As a global administrator or security administrator, go to [https://protection.office.com](https://protection.office.com) and sign in using your work or school account. 
    
2. In the Security &amp; Compliance Center, choose **Alerts** \> **Manage advanced alerts**.
    
3. Choose **Go to Office 365 Cloud App Security**.
    
    This takes you to the Office 365 Cloud App Security Policies page.
    
    ![When you go to the Office 365 Cloud App Security portal, you start with the Policies page](media/5cb8833c-4e08-438c-bab3-91b5106f6f3f.png)
  
4. Click **Create policy**, and then select **Activity policy**.
    
    ![When you create a policy in O365 CAS, you can choose between Activity policies and Anomaly Detection policies.](media/79f34535-ddf9-4a5b-a0a3-8766bf9c174c.png)
  
5. On the **Create activity policy** page, specify the **Policy name** and **Description**. To base your policy on a default template, choose one in the **Policy template** list, or create your own policy without using a template. 
    
    ![You can create activity policies with Office 365 Cloud App Security.](media/4083a76f-7074-4d6a-8200-6d76d49259d7.png)
  
6. Choose a **Policy severity** (Low, Medium, or High) that measures how serious it is to you if this policy triggers an alert. This will help you filter alerts when you're reviewing them later. 
    
7. Choose a **Category** for this policy. This will help you filter and sort alerts that have been triggered, or to group policies when you're reviewing them to make changes. 
    
8. Choose **Activity filters** to set up other actions or metrics that will trigger an alert based on this policy. 
    
9. Under **Activity match parameters**, specify whether a policy violation will be triggered when a single activity matches the filters, or if a specified number of repeated activities is required before the alert triggers.
    
    If you select **Repeated activity**, specify the number of activities, the time frame, and whether a violation will count for a user within a specific app or for the same user with any app.
    
10. Optionally, you can select **Create alert** to create additional alerts to receive notifications from this policy (via email, text message, or both). 
    
    > [!IMPORTANT]
    > Make sure that your email provider doesn't block emails sent from no-reply@cloudappsecurity.com. 
  
11. Choose the **Actions** that should be taken when an alert is triggered to suspend the user or require the user to sign in again to Office 365 apps. 
    
12. Choose **Create** to finish creating your policy. 
    
## Next steps

- [Anomaly detection policies](anomaly-detection-policies-in-ocas.md)
    
- [Integrate your SIEM server](integrate-your-siem-server-with-office-365-cas.md)
    
- [Review and take action on alerts](review-office-365-cas-alerts.md)
    
- [Group your IP addresses to simplify management](group-your-ip-addresses-in-ocas.md)
    

