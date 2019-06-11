---
title: "Use the communications editor"
ms.reviewer: 
ms.author: markjjo
author: markjjo
manager: laurawi
ms.date: 
audience: Admin
ms.topic: article
ms.service: O365-seccomp
localization_priority: Normal
ms.collection: M365-security-compliance 
search.appverid: 
- MOE150
- MET150
ms.assetid: 

description: ""
---

# Use the communications editor

As you define the content of your portal content, legal hold notifications, and related reminders/escalations, you can leverage the Communications Editor to format and dynamically customize your content.

## Rich text editor 

The Communications Editor allows user to customize the text using the editor options. For example, users can change font types, create bulleted lists, highlight content, and more. 

## Merge field variables

You can leverage email merge variables from the Communications Editor to embed customized custodian attributes into a communication's body text. When sent to the custodian, the merge field will be populated with the corresponding field. For example, when sent to custodian John Smith, the merge field [Custodian Name] would be translated with the corresponding name. 

You can use email merge fields by selecting the **Merge field** icons on the top of the rich-text editor control. The placeholder will be added based off the location of the users' cursor. 

### List of merge field variables

| Field name                  | Field details | 
| :------------------- | :------------------- |
| Display Name  | The custodian's first and last name. | 
| Acknowledgement Link | A customized link to record each custodian's acknowledgement.|                 |
| Portal Link     | A customized link for the custodian's Compliance Portal.|                |
| Issuing Officer                   | The email address of the specified issuing officer.|                   |
| Issuing Date                   | The date that the notice was issued (UTC).              |
