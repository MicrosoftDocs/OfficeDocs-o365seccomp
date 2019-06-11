---
title: "Administrative Access Controls in Office 365"
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
description: "Summary: An overview of Office 365's Administrative Access Controls and data categorization."
---

# Administrative Access Controls in Office 365 

Microsoft has invested heavily in systems and controls that automate most Office 365 operations while intentionally limiting access to customer content by Microsoft. Humans govern the service, and software operates the service. This enables Microsoft to manage Office 365 at scale and manage the risks of internal threats to customer content.

By default, Microsoft engineers have zero standing administrative privileges and zero standing access to customer content in Office 365. A Microsoft engineer can have limited, audited, and secured access to a customer's content for a limited amount of time. Access is only when necessary for service operations and only when approved by a member of Microsoft senior management. For Customer Lockbox licensed customers, the customer provides access approval to their content hosted on Office 365.

Microsoft provides online services using multiple forms of cloud delivery:

- **Public Clouds:** Includes multi-tenant versions of Office 365, Azure, and other services hosted in North America, South America, Europe, Asia, Australia, etc.
- **National Clouds:** Includes all sovereign and third party-operated clouds outside of the United States (except ones noted previously), such as Office 365 in China (operated by 21Vianet), and Office 365 in Germany (operated by Microsoft, but under a model in which a German data trustee, Deutsche Telekom, controls and monitors Microsoft's access to Customer Data and systems that contain Customer Data).
- **Government Clouds:** Includes Office 365 and Azure services that are available to United States government customers.

For purposes of this article, Office 365 services include:

- [Exchange Online](https://docs.microsoft.com/Exchange/exchange-online)
- [Exchange Online Protection](https://docs.microsoft.com/Office365/SecurityCompliance/eop/exchange-online-protection-overview)
- [SharePoint Online](https://docs.microsoft.com/sharepoint/sharepoint-online)
- [OneDrive for Business](https://docs.microsoft.com/OneDrive/onedrive)
- [Skype for Business](https://docs.microsoft.com/SkypeForBusiness/skype-for-business-online)
- [Microsoft Teams](https://docs.microsoft.com/MicrosoftTeams/Teams-overview)
- [Yammer](https://docs.microsoft.com/yammer/yammer-landing-page)

## Office 365 Access Controls

For access control purposes, Microsoft categorizes Office 365 data as Customer data or other types of data.

### Customer data

Customer data is all data provided by or on behalf of a customer when using Office 365 services. This is customer content directly created or uploaded by Office 365 users, including:

- Emails
- SharePoint Online content
- Instant messages
- Calendar items
- Documents
- Contacts
- End-user identifiable information (EUII) (data that is unique to a user or that is linkable to an individual user but does not include customer content).

### Other types of data

Other types of data include:

- **Account data:** Includes administrative data (information provided by administrators when they sign-up or purchase services), and payment data (information about payment instruments, such as credit card details).
- **Organizationally identifiable information:** Includes data used to identify a tenant, usage data, and not linkable to an individual user or included in customer content.
- **System metadata:** Includes service logs that contain configuration settings, system status, Microsoft IP addresses, and technical information about subscriptions and tenants.

Microsoft has established access control mechanisms to ensure that no one has unapproved access to Customer Data or access control data. Access control data manages access to other types of data or functions within the environment, including access to customer content or EUII, Microsoft passwords, security certificates, and other authentication-related data. Access control mechanisms also guard against unapproved physical, logical, or remote access to the Office 365 production environment.

There are three categories of access controls used by Microsoft for operating Office 365:

- Isolation Controls
- Personnel Controls
- Technology Controls

When combined, these controls help prevent and detect malicious actions in Office 365. In addition to the isolation, personnel, and technology controls used by Microsoft, there is a fourth category of controls: those implemented by customers.

Office 365 allows you to manage data the same way data is managed in on-premises environments. The person who signs up an organization for Office 365 automatically becomes a global administrator. The global admin has access to all features in Management Portals and can:

- Create or edit users
- Assign admin roles to others
- Reset user passwords
- Manage user licenses
- Manage domains
- Approve Customer Lockbox requests

We recommend that each organization configure at least two admin accounts. For large enterprise organizations, we recommend specialized admin accounts that serve different functions.

For information about assigning admin roles and permissions, see [Assigning admin roles in Office 365](https://support.office.com/article/Assigning-admin-roles-in-Office-365-eac4d046-1afd-4f1a-85fc-8219c79e1504) and [About Office 365 admin roles](https://support.office.com/article/Permissions-in-Office-365-DA585EEA-F576-4F55-A1E0-87090B6AAA9D).

## Related Links

- [Isolation Controls](office-365-isolation-controls.md)
- [Personnel Controls](office-365-personnel-controls.md)
- [Technology Controls](office-365-technology-controls.md)
- [Monitoring and Auditing Access Controls](office-365-monitoring-and-auditing-access-controls.md)
- [Yammer Enterprise Access Controls](office-365-yammer-enterprise-access-controls.md)
