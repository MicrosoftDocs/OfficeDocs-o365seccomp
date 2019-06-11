---
title: "Set up your EOP service"
ms.reviewer: 
ms.author: krowley
author: kccross
manager: laurawi
ms.date: 10/23/2018
audience: ITPro
ms.topic: article
ms.service: O365-seccomp
localization_priority: Normal
ms.assetid: d74c6ddf-11b0-43ee-b298-8bb0340895f0
description: "This topic explains how to set up Microsoft Exchange Online Protection (EOP). If you landed here from the Office 365 domains wizard, go back to the Office 365 domains wizard if you don't want to use Exchange Online Protection. If you're looking for more information on how to configure connectors, see Configure mail flow using connectors in Office 365."
---

# Set up your EOP service

This topic explains how to set up Microsoft Exchange Online Protection (EOP). If you landed here from the Office 365 domains wizard, go back to the Office 365 domains wizard if you don't want to use Exchange Online Protection. If you're looking for more information on how to configure connectors, see [Configure mail flow using connectors in Office 365](http://technet.microsoft.com/library/854b5a50-4462-4836-a092-37e208d29624.aspx).
  
> [!NOTE]
> This topic assumes you have on-premises mailboxes and you want to protect them with EOP, which is known as a standalone scenario. If you want to host all of your mailboxes in the cloud with Exchange Online, you don't have to complete all of the steps in this topic. Go to [Exchange Online](https://go.microsoft.com/fwlink/p/?LinkId=286312) to sign up and purchase cloud mailboxes. If you want to host some of your mailboxes on premises and some in the cloud, this is known as a hybrid scenario. It requires more advanced mail-flow settings. [Exchange Server 2013 Hybrid Deployments](http://technet.microsoft.com/library/59e32000-4fcf-417f-a491-f1d8f9aeef9b.aspx) explains hybrid mail flow and has links to resources that show how to set it up. 
  
## What do you need to know before you begin?

- Estimated time to complete this task: 1 hour
    
- To configure connectors, your account must be an Office 365 Global Admin, or an Exchange Company Administrator (the Organization Management role group). For information about how Office 365 permissions relate to Exchange permissions, see [Permissions in Office 365](https://go.microsoft.com/fwlink/p/?LinkID=335814).
    
- If you haven't signed up for EOP, visit [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?LinkId=282660) and choose to buy or try the service. 
    
- For information about keyboard shortcuts that may apply to the procedures in this topic, see **Keyboard shortcuts in the Exchange admin center**.
    
> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at [Exchange Server](https://go.microsoft.com/fwlink/p/?linkId=60612),[Exchange Online](https://go.microsoft.com/fwlink/p/?linkId=267542), or [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkId=285351). 
  
## How do you do this?

### Step 1: Use the Microsoft 365 admin center to add and verify your domain

1. In the Microsoft 365 admin center, navigate to **Setup** to add your domain to the service. 
    
    Not sure where to find the Microsoft 365 admin center? Learn more at [About the Microsoft 365 admin center](https://go.microsoft.com/fwlink/p/?LinkId=521888).
    
2. Follow the steps to add the applicable DNS records to your DNS-hosting provider in order to verify domain ownership.
    
> [!TIP]
> [Add your domain to Office 365](https://support.office.com/en-us/article/add-a-domain-to-office-365-6383f56d-3d09-4dcb-9b41-b5f5a5efd611) and [Create DNS records for Office 365](https://support.office.com/en-us/article/create-dns-records-at-any-dns-hosting-provider-for-office-365-7b7b075d-79f9-4e37-8a9e-fb60c1d95166) are helpful resources to reference as you add your domain to the service and configure DNS. 
  
### Step 2: Add recipients and optionally enable DBEB

Before configuring your mail to flow to and from the EOP service, we recommend adding your recipients to the service. There are several ways in which you can do this, as documented in [Manage mail users in EOP](manage-mail-users-in-eop.md). Also, if you want to enable Directory Based Edge Blocking (DBEB) in order to enforce recipient verification within the service after adding your recipients, you need to set your domain type to Authoritative. For more information about DBEB, see [Use Directory Based Edge Blocking to Reject Messages Sent to Invalid Recipients](http://technet.microsoft.com/library/ca7b7416-92ed-40ad-abdb-695be46ea2e4.aspx).
  
### Step 3: Use the EAC to set up mail flow

Create connectors in the Exchange admin center (EAC) that enable mail flow between EOP and your on-premises mail servers. For detailed instructions, see [Set up connectors to route mail between Office 365 and your own email servers](http://technet.microsoft.com/library/2e93fd60-a5ef-4e64-8e62-2b862b2d1033.aspx).
  
#### How do you know this task worked?

Use the Remote Connectivity Analyzer to run a test that checks mail flow between the service and your environment. For more information, see the "Use the Remote Connectivity Analyzer to test email delivery" section in [Testing Mail Flow with the Remote Connectivity Analyzer](http://technet.microsoft.com/library/6c8c2964-d553-4329-8166-6e508dd63fa0.aspx).
  
### Step 4: Allow inbound port 25 SMTP access

After you configured connectors, wait 72 hours to allow propagation of your DNS-record updates. Following this, restrict inbound port-25 SMTP traffic on your firewall or mail servers to accept mail only from the EOP datacenters, specifically from the IP addresses listed at [Exchange Online Protection IP addresses](exchange-online-protection-ip-addresses.md). This protects your on-premises environment by limiting the scope of inbound messages you can receive. Additionally, if you have settings on your mail server that control the IP addresses allowed to connect for mail relay, update those settings as well.
  
> [!TIP]
> Configure settings on the SMTP server with a connection time out of 60 seconds. This setting is acceptable for most situations, allowing for some delay in the case of a message sent with a large attachment, for instance. 
  
### Step 5: Use the Shell to ensure that spam is routed to each user's junk email folder

To ensure that spam (junk) email is routed correctly to each user's Junk Email folder, you must perform a couple of configuration steps. The steps are provided in [Ensure that spam is routed to each user's Junk Email folder](../ensure-that-spam-is-routed-to-each-user-s-junk-email-folder.md).
  
If you don't want to move messages to each user's Junk Email folder, you may choose another action by editing your content filter policies in the Exchange admin center. For more information, see [Configure your spam filter policies](../configure-your-spam-filter-policies.md).
  
### Step 6: Use the Microsoft 365 admin center to point your MX record to EOP

Follow the Office 365 domain configuration steps to update your MX record for your domain, so that your inbound email flows through EOP. Be sure to point your MX record directly to EOP as opposed to having a third-party filtering service relay email to EOP. For more information, you can again reference [Create DNS records for Office 365](https://docs.microsoft.com/office365/admin/get-help-with-domains/create-dns-records-at-any-dns-hosting-provider).
  
#### How do you know this task worked?

Use the Remote Connectivity Analyzer to run a test that verifies your MX record. For more information, see the "Use the Remote Connectivity Analyzer to test your MX record and Outbound connector" section in [Testing Mail Flow with the Remote Connectivity Analyzer](http://technet.microsoft.com/library/6c8c2964-d553-4329-8166-6e508dd63fa0.aspx). 
  
At this point, you've verified service delivery for a properly configured Outbound on-premises connector, and you've verified that your MX record is pointing to EOP. You can now choose to run the following additional tests to verify that an email will be successfully delivered by the service to your on-premises environment:
  
- In the Remote Connectivity Analyzer, click the **Office 365** tab, and then run the **Inbound SMTP Email** test located under **Internet Email Tests**. 
    
- Send an email message from any web-based email account to a mail recipient in your organization whose domain matches the domain you added to the service. Confirm delivery of the message to the on-premises mailbox using Microsoft Outlook or another email client.
    
- If you want to run an outbound email test, you can send an email message from a user in your organization to a web-based email account and confirm that the message is received.
    
> [!TIP]
> When you've completed your setup, you don't have to perform extra steps to make EOP remove spam and malware. EOP removes spam and malware automatically. However, you can fine tune your settings in the EAC, based on your business requirements. For more information, see [Anti-Spam and Anti-Malware Protection](http://technet.microsoft.com/library/93c6c227-7442-4293-b64d-ec8f15c928db.aspx). > Now that your service is running, we recommend reading [Best practices for configuring EOP](best-practices-for-configuring-eop.md), which describes recommended settings and considerations for after you set up EOP. 
  

