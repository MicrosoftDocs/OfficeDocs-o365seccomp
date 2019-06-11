---
title: "Overview of inactive mailboxes in Office 365"
ms.reviewer: 
ms.author: markjjo
author: markjjo
manager: laurawi
ms.date: 
audience: Admin
ms.topic: overview
ms.service: O365-seccomp
localization_priority: Normal
ms.collection: 
- Strat_O365_IP
- M365-security-compliance
search.appverid: 
- MOE150
- MET150
ms.assetid: 1fbd74e8-7a60-4157-afe8-fe79f05d2038
description: "Learn about retaining mailbox content for former employees by turning the mailbox into an inactive mailbox. You can do this by placing the mailbox on Litigation Hold or applying an Office 365 retention policy to the mailbox and then removing the corresponding Office 365 account."
---

# Overview of inactive mailboxes in Office 365

Your organization might need to retain former employees' email after they leave the organization. Depending on your organization's retention requirements, you might need to retain mailbox content for a few months or years after employment ends, or you might need to retain mailbox content indefinitely. Regardless of how long you need to retain email, you can create inactive mailboxes in Office 365 to retain the mailbox of former employees. 
  
## What are inactive mailboxes?

When an employee leaves your organization (or goes on an extended leave of absence), you can remove their Office 365 account. The employee's mailbox data is retained for 30 days after the account is removed. During this period, you can still recover the mailbox data by undeleting the account. After 30 days, the data is permanently removed.
  
But if your organization needs to retain mailbox content for former employees, you can turn the mailbox into an inactive mailbox by placing the mailbox on Litigation Hold or applying an Office 365 retention policy to the mailbox in the Security & Compliance Center and then removing the corresponding Office 365 account. The contents of an inactive mailbox are retained for the duration of the Litigation Hold placed on the mailbox or the retention period of the Office 365 retention policy applied to it before the mailbox was deleted. You can still recover the corresponding user account for a 30-day period. However, after 30 days, the inactive mailbox is retained in Office 365 until the hold or retention policy is removed. 
  
> [!NOTE]
> We've postponed the July 1, 2017 deadline for creating new In-Place Holds to make a mailbox inactive. But later this year or early next year, you won't be able to create new In-Place Holds in Exchange Online. At that time, only Litigation Holds and Office 365 retention policies can be used to create an inactive mailbox. However, existing inactive mailboxes that are on In-Place Hold will still be supported, and you can continue to manage the In-Place Holds on inactive mailboxes. This includes changing the duration of an In-Place Hold and permanently deleting an inactive mailbox by removing the In-Place Hold. 
 
  
## Inactive mailboxes and Office 365 retention policies

In addition to Litigation Hold, using the new Office 365 retention policy feature in the Security & Compliance Center is another way to make a mailbox inactive. To use a retention policy to make an inactive mailbox: 
  
- It has to be configured to retain content or retain and then delete content. If a retention policy is configured to just delete content, a mailbox that the policy is applied to won't become inactive when the mailbox is deleted.

- It has to be applied to Exchange mailboxes or Skype for Business locations (because Skype-related content is stored in the user's mailbox). 
    
- It can be query-based so that it retains only items that match a search query. 
    
For more information about configuring Office 365 retention policies, see [Overview of retention policies in Office 365](retention-policies.md).
  
If you use a retention policy to make an inactive mailbox, Office 365 will continue to process the retention policy on the inactive mailbox. This means if the retention policy is configured to retain and then delete content, items will be moved to the Recoverable Items folder when the retention duration expires, and then eventually purged from the inactive mailbox. If the Office 365 retention policy isn't configured to deleted items, then items that haven't been permanently deleted by the user (before the mailbox was made inactive) won't be moved to the Recoverable Items folder and will be retained indefinitely after the mailbox becomes inactive. 
  
You might consider creating an Office 365 retention policy specifically for inactive mailboxes. Here are some reasons for doing this and things to keep in mind.
  
- You can configure the retention policy to retain mailbox content only as long as necessary to meet your organization's requirement for former employees.
    
- It's a good way to identify inactive mailboxes because the retention policy will only be applied to inactive mailboxes.
    
- You'll be able to quickly identify the retention policy that's assigned to inactive mailboxes in your organization. This will make it easier to change the retention (or deletion) settings if necessary. It will also make it easier to permanently delete an inactive mailbox because you can just remove it from the policy by using the Security & Compliance Center. Otherwise, you have to use Exchange Online PowerShell to remove a Litigation Hold from an inactive mailbox or use Security & Compliance Center PowerShell to exclude an inactive mailbox from an organization-wide Office 365 retention policy.
    
- If you create an Office 365 retention policy specifically for inactive mailboxes, you can add a maximum of 1,000 mailboxes to the policy. If you're a very large organization, you might have to create more than one Office 365 retention policy to use for inactive mailboxes.

> [!CAUTION]
> If you use a retention policy to make a mailbox inactive, do not change or remove the user principal name (UPN) for the mailbox before you delete the corresponding Office 365 user account. Additionally, do not change the primary SMTP address (that's derived from the UPN) or remove this email address from the list of secondary SMTP addresses associated with the mailbox before making the mailbox inactive. If you change the UPN or email addresses (that were assigned to the mailbox at the time the retention policy was applied to it) and then delete the user account to make the mailbox inactive, you won't be able to delete the inactive mailbox when you no longer need to retain it. That's because you can't remove the inactive mailbox from the retention policy using a UPN or email address (to identify the inactive mailbox) that's different than the ones that existed when the retention policy was initially applied to the mailbox. For more information about deleting inactive mailboxes, see [Delete an inactive mailbox in Office 365](delete-an-inactive-mailbox.md).
  
## Inactive mailboxes and eDiscovery case holds

If a hold that's associated with an eDiscovery case in the Security & Compliance Center is placed on a mailbox and then the mailbox or the user's Office 365 account is deleted, the mailbox will become an inactive mailbox. However, we don't recommend using eDiscovery case holds to make a mailbox inactive. That's because eDiscovery cases are intended for specific, time-bound cases related to a legal issue. At some point, a legal case will probably end and the holds associated with the case will be removed and the eDiscovery case will be closed. In fact, if a hold that's placed on an inactive mailbox is associated with an eDiscovery case, and then the hold is released or the eDiscovery case is closed (or deleted), the inactive mailbox will be permanently deleted. Additionally, you can't create a time-based eDiscovery hold. That's means content in an inactive mailbox will be retained forever or until the hold is removed and the inactive mailbox is deleted. Therefore, we recommend using a Litigation Hold or an Office 365 retention policy for inactive mailboxes.
  
For more information about eDiscovery cases and holds, see [eDiscovery cases](ediscovery-cases.md).
  
## Inactive mailboxes and Office 365 labels

Labels in Office 365 help you classify email data in your organization for governance, and enforce retention rules based on that classification. A label can be applied to an email item either manually by users or automatically by administrators, and an email item can only have single label assigned to it. If a single email item in a user's mailbox has a label assigned to it (and it's configured to retain or retain and then delete the item) and the mailbox or the user's Office 365 account is deleted, the mailbox will become an inactive mailbox. Similar to eDiscovery case holds, we don't recommend using labels to make a mailbox inactive. Instead, we recommend that you use a Litigation Hold or an Office 365 retention policy. Be aware that in the case of labels, you might not realize that a label has been applied to an email item and then inadvertently make an inactive mailbox when you delete the user's account. 
  
For more information about labels, see [Overview of labels in Office 365](labels.md).
  
## Inactive mailboxes and Exchange MRM retention policies

If an Exchange retention policy (the Messaging Records Management, or MRM, feature in Exchange Online) was applied to mailbox when it was made inactive, any deletion policies (which are retention tags configured with a **Delete** retention action) will continue to be processed on the inactive mailbox. That means items that are tagged with a deletion policy will be moved to the Recoverable Items folder when the retention period expires. Those items are purged from the inactive mailbox when the hold duration expires. If a hold duration isn't specified for the inactive mailbox, items in the Recover Items folder will be retained indefinitely. 
  
Conversely, any archive policies (which are retention tags configured with a **MoveToArchive** retention action) that are included in the retention policy assigned to an inactive mailbox are ignored. That means items in an inactive mailbox that are tagged with an archive policy will remain in the primary mailbox when the retention period expires. They're not moved to the archive mailbox or to the Recoverable Items folder in the archive mailbox. They will be retained indefinitely. 
  
## Creating an inactive mailbox

To make a mailbox inactive, it must be assigned an Exchange Online (Plan 2) license so that a Litigation Hold or Office 365 retention policy can be applied to the mailbox before it's deleted. After the mailbox is deleted, the Exchange Online license that was associated with it will be available to assign to a new user. Inactive mailboxes don't require ongoing licenses.
  
The following table summarizes the process of making an inactive mailbox for different retention scenarios. For more information, see [Manage inactive mailboxes in Office 365](create-and-manage-inactive-mailboxes.md).
  
|**To…**|**Do this...**|**Result**|
|:-----|:-----|:-----|
|Retain mailbox content indefinitely after an employee leaves the organization  <br/> | Place the mailbox on Litigation Hold or apply an Office 365 retention policy (that's configured to retain content) to the mailbox.  <br/>  Don't specify a hold duration for the Litigation Hold or don't configure the Office 365 retention policy to delete items; alternatively you can use a retention policy that retains items forever.  <br/>  Remove the user's Office 365 account.  <br/> |All content in the inactive mailbox, including items in the Recoverable Items folder, is retained indefinitely.  <br/> |
|Retain mailbox content for a specific period after an employee leaves the organization and then delete it  <br/> | Apply an Office 365 retention policy to the mailbox.  <br/>  Configure the retention policy to retain and then delete items when the retention period expires.  <br/>  Remove the user's Office 365 account.  <br/> |When the retention period for a mailbox item expires, the item is moved to the Recoverable Items folder and then it's permanently deleted (purged) from the inactive mailbox when the deleted item retention period (for Exchange mailboxes) expires. The retention period of the Office 365 retention policy can be configured based on the original date a mailbox item was received or created, or when it was last modified.  <br/> |
   
**NOTE:** If a Litigation Hold is already placed on a mailbox, or if an Office 365 retention policy (that's configured to retain or retain and then delete content) is already applied to the mailbox, then all you have to do is delete the corresponding Office 365 user account to create an inactive mailbox. 
  
## Managing inactive mailboxes

After you make a mailbox inactive, you can perform various management tasks on inactive mailboxes.
  
- **Change the hold duration for an inactive mailbox** After a mailbox is made inactive, you can change the hold duration of the Litigation Hold or Office 365 retention policy applied to the inactive mailbox. For step-by-step procedures, see [Change the hold duration for an inactive mailbox in Office 365](change-the-hold-duration-for-an-inactive-mailbox.md).

  > [!NOTE]
  > You can't apply other retention policies to an inactive mailbox. You can only change the retention duration of an existing retention policy applied to the inactive mailbox.
    
- **Recover an inactive mailbox** If a former employee (or an employee on a leave of absence) returns to your organization, or if a new employee is hired to take on the job responsibilities of the former employee, you can recover the contents of the inactive mailbox. When you recover an inactive mailbox, the mailbox is converted to a new mailbox, the contents and folder structure of the inactive mailbox are retained, and the mailbox is linked to a new user account. After it's recovered, the inactive mailbox no longer exists. For step-by-step procedures and information about what happens when you recover an inactive mailbox, see [Recover an inactive mailbox in Office 365](recover-an-inactive-mailbox.md).
    
- **Restore an inactive mailbox** If another employee takes on the job responsibilities of a former employee, or if another person needs access to the contents of the inactive mailbox, you can restore (or merge) the contents of the inactive mailbox to an existing mailbox. When you restore an inactive mailbox, the contents are copied to another mailbox. The inactive mailbox is retained and remains an inactive mailbox. The inactive mailbox can still be searched using eDiscovery tools, its contents can be restored to another mailbox, and it can be recovered or deleted at a later date. For step-by-step procedures, see [Restore an inactive mailbox in Office 365](restore-an-inactive-mailbox.md).
    
- **Delete an inactive mailbox** When you no longer need to retain the contents of an inactive mailbox, you can permanently delete it by removing all holds or Office 365 retention policies applied to the inactive mailbox. If a mailbox was made inactive more than 30 days ago, it will be marked for permanent deletion after you remove the hold. If the mailbox was made inactive within the last 30 days, you can make it active again after removing the hold or retention policy. For step-by-step procedures, see [Delete an inactive mailbox in Office 365](delete-an-inactive-mailbox.md).
