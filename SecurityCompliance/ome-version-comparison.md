---
title: "Office 365 Message Encryption (OME) version comparison"
ms.reviewer: 
ms.author: krowley
author: kccross
manager: laurawi
audience: Admin
ms.topic: conceptual
ms.service: O365-seccomp
localization_priority: Normal
ms.date: 4/30/2019
ms.collection: 
- Strat_O365_IP
- M365-security-compliance
search.appverid:
- MET150
description: "Helps explain the differences between the versions of Office 365 Message Encryption."
---

# Compare versions of OME

This article compares legacy Office 365 Message Encryption (OME) to the new OME capabilities and Office 365 Advanced Message Encryption. The new capabilities are a merger and newer version of both OME and Information Rights Management (IRM). Unique characteristics of deploying into GCC High are also outlined. The two can coexist in your Office 365 organization. For information on how the new capabilities work, see [Office 365 Message Encryption (OME)](ome.md).

||
|:-----|
|This article is part of a larger series of articles about Office 365 Message Encryption. This article is intended for administrators and ITPros. If you're just looking for information on sending or receiving an encrypted message, see the list of articles in [Office 365 Message Encryption (OME)](ome.md) and locate the article that best fits your needs. |
||

## Side-by-side comparison of features and capabilities

|                                   |Old features       |                   |New features              |
|-----------------------------------|-------------------|-------------------|--------------------------|
|**Capability**                     | **Legacy OME**    | **IRM**           | **New OME capabilities** |
|*Sending an encrypted mail*        |Through Exchange mail flow rules|End-user initiated from Outlook desktop or Outlook on the Web; or through Exchange mail flow rules|End-user initiated from Outlook desktop, Outlook for Mac, or Outlook on the Web; through Exchange mail flow rules (also known as transport rules) and Office 365 Data Loss Prevention (DLP)|
|*Rights management template*       |   N/A      |Do Not Forward option and custom templates|Do Not Forward option, Encrypt-Only option, and custom templates|
|*Recipient type*                   |Internal and external recipients|Internal recipients only         |Internal and external recipients|
|*Experience for internal recipient*|Recipients receive an HTML message, which they download and open in a web browser or mobile app|Native inline experience in Outlook clients|Native inline experience for recipients in the same organization using Outlook clients.  Recipients can read message from OME portal using clients other than Outlook (no download or app required).|
|*Experience for external recipient*|Recipients receive an HTML message, which they download and open in a web browser or mobile app|N/A|Native inline experience for Office 365 recipients. All other recipients can read message from OME portal (no download or app required).|
|*Attachment permissions*           |No restrictions on attachments|Attachments are protected|Attachments are protected for the Do Not Forward option and custom templates. Admins can choose whether attachments for the Encrypt-Only option are protected or not.|
|*Bring your own key (BYOK) support*|None                |None               |BYOK supported          |
||

## Advantages of the new OME capabilities over legacy OME

The new capabilities provide the following advantages:

- Ability to use Encrypt-Only (which enables secure collaboration), Do Not Forward, and custom restrictions.
- Senders can send mail encrypted with the new capabilities manually from Outlook Desktop, Outlook for Mac and Outlook on the web clients.
- Office 365 recipients get to use an inline experience in supported Outlook clients. Alternatively, admins can choose to show Office 365 recipients a branded experience.
- Accounts outside of Office 365, such as Gmail, Yahoo, and Microsoft accounts, are federated with the OME portal, which provides a better user experience for these recipients. All other identities use a one-time pass code to access encrypted messages.
- Admins can customize branding, and create multiple branding templates.
- Admins can revoke emails encrypted with the new capabilities.
- The new capabilities provide detailed usage reports through the Security &amp; Compliance Center.

## Office 365 Advanced Message Encryption capabilities

Office 365 Advanced Message Encryption offers additional capabilities on top of the new OME capabilities. You must have the new Office 365 Message Encryption capabilities set up in your organization in order to use the Advanced Message Encryption capabilities. Also, in order to use these capabilities, recipients must view and reply to secure mail through the OME Portal. The advanced capabilities  include:

- Message revocation

- Message expiration

- Multiple branding templates

Office 365 Advanced Message Encryption is not supported in GCC High.

For information on using Advanced Message Encryption, see [Office 365 Advanced Message Encryption](ome-advanced-message-encryption.md).

## Unique characteristics of Office 365 Message Encryption in a GCC High deployment

Office 365 Advanced Message Encryption is not available in a GCC High environment. You can still use a single brand template in a GCC High environment.

In addition, if you plan to use Office 365 Message Encryption in a GCC High environment, there are some unique characteristics about the recipient experience.

Office 365 Advanced Message Encryption is not supported in GCC High.

### Encrypted email from GCC High to GCC High recipients

Senders can manually encrypt emails in Outlook for PC and Mac and Outlook on the web, or organizations can set up a policy to encrypt emails using Exchange mail flow rules.

Recipients inside GCC High receive the same inline reading experience in Outlook for PC and Mac and Outlook on the web as all other Office 365 users.

### Encrypted email from GCC High to Non-GCC High recipients

Senders inside GCC High can send encrypted email outside of the GCC High boundary.

All recipients outside GCC High, including commercial Office 365 users, Outlook.com users, and other users of other email providers such as Gmail and Yahoo, receive a wrapper mail. This wrapper mail redirects the recipient to the OME Portal where the recipient can read and reply to message.

## Coexistence of legacy OME and the new capabilities in the same tenant

You can use both legacy OME and the new capabilities in the same tenant. As an administrator, you do this by choosing which version of OME you want to use when you create your mail flow rules.

- To specify the legacy version of OME, use the Exchange mail flow rule action **Apply the previous version of OME**.

- To specify the new capabilities, use the Exchange mail flow rule action **Apply Office 365 Message Encryption and rights protection**.

Users can manually send mail that is encrypted with the new capabilities from Outlook Desktop, Outlook for Mac, and Outlook on the web.

## Migrate from legacy OME to the new capabilities

Even though both versions of OME can coexist, we highly recommend that you edit your old mail flow rules that use the rule action **Apply the previous version of OME** to use the new capabilities. Update these rules to use the mail flow rule action **Apply Office 365 Message Encryption and rights protection**. For instructions, see [Define mail flow rules to encrypt email messages in Office 365](define-mail-flow-rules-to-encrypt-email.md).

## Get started with OME

Typically, the new OME capabilities are automatically enabled for your Office 365 organization. For more information about the new OME capabilities within your organization, see [Set up new Office 365 Message Encryption capabilities](set-up-new-message-encryption-capabilities.md).

The legacy version of OME is automatically enabled for your Office 365 organization if you have enabled Azure Information Protection. In the past, legacy OME worked even if Azure Information Protection wasn’t enabled. This is no longer the case.

To start using legacy OME, if you have enabled Azure Information Protection, configure mail flow rules that use the rule action **Apply the previous version of OME**. For instructions, see [Define mail flow rules to encrypt email messages in Office 365](define-mail-flow-rules-to-encrypt-email.md).
