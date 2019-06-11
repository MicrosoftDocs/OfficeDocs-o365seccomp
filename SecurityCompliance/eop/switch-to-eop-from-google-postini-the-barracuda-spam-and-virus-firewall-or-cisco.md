---
title: "Switch to EOP from Google Postini, the Barracuda Spam and Virus Firewall, or Cisco IronPort"
ms.reviewer: 
ms.author: krowley
author: kccross
manager: laurawi
ms.date: 12/9/2016
audience: ITPro
ms.topic: article
ms.service: O365-seccomp
localization_priority: Normal
ms.assetid: 81b75194-3b04-48da-8b81-951afbabedde
description: "The purpose of this topic is to help you understand the process for switching to Exchange Online Protection (EOP) from an on-premises email hygiene appliance or cloud-based protection service, and then to provide you with help resources to get started."
---

# Switch to EOP from Google Postini, the Barracuda Spam and Virus Firewall, or Cisco IronPort

 The purpose of this topic is to help you understand the process for switching to Exchange Online Protection (EOP) from an on-premises email hygiene appliance or cloud-based protection service, and then to provide you with help resources to get started. There are many spam-filtering solutions, but the process for switching to EOP is similar in most cases.
  
If you are new to EOP and you want to read an overview of its features before you decide to switch, start with the [Exchange Online Protection overview](exchange-online-protection-overview.md) on TechNet. 
  
Before you switch to EOP, it's important to think about whether you want to host your EOP-protected mailboxes in the cloud, with Exchange Online, on-premises, or in a hybrid scenario. (Hybrid means that you have some mailboxes hosted on-premises and another portion hosted with Exchange Online.) Each of these hosting scenarios: cloud, on-premises, and hybrid, is possible, but the setup steps can vary. Here are a few considerations to help you choose the appropriate deployment:
  
- **EOP protection with on-premises mailboxes** This scenario is appropriate if you have existing mail-hosting infrastructure you want to use, or you have business requirements to keep mailboxes on-premises, and you want EOP's cloud-based email protection. [Switch to EOP standalone](#switch-to-eop-standalone) describes this scenario in more detail. 
    
- **EOP protection with Exchange Online mailboxes** This scenario is appropriate if you want EOP protection and all of your mailboxes hosted in the cloud. It can help you reduce complexity, because you don't have to maintain on-premises messaging servers. [Switch to Exchange Online](switch-to-eop-from-google-postini-the-barracuda-spam-and-virus-firewall-or-cisco.md#BKMK_SwitchEXO) describes this scenario. 
    
- **EOP protection with hybrid mailboxes** Perhaps you want cloud mailboxes, but you need to keep mailboxes for some users on-premises. Choose this scenario if you want some mailboxes hosted on-premises and another portion hosted with Exchange Online. [Switch to a hybrid solution](#switch-to-a-hybrid-solution) describes this scenario. 
    
## Switch to EOP standalone

If you currently host your mailboxes on premises and use an on-premises protection appliance or a cloud messaging-protection service, you can switch to EOP to take advantage of its protection features and availability. To set up EOP in a standalone scenario, which means you host your mailboxes on premises and use EOP to provide email protection, you can follow the steps outlined in [Set up your EOP service](set-up-your-eop-service.md). The topic outlines the steps for setting up EOP protection, which include sign up, adding your domain, and setting up mail flow with connectors.
  
## Switch to Exchange Online
<a name="BKMK_SwitchEXO"> </a>

Perhaps you have on-premises mailboxes protected by an on-premises appliance, and you want to jump to Exchange Online cloud-hosted mailboxes and EOP protection to take advantage of Office 365 cloud messaging and protection features. To get started, you can sign up for Office 365 and add your domain. This scenario doesn't require you to setup connectors, because there isn't any routing to on-premises mailboxes. Begin at the [Office 365 sign up page](https://www.microsoft.com/en-us/office365/online-software.aspx). ([Get started with Office 365](https://go.microsoft.com/fwlink/p/?LinkId=275407) provides resources to get familiar with its features.) 
  
During the Office 365 setup process, you will create your cloud-based mailbox users.
  
## Switch to a hybrid solution
<a name="BKMK_SwitchHybrid"> </a>

You may want to move only a portion of your mailboxes to the cloud because of business requirements or regulatory considerations. When you deploy a hybrid scenario, you can move mailboxes to the cloud as your business requirements dictate. Migrating to a hybrid scenario with EOP protection is more complicated than moving to an all-cloud scenario, but Microsoft provides full hybrid support and ample resources to make the move to hybrid easier.
  
The best place to start, if you are considering a hybrid deployment, is [Exchange Server 2013 Hybrid Deployments](http://technet.microsoft.com/library/59e32000-4fcf-417f-a491-f1d8f9aeef9b.aspx). Additionally, there are a few different ways you can route mail in a hybrid scenario that are important to understand. [Transport Routing in Exchange 2013 Hybrid Deployments](http://technet.microsoft.com/library/36c2cea3-2e2f-40ac-88bd-7e1b6bd27828.aspx) explains each type, so you can choose the best routing scenario, based on your business requirements. 
  
## Migration planning
<a name="sectionSection3"> </a>

When you decide to switch to EOP, make sure you give special consideration to the following areas:
  
- **Custom Filtering Rules** If you have custom filtering or business-policy rules to catch specific spam, we recommend that you try EOP with the default settings for a period, before you migrate your rules. EOP offers enterprise-level spam protection with the default settings, it may turn out that you don't need to migrate some of your rules to EOP. Of course, if you have rules in place that enforce specific custom business policies, you can create those. [Mail flow rules (transport rules) in Exchange Online Protection](mail-flow-rules-transport-rules-0.md) provides detailed instructions for creating mail flow rules in EOP. 
    
- **IP allow lists and IP block lists** If you have per-user allow lists and block lists, allow some time to copy the lists to EOP as part of your setup process. For more information about IP allow lists and IP block lists, see [Configure the connection filter policy](../configure-the-connection-filter-policy.md).
    
- **Secure Communication** If you have a partner that requires encrypted messaging, we recommend that you set this up in the Exchange admin center. To configure this scenario, see [Create connectors for a secure mail channel using transport layer security (TLS)](http://technet.microsoft.com/library/1ce4d6a4-41ba-4d1e-9ca9-e826252c1041.aspx).
    
> [!TIP]
> When you switch from an on-premises appliance to EOP, it is possible to leave your appliance or a server in place that performs business rule checks. For instance, if your appliance performs custom filtering on outbound mail, and you want it to continue doing so, you can configure EOP to send mail directly to the appliance for additional filtering, before it is routed to the Internet. [Exchange Online Protection Connectors - Outbound Smart Host Scenario](http://technet.microsoft.com/library/431b3f02-4efd-4bd3-94e7-eecd03f8ef5e.aspx) shows you how to set up mail flow in this case. 
  

