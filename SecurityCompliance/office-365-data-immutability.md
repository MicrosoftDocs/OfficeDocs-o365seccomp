---
title: "Office 365 Data Immutability"
ms.reviewer: 
ms.author: robmazz
author: robmazz
manager: laurawi
audience: ITPro
ms.topic: article
ms.service: O365-seccomp
localization_priority: Normal
search.appverid:
- MET150
ms.collection:
- Strat_O365_IP
- M365-security-compliance
description: "Defines and explains data immutability in Office 365."
---

# Immutability in Office 365

Regulatory compliance, internal governance requirements, or litigation risks require organizations to preserve email and associated data in a discoverable form. All data in the system must be discoverable and none of it can be destroyed or altered. The industry-standard term for this is "immutability."

Traditional methods for immutability typically worked by moving email messages to a separate, read-only storage location. While such systems serve the purpose of preserving mailbox items for discovery, they often affect the user experience by removing preserved items from the customary daily workflow. For IT professionals, this immutability approach requires the deployment and ongoing maintenance of a separate server and storage infrastructure. Discovery is performed with tools external to the mail system and includes associated deployment and maintenance costs.

Through in-place retention and preservation policy features of archiving in Office 365 and its services, you can preserve and retain many classes of incoming, internal, and outgoing data. THis includes:

- Inbound and outbound email communications
- Books and records contained in email form or in shared online documents
- Meeting requests
- Faxes
- Instant messages
- Documents shared during online meetings
- Voicemails

In addition, Microsoft has developed add-on features to allow [archiving of data](https://support.office.com/article/Archiving-third-party-data-in-Office-365-0ce338d5-3666-4a18-86ab-c6910ff408cc) from other sources through integration with third-party data capturing and management solutions. After third-party data is imported, you can apply Office 365 compliance features to the data, including:

- [Litigation Hold](create-a-litigation-hold.md)
- [In-Place eDiscovery and Hold](manage-legal-investigations.md)
- [Compliance Search](search-for-content.md)
- [In-Place Archiving](enable-archive-mailboxes.md)
- [Mailbox auditing](enable-mailbox-auditing.md)
- [Retention Policies](retention-policies.md)

For example, when a mailbox is placed on Litigation Hold, third-party data is preserved. You can search third-party data using In-Place eDiscovery or Compliance Search. Or you can apply archiving and retention policies to third-party data just like you can for Microsoft data. Archiving third-party data in Office 365 helps your organization stay compliant with government and regulatory policies.

Archiving in Office 365 provides Securities and Exchange Commission (SEC) Rule 17a-4-compliant storage. Office 365 preserves permanent files of all data collected in a non-rewriteable, non-erasable format using in-place retention policies and preservation policies, including preservation lock.

Specifically:

- All records stored using the retention policies noted above are retained in a dedicated storage area out of the purview of the ordinary user. Only authorized users can access and search these records, but cannot alter or erase them.
- Metadata for each item includes a timestamp used in the calculation of retention duration. Timestamps are applied when a new item is received or created and cannot be modified or removed from the metadata.
- Archiving in Office 365 allows users to combine different retention policies and hold actions to create granular retention policies. THese policies define the type or location of the items preserved and the duration of preservation.
- The Preservation Lock feature allows users to choose whether to make the policy a restrictive policy. A restrictive policy prohibits anyone from having the ability to remove, disable, or make any changes to the retention policy. This means that once Preservation Lock is enabled, it cannot be disabled, and no mechanism will exist under which any data from existing custodians that has been collected by the retention policies in place may be overwritten, modified, erased, or deleted during the preservation period. Further, the hold period set by Preservation Lock may not be shortened or decreased. It may, however, be lengthened, in the case of a legal requirement to continue retention of the stored data, as noted above. Preservation Lock ensures that no one, not even administrators or those with certain control access, may change the settings or overwrite or erase data that has been stored, bringing archiving in Office 365 in line with the guidance set forth in the 2003 Release of SEC Rule 17a-4.

To understand how Office 365 helps you meet regulatory obligations, specifically in relation to Rule 17a-4 requirements, see this [whitepaper](https://go.microsoft.com/fwlink/?linkid=830440) that covers Exchange Online Archiving, SharePoint Online, OneDrive for Business, and Skype for Business. The whitepaper also provides an in-depth analysis of Office 365 archiving features and functionalities against each of the requirements under SEC Rule 17a-4 and demonstrates to regulated customers how Office 365 archiving can enable them to meet these requirements.
