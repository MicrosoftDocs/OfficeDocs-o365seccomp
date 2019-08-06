---
title: "Office 365 email anti-spam protection"
ms.author: krowley
author: kccross
manager: dansimp
ms.date: 6/29/2018
audience: Admin
ms.topic: overview
ms.service: O365-seccomp
localization_priority: Normal
search.appverid:
- MET150
- MOE150
ms.assetid: 6a601501-a6a8-4559-b2e7-56b59c96a586
ms.collection:
- M365-security-compliance
description: "Learn about the anti-spam settings and filters that will help you prevent spam in Exchange Online and Office 365. Getting too much spam in Office 365? You can customize your spam filters and anti-spam policy settings."
---

# Office 365 email anti-spam protection

Are you concerned about too much spam in Office 365? We've built multiple spam filters into your Office 365 or Exchange Online Protection (EOP) service, so your email is protected from the moment you receive your first message. In order to help prevent spam in Office 365, you may want to change a protection setting to deal with a specific issue in your organization—say you're receiving a lot of spam from a particular sender, for example—or to simply fine tune your settings so that they're tailored to best meet the needs of your organization. To do this, you can change anti-spam settings in the Office 365 Security &amp; Compliance Center.
  
This article is intended for Office 365 administrators. If you're not an administrator, but you are an Office 365 user and you want to learn how to deal with spam you receive, this isn't the article you're looking for. Instead, if you use Outlook for PC or Outlook for Mac, start with [Overview of the Junk Email Filter](https://support.office.com/article/5ae3ea8e-cf41-4fa0-b02a-3b96e21de089). If you use Outlook on the web, start with [Learn about junk email and phishing](https://support.office.com/article/86c1d76f-4d5a-4967-9647-35665dc17c31).
  
## These options help you prevent spam in Office 365

 **Connection filtering**: When you use connection filtering, Office 365 checks the reputation of the sender before allowing a message to get through. You can create an allow list, or safe sender list, to make sure you receive every message sent to you from a specific IP address or IP address range. You can also create a list of IP addresses from which to block messages, called a block list. For more information, see [Configure the Connection Filter Policy](https://technet.microsoft.com/library/jj200718%28v=exchg.150%29.aspx). If you're concerned about spam in Office 365, use connection filtering to help prevent spam.
  
For customers who have Office 365 Enterprise E5 or have purchased Advanced Threat Protection (ATP) licenses, connection filtering is used by spoof intelligence to create allow and block lists of senders who are spoofing your domain. For more information, see [Learn more about spoof intelligence](https://go.microsoft.com/fwlink/?LinkID=735009).
  
 **Spam filtering**: Office 365 checks for message characteristics consistent with spam by using spam filtering. You can change what actions to take on messages identified as spam, and choose whether to filter messages written in specific languages, or sent from specific countries or regions. You can also turn on advanced spam filtering options if you want to pursue an aggressive approach to spam filtering. Additionally, you can configure end-user spam notifications to inform users when messages intended for them were sent to the quarantine instead. (Sending messages to the quarantine is one of the configurable actions.) From these notifications, end users can release false positives and report them to Microsoft for analysis. For more information, see [Configure your spam filter policies](https://go.microsoft.com/fwlink/p/?LinkId=617147). In order to help prevent spam in Office 365, use spam filtering, if you're concerned about too much spam in Office 365, use connection filtering to help prevent spam.
  
> [!NOTE]
> For EOP standalone customers: By default, the EOP spam filters send spam-detected messages to each recipients' Junk Email folder. However, in order to ensure that the **Move message to Junk Email folder** action will work with on-premises mailboxes, you must configure two Exchange mail flow rules (also known as transport rules) on your on-premises servers to detect spam headers added by EOP. For details, see [Ensure that spam is routed to each user's Junk Email folder](https://technet.microsoft.com/library/jj837173%28v=exchg.150%29.aspx). 
  
## Extra information if you receive too much spam in Office 365

The following video provides an overview of configuring spam filtering in EOP.
  
> [!VIDEO https://www.microsoft.com/videoplayer/embed/608be94c-d763-4c47-af94-99e7cb277713?autoplay=false]
  
For more details, see the [Configure spam filter policies](https://go.microsoft.com/fwlink/p/?LinkId=617147) topic.
  
## Check your outgoing messages to prevent spam in Office 365

 **Outbound filtering**: Office 365 also checks to make sure that your users don't send spam. For instance, a user's computer may get infected with malware that causes it to send spam messages, so we build protection against that called *outbound filtering*. You can't turn off outbound filtering, but you can configure the settings described in [Configure the outbound spam policy](https://technet.microsoft.com/library/jj200737%28v=exchg.150%29.aspx). If you're concerned about too much spam in Office 365, use outbound filtering to help prevent spam in Exchange Online.
  
## Beyond the basics: More ways to prevent spam in Office 365

 **Mail flow rules**: If you want to go beyond built-in spam filtering and create custom rules that are based on your business policies, _[mail flow rules](https://technet.microsoft.com/library/jj919238%28v=exchg.150%29.aspx)_ (also known as _transport rules_) are another filter that helps you prevent spam in Office 365. For example, you can use mail flow rules to set the spam confidence level (SCL) value for messages that match specific conditions, as described in [Use mail flow rules to set the spam confidence level (SCL) in messages](use-mail-flow-rules-to-set-the-spam-confidence-level-scl-in-messages.md).
  
 **Email authentication**: Techniques that use the Domain Name System (DNS) to add verifiable information to email messages about the sender of an email message are called email authentication. More advanced Office 365 admins can make use of these email authentication methods:
  
- **Sender Policy Framework (SPF)**: SPF validates the origin of email messages by verifying the IP address of the sender against the alleged owner of the sending domain. For a quick introduction to SPF and to get it configured quickly, see [Set up SPF in Office 365 to help prevent spoofing](https://technet.microsoft.com/library/dn789058%28v=exchg.150%29.aspx). For a more in-depth understanding of how Office 365 uses SPF, or for troubleshooting or non-standard deployments such as hybrid deployments, start with [How Office 365 uses Sender Policy Framework (SPF) to prevent spoofing](https://technet.microsoft.com/library/mt712724%28v=exchg.150%29.aspx).

- **DomainKeys Identified Mail (DKIM)**: DKIM lets you attach a digital signature to email messages in the message header of emails you send. Email systems that receive email from your domain use this digital signature to determine if incoming email that they receive is legitimate. For information about DKIM and Office 365, see [Use DKIM to validate outbound email sent from your domain in Office 365](https://technet.microsoft.com/library/mt695945%28v=exchg.150%29.aspx).

- **Domain-based Message Authentication, Reporting, and Conformance (DMARC)**: DMARC helps receiving mail systems determine what to do with messages that fail SPF or DKIM checks and provides another level of trust for your email partners. For information on setting up DMARC, see [Use DMARC to validate email in Office 365](https://technet.microsoft.com/library/mt734386%28v=exchg.150%29.aspx).

If you're concerned about spam, phishing, and spoofing in Office 365, use SPF, DKIM, and DMARC together to help prevent spam and unwanted spoofing.
  
 **End-user managed settings**: If you're looking for information about how end users can manage their own spam settings, check out [Overview of the Junk Email Filter](https://go.microsoft.com/fwlink/?LinkId=270065) (for Microsoft Outlook users) or [Learn about Junk email and phishing](https://go.microsoft.com/fwlink/?LinkId=270068) (for Outlook on the web users). If you're using EOP to protect on-premises mailboxes, be sure to use directory synchronization to ensure that these settings are synced to the service. For more information about setting up directory synchronization, see "Use directory synchronization to manage mail users" in [Manage mail users in EOP](https://technet.microsoft.com/library/dn636911%28v=exchg.150%29.aspx).
  
## For more information

[Blog: Why does spam and phishing get through Office 365?](https://go.microsoft.com/fwlink/?LinkId=528179 )
  
[Anti-Spam Protection FAQ](https://technet.microsoft.com/library/jj937231%28v=exchg.150%29.aspx)
  
[Prevent false positive email marked as spam with a safelist or other techniques](prevent-email-from-being-marked-as-spam-0.md)
  
[How to set up Office 365 spam filtering to help block junk messages](reduce-spam-email.md)
  
[What's the Difference Between Junk Email and Bulk Email?](https://technet.microsoft.com/library/dn720441%28v=exchg.150%29.aspx)
  
[Anti-spam message headers](https://technet.microsoft.com/library/dn205071%28v=exchg.150%29.aspx)
  
[Backscatter Messages and EOP](https://technet.microsoft.com/library/dn499795%28v=exchg.150%29.aspx)

## More resources

[Get help from the Office 365 community forums](https://go.microsoft.com/fwlink/p/?LinkId=518605)
  
[Admins: Sign in and create a service request](https://go.microsoft.com/fwlink/p/?LinkId=519124)
  
[Admins: Call Support](https://go.microsoft.com/fwlink/p/?LinkID=518322)
