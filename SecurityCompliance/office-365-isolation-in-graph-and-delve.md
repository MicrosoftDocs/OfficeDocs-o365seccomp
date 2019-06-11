---
title: "Office 365 Tenant Isolation in the Office Graph and Delve"
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
description: "Summary: An explanation of tenant isolation in the Office Graph and in Delve."
---

# Tenant Isolation in the Office Graph and Delve

## Tenant Isolation in the Office Graph
The [Office Graph](https://dev.office.com/officegraph) models activity in Office 365 services, including Exchange Online, SharePoint Online, Yammer, Skype for Business, Azure Active Directory, and more, and in external services, such as other Microsoft services or third-party services. Office Graph components are used throughout Office 365. The Office Graph represents a collection of content and activity, and the relationships between them that happen across the entire Office suite. It uses sophisticated machine learning techniques to connect people to the relevant content, conversations and people around them. For example, the tenant index in SharePoint Online has an Office Graph index that is used to serve Delve queries, the Analytics Processing Engine in SharePoint Online is used to store signals and calculate insights, and Exchange Online calculates each user's recipient cache as input into tenant analytics.

The Office Graph contains information about enterprise objects, such as people and documents, as well as the relationships and interactions among these objects. The relationships and interactions are represented as *edges*. The Office Graph is segmented by tenant such that edges can only exist between *nodes* in the same tenancy. A *node* is an entity with a Uniform Resource Identifier (URI), node type, access control list, and a set of facets containing *metadata* and edges. Each node has associated metadata and edges, arranged into *facets* as in the Common Knowledge Model. *Metadata* are named properties stored on a node which can be used for searching, filtering, or analysis within the office graph. A *facet* is a logical collection of metadata and edges on a node. Each facet describes one aspect of a node. 

The Office Graph does not bring all the data into a single repository; rather, it stores metadata and relationships about data that lives elsewhere. The Office Graph consists of several data stores and processing components:
- The Tenant Graph Store provides bulk storage optimized for efficient analytics.
- The Active Content Cache provides quick random access to active node and edges to drive user experiences.
- The input router notifies components internal and external of changes to the tenant graph.

Analytics within each workload deduce insights relevant to the tenant-wide calculations and push them to the tenant graph. Tenant analytics reasons over all activity in a tenancy to produce insights into patterns of behavior. For example, Exchange Online calculates the recipient cache for each user with analytics that efficiently reason over each user's mailbox. These per-user analytics produce a set of *RecipientCache Edges* on each person, which are in turn pushed to the tenant graph. This keeps the as much of the analytics processing as close to the source data as possible.

## Tenant Isolation in Delve
As mentioned previously, the Office Graph powers experiences that help people discover and collaborate on current activities in their enterprise, and provides an entity-centric platform for analytics to reason over content and activity across workloads and beyond Office 365. Delve is the first such experience powered by the Office Graph.
Delve is an Office 365 web experience that surfaces content from Office 365 and Yammer Enterprise to Office 365 users via the Office Graph. The web experience displays data as different boards, each with a certain topic, such as *Trending around me* or *Modified by me*. Each board consists of several document cards that display summary text and a picture from the document. The card lets users do things like open the document or a Yammer page for the document. There is a page for each person in an Office 365 tenant that displays the most relevant documents for this person, and icons that can invoke Exchange Online or Skype for Business for interacting with that person. Because Delve is based on the Office Graph API, it is bound by the tenant-based isolation of that API.
