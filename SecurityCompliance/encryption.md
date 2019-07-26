---
title: "Encryption in Office 365"
ms.author: krowley
author: kccross
manager: laurawi
ms.date: 1/3/2018
audience: Admin
ms.topic: overview
ms.service: O365-seccomp
localization_priority: Normal
search.appverid:
- MET150
- MOE150
ms.assetid: 0a322724-08ca-43db-b69a-afbfa20484cd
ms.collection:
- M365-security-compliance
- Strat_O365_IP
description: "With Office 365, your content is encrypted at rest and in transit, using the strongest encryption, protocols, and technologies available. Get an overview of encryption in Office 365."
---

# Encryption in Office 365

Encryption is an important part of your file protection and information protection strategies. Read this article to get an overview of encryption used for all versions of Office 365, and get help with encryption tasks, from setting up encryption for your organization to password-protecting Office documents.
  
- If you're looking for information about certificates and technologies like TLS, see [Technical reference details about encryption in Office 365](technical-reference-details-about-encryption.md).

- If you are looking for information about how to configure or set up encryption for your organization, see [Set up encryption in Office 365 Enterprise](set-up-encryption.md).

## What is encryption, and how does it work in Office 365?

At a high level, encryption is the process of encoding your data (referred to as plaintext) into ciphertext that cannot be used by people or computers unless and until the ciphertext is decrypted. Decryption requires an encryption key that only authorized users have. Encryption helps ensure that only authorized recipients can decrypt your content, such as email messages and files.
  
Encryption by itself does not prevent content, such as files, email messages, calendar entries, and so on, from getting into the wrong hands. Encryption is part of a larger information protection strategy for your organization. By using encryption, you can help ensure that only those who should be able to use encrypted data are able to.
  
You can have multiple layers of encryption in place at the same time. For example, you can encrypt email messages and also the communication channels through which your email flows. With Office 365, your data is encrypted at rest and in transit, using several strong encryption protocols, and technologies that include Transport Layer Security/Secure Sockets Layer (TLS/SSL), Internet Protocol Security (IPSec), and Advanced Encryption Standard (AES).
  
## Encryption for data at rest and data in transit

 **Examples of data at rest** include files that have been uploaded to a SharePoint library, Project Online data, documents that have been uploaded in a Skype for Business meeting, email messages and attachments that are stored in folders in your Office 365 mailbox, and files uploaded to OneDrive for Business. 
  
 **Examples of data in transit** include mail messages that are in the process of being delivered, or conversations that are taking place in an online meeting. In Office 365, data is in transit whenever a user's device is communicating with an Office 365 server, or when an Office 365 server is communicating with another server. 
  
With Office 365, you can have multiple layers and kinds of encryption working together to secure your data. The following table includes some examples, with links to additional information.
  
|**Kinds of Content**|**Encryption Technologies**|**Resources to learn more**|
|:-----|:-----|:-----|
|Files on a device. This can include email messages saved in a folder, Office documents saved on a computer, tablet, or phone, or data saved to the Microsoft cloud.  <br/> |BitLocker in Microsoft datacenters. BitLocker can also be used on client machines, such as Windows computers and tablets  <br/> Distributed Key Manager (DKM) in Microsoft datacenters  <br/> Customer Key for Office 365  <br/> |[Windows IT Center: BitLocker](https://docs.microsoft.com/windows/device-security/bitlocker/bitlocker-overview) <br/> [Microsoft Trust Center: Encryption](https://www.microsoft.com/en-us/TrustCenter/Security/Encryption) <br/> [Cloud security controls series: Encrypting Data at Rest](https://blogs.microsoft.com/microsoftsecure/2015/09/10/cloud-security-controls-series-encrypting-data-at-rest) <br/> [How Exchange Online secures your email secrets](exchange-online-secures-email-secrets.md) <br/> [Controlling your data in Office 365 using Customer Key](controlling-your-data-using-customer-key.md) <br/> |
|Files in transit between users. This can include Office documents or SharePoint list items shared between users.  <br/> |TLS for files in transit  <br/> |[Data Encryption in OneDrive for Business and SharePoint Online](data-encryption-in-odb-and-spo.md) <br/> [Skype for Business Online: Security and Archiving](https://technet.microsoft.com/library/skype-for-business-online-security-and-archiving.aspx) <br/> |
|Email in transit between recipients. This includes email hosted by Exchange Online.  <br/> |Office 365 Message Encryption with Azure Rights Management, S/MIME, and TLS for email in transit  <br/> |[Office 365 Message Encryption (OME)](ome.md) <br/> [Email encryption in Office 365](email-encryption.md) <br/> [How Exchange Online uses TLS to secure email connections in Office 365](exchange-online-uses-tls-to-secure-email-connections.md) <br/> |

## What if I need more control over encryption to meet security and compliance requirements?

In addition to Microsoft-managed solutions of volume encryption, file encryption, and mailbox encryption in Office 365, customer-managed options can be used to meet more stringent security and compliance requirements. Such solutions use Azure Rights Management (Azure RMS) together with Office 365.
  
See the following resources to learn more:
  
- [What is Azure Rights Management?](https://docs.microsoft.com/information-protection/understand-explore/what-is-azure-rms)

- [Activate Rights Management in the Office 365 admin center](https://support.office.com/article/5b6d3ac7-b1ac-428e-b03e-50e882f85a6e)

- [Set up Information Rights Management (IRM) in SharePoint admin center](set-up-irm-in-sp-admin-center.md)

## How do I...

|**To do this task**|**See these resources**|
|:-----|:-----|
|Set up encryption for my organization  <br/> |[Set up encryption in Office 365 Enterprise](set-up-encryption.md) <br/> |
|View details about certificates, technologies, and TLS cipher suites in Office 365  <br/> |[Technical details about encryption in Office 365](technical-reference-details-about-encryption.md) <br/> |
|Work with encrypted messages on a mobile device  <br/> |[View encrypted messages on your Android device](https://support.office.com/article/83d60f17-2305-407a-a762-7d518401fdeb) <br/> [View encrypted messages on your iPhone or iPad](https://support.office.com/article/4d631321-0d26-4bcc-a483-d294dd0b1caf) <br/> |
|Encrypt a document using password protection  <br/><br/>  Currently, password protection is not supported in Office Online. Use desktop versions of Word, Excel, and PowerPoint for password protection.           |[Add or remove protection in your document, workbook, or presentation](https://support.office.com/article/05084cc3-300d-4c1a-8416-38d3e37d6826) (Choose an **Add protection** section, and then see **Encrypt with Password** )  <br/> |
|Remove encryption from a document  <br/> |[Add or remove protection in your document, workbook, or presentation](https://support.office.com/article/05084cc3-300d-4c1a-8416-38d3e37d6826) (Choose a **Remove protection** section, and then see **Remove password encryption** )  <br/> |

## Related topics

[Plan for Office 365 security and information protection capabilities](plan-for-security-and-compliance.md)
  
[Secure your small business](https://docs.microsoft.com/en-us/Office365/Admin/security-and-compliance/secure-your-business-data)
