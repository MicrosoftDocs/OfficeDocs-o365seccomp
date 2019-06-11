---
title: "Run an administrator role group report in EOP "
ms.reviewer: 
ms.author: markjjo
author: markjjo
manager: laurawi
ms.date: 11/17/2014
audience: ITPro
ms.topic: article
ms.service: O365-seccomp
localization_priority: Normal
ms.assetid: 23b47b57-0eec-46a3-a03b-366ea014ab31
description: "When an administrator adds members to or removes members from administrator role groups, Microsoft Exchange Online Protection (EOP) logs each occurrence."
---

# Run an administrator role group report in EOP 

 When an administrator adds members to or removes members from administrator role groups, Microsoft Exchange Online Protection (EOP) logs each occurrence. When you run an administrator role group report in the Exchange admin center, entries are displayed as search results and include the role groups affected, who changed the role group membership and when, and what membership updates were made. Use this report to monitor changes to the administrative permissions assigned to users in your organization.
  
## What do you need to know before you begin?

- Estimated time to complete: 2 minutes
    
- You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Reports" section of the [Feature permissions in EOP](feature-permissions-in-eop.md) topic. 
    
- For information about keyboard shortcuts that may apply to the procedures in this topic, see **Keyboard shortcuts in the Exchange admin center**.
    
> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at [Exchange Server](https://go.microsoft.com/fwlink/p/?linkId=60612),[Exchange Online](https://go.microsoft.com/fwlink/p/?linkId=267542), or [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkId=285351). 
  
## Use the EAC to run an administrator role group report

Run the administrator role group report to find the changes to management role groups in your organization within a particular timeframe.
  
1. In the EAC, navigate to **Compliance management** \> **Auditing**, and choose **Run an administrator role group report**.
    
2. Choose the **Start date** and **End date**. By default, the report searches for changes made to administrator role groups in the past two weeks.
    
3. To view the changes for a specific role group, click **Select role groups**. Select the role group (or groups) in the subsequent dialog box, and click **OK**. You can also leave the field blank to find all changed role groups.
    
4. Click **Search**.
    
If any changes are found using the criteria you specified, they will appear in the results pane. Click a role group in the search results to see the changes in the details pane.
  
## How do you know this worked?

If you've successfully run an administrator role group report, role groups that have been changed within the date range are displayed in the search results pane. If there are no results, then no changes to role groups have taken place within the specified date range. If you think there should be results, change the date range and then run the report again.
  
## Monitor changes to role group membership

When members are added to or removed from a role group, the search results displayed in the details pane indicate that the role group membership was updated and lists the current members. The results don't explicitly state which user was added or removed.
  
To determine if a user was added or removed, you have to compare two separate entries in the report. For example, let's look at the following log entries for the **HelpDesk** role group: 
  
 **1/27/2013 4:43 PM**
  
 **Administrator**
  
 **Updated members: Administrator;annb,florencef;pilarp**
  
 **2/06/2013 10:09 AM**
  
 **Administrator**
  
 **Updated members: Administrator;annb;florencef;pilarp;tonip**
  
 **2/19/2013 2:12 PM**
  
 **Administrator**
  
 **Updated members: Administrator;annb;florencef;tonip**
  
In this example, the Administrator user account made the following changes:
  
- On 2/06/2013, it added the user tonip.
    
- On 2/19/2013, it removed the user pilarp.
    

