---
title: "Give users access to the Office 365 Security &amp; Compliance Center"
ms.reviewer: 
ms.author: stephow
author: stephow-MSFT
manager: laurawi
ms.date: 
audience: Admin
ms.topic: article
f1_keywords:
- 'ms.o365.cc.PermissionsHelp'
ms.service: O365-seccomp
localization_priority: Normal
ms.collection: Strat_O365_IP
search.appverid: 
- MOE150
- MET150
ms.assetid: 2cfce2c8-20c5-47f9-afc4-24b059c1bd76
description: "Users need to be assigned permissions in the Office 365 Security &amp; Compliance Center before they can manage any of its security or compliance features."
---

# Give users access to the Office 365 Security &amp; Compliance Center

Users need to be assigned permissions in the Office 365 Security &amp; Compliance Center before they can manage any of its security or compliance features. As an Office 365 global admin or member of the OrganizationManagement role group in the Security &amp; Compliance Center, you can give these permissions to users. Users will only be able to manage the security or compliance features that you give them access to. 
  
For more information about the different permissions you can give to users in the Security &amp; Compliance Center, check out [Permissions in the Office 365 Security &amp; Compliance Center](permissions-in-the-security-and-compliance-center.md).
  
## What do you need to know before you begin?

- You need to be an Office 365 global admin, or a member of the OrganizationManagement role group in the Security &amp; Compliance Center, to complete the steps in this article.
    
- Role groups for the Security &amp; Compliance Center might have similar names to the role groups in Exchange Online, but they're not the same. 
    
- Role group memberships aren't shared between Exchange Online and the Security &amp; Compliance Center.
    
## Use the Office 365 admin center to give another user access to the Security &amp; Compliance Center

1. [Sign in to Office 365 and go to the Admin center](https://go.microsoft.com/fwlink/p/?LinkId=525275).
    
2. In the Office 365 admin center, open **Admin centers** and then click **Security &amp; Compliance**. 
    
3. In the Security &amp; Compliance Center, go to **Permissions**.
    
4. From the list, choose the role group that you want to add the user to and click **Edit** ![Edit icon](media/O365_MDM_CreatePolicy_EditIcon.gif).
    
5. In the role group's properties page under **Members**, click **Add**![Add Icon](media/ITPro-EAC-AddIcon.gif) and select the name of the user (or users) you want to add. 
    
6. When you've selected all of the users you want to add to the role group, click **add-\>** and then **OK**.
    
7. Click **Save** to save the changes to the role group. 
    
### How do you know this worked?

1. In the Security &amp; Compliance Center, go to **Permissions**.
    
2. From the list, select the role group to view the members.
    
3. On the right, in the role group details, you can view the members of the role group.
    
## Use PowerShell to give another user access to the Security &amp; Compliance Center

1. [Connect to Office 365 Security & Compliance Center PowerShell](https://docs.microsoft.com/en-us/powershell/exchange/office-365-scc/connect-to-scc-powershell/connect-to-scc-powershell?view=exchange-ps).
    
2. Use the **Add-RoleGroupMember** command to add a user to the Organization Management Role, as shown in the following example. 
    
  ```
  Add-RoleGroupMember -Identity "OrganizationManagement" -Member MatildaS
  
  ```

 **Parameters**
  
- _-Identity_ is the role group to add a member to. 
    
- _Member_ is the mailbox, universal security group (USG), or computer to add to the role group. You can specify only one member at a time. 
    
For detailed information on syntax and parameters, see [Add-RoleGroupMember](https://go.microsoft.com/fwlink/p/?LinkId=510859).
  
### How do you know this worked?

To verify that you've given users access to the Security &amp; Compliance Center, use the **Get-RoleGroupMember** cmdlet to view the members in the Organization Management role group, as shown in the following example. 
  
```
Get-RoleGroupMember -Identity "OrganizationManagement"

```

For detailed information on syntax and parameters, see [Get-RoleGroupMember](https://go.microsoft.com/fwlink/p/?LinkId=510860).
  

