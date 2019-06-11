---
title: "Office 365 Isolation Controls"
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
description: "Summary: An explanation of isolation controls within Office 365."
---

# Office 365 Isolation Controls 

Microsoft continuously works to ensure that the multi-tenant architecture of Office 365 supports enterprise-level security, confidentiality, privacy, integrity, local, international, and availability [standards](https://www.microsoft.com/TrustCenter/Compliance?service=Office#Icons). The scale and the scope of services provided by Microsoft make it difficult and non-economical to manage Office 365 with significant human interaction. Office 365 services are provided through multiple globally distributed data centers, each highly automated with few operations requiring a human touch or any access to customer content. Our staff supports these services and data centers using automated tools and highly secure remote access. For some of the details about how large-scale services are operated in Office 365, see [a behind the scenes look at Office 365 for IT Pros](https://channel9.msdn.com/Events/SharePoint-Conference/2014/SPC202).

Office 365 is composed of multiple services that provide important business functionality and contribute to the entire Office 365 experience. Each of these services is self-contained and designed to integrate with one another.

Office 365 is designed with the following principles:

 - **[Service-Oriented Architecture](https://msdn.microsoft.com/library/aa480021.aspx):** designing and developing software in the form of interoperable services providing well-defined business functionality.
 - **[Operational Security Assurance](http://www.microsoft.com/download/details.aspx?id=40872):** a framework that incorporates the knowledge gained through various capabilities that are unique to Microsoft, including the Microsoft [Security Development Lifecycle](https://www.microsoft.com/sdl/default.aspx), the [Microsoft Security Response Center](https://technet.microsoft.com/library/dn440717.aspx), and deep awareness of the cybersecurity threat landscape.

Office 365 services inter-operate with each other, but are designed and implemented so they can be deployed and operated as autonomous services, independent of each other. Microsoft segregates duties and areas of responsibility for Office 365 to reduce opportunities for unauthorized or unintentional modification or misuse of the organization's assets. Office 365 teams have defined roles as part of a comprehensive role-based access control mechanism.

## Customer content isolation

All customer content in a tenant is isolated from other tenants and from operations and systems data used in the management of Office 365. Multiple forms of protection are implemented throughout Office 365 to minimize the risk of compromise of any Office 365 service or application. Multiple forms of protection also prevent unauthorized access to the information of tenants or the Office 365 system itself.

For information about how Microsoft implements logical isolation of tenant data within Office 365, see [Tenant Isolation in Office 365](office-365-tenant-isolation-overview.md).
