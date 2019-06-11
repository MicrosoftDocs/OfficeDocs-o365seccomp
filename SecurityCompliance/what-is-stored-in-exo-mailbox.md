---
title: "Content stored in Exchange Online mailboxes"
ms.reviewer: 
ms.author: markjjo
author: markjjo
manager: laurawi
audience: Admin
ms.topic: article
ms.service: O365-seccomp
localization_priority: Normal
ms.collection: M365-security-compliance
search.appverid:
- MOE150
- MED150
- MET150
ms.assetid:
ROBOTS: NOINDEX, NOFOLLOW 
description: "Data produced by cloud-based apps in Office 365 is stored in a user's Exchange Online mailbox in the Microsoft cloud."
---

# Content stored in Exchange Online mailboxes

A mailbox in Exchange Online is primarily used to store email-related items such as messages, calendar items, tasks, and notes. But that's changing as more cloud-based Office 365 apps also store their data in a user's mailbox. One advantage of storing data in a mailbox is that you can use the search tools in Content Search, eDiscovery, Advanced eDiscovery, and Data Investigations to find, view, and export the data from these cloud-based apps. Note that the data from some of these apps is stored in hidden folders located in a non-interpersonal message (non-IPM) subtree in the mailbox. This means the data is hidden from the user's view when they use Outlook or other mail clients to access their mailbox.

The following table lists the Office 365 apps that store data in a cloud-based mailbox. The table also describes the type of content that each app stores.

|Office 365 app  |Description  |
|:---------|:---------|
|Forms     <br/> |Forms (stored as a PDF file) and responses to a form (stored in a CSV file) are attached to email messages and stored in a hidden folder in the mailbox of the user who created the form. When you export content from Forms in a PST file, this data is located in the **ApplicationDataRoot** folder in a subfolder that is named with the following globally unique identified (GUID): **c9a559d2-7aab-4f13-a6ed-e7e9c52aec87**.        <br/> |
|MyAnalytics    <br/> |   MyAnalytics provides users with insights about how they spend their time based on the mail and calendar data in their mailbox. This data is stored in the user's mailbox in a hidden folder. For more information MyAnalytics data and how to export it, see [Exporting data from MyAnalytics](manage-gdpr-data-subject-requests-with-the-dsr-case-tool.md#exporting-data-from-myanalytics-and-the-office-roaming-service).      <br/> |
|Office 365 Groups    <br/>|  Email messages, calendar items, contacts (People), notes, and tasks are stored in the mailbox that's associated with an Office 365 group.       <br/> |
|Outlook/Exchange Online<br/>|  Email messages, calendar items, contacts (People), notes, and tasks are stored in a user's mailbox.       <br/> |
|People    <br/> |  Contacts in the People app (which are the same contacts as the ones accessible in Outlook) are stored in a user's mailbox.      <br/> |
|Planner     <br/> |   Plans created in Planner are stored in the mailbox of the corresponding Office 365 Group that is provisioned when a new plan is created. The alias for the group mailbox is the name of the plan.      <br/> |
|Skype for Business    <br/>  | Conversations in Skype for Business are stored in the Conversation History folder in a user's mailbox. If the mailbox of a participant of a Skype meeting is placed on Litigation Hold or assigned to a retention policy, files attached to a meeting are retained in the participants mailbox.         <br/> |
|Sway     <br/> |  Sways are stored as an HTML file that is attached to an email message and stored in a hidden folder in the mailbox of the user who created the sway. When you export content from Sway in a PST file, this data is located in the **ApplicationDataRoot** folder in a subfolder that is named with the following GUID) **905fcf26-4eb7-48a0-9ff0-8dcc7194b5ba**.       <br/> |
|Tasks    <br/> |  Tasks in the Tasks app (which are the same tasks as the ones accessible in Outlook) are stored in a user's mailbox.       <br/> |
|Teams    <br/>  |Conversations that are part of a Teams channel are stored in the mailbox that's associated with the Team. Conversations that are part of the Chat list in Teams (also called *1 x N chats*) are stored in the mailbox of the users who participate in the chat. Additionally, summary information for meetings and calls in a Teams channel are stored in the mailboxes of users who dialed into the meeting or call. <br/> | 
|To-Do  <br/> | Tasks (called *to-dos*, which are saved in to-do lists) in the To-Do app are stored in a user's mailbox.        <br/> |
||||

> [!NOTE]
> Currently, if a hold is placed on a mailbox (by using holds in eDiscovery and Advanced eDiscovery cases), content from Forms and Sway will not be preserved by the hold. 
