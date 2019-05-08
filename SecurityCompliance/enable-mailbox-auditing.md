---
title: "Manage mailbox auditing"
ms.author: chrisda
author: chrisda
manager: serdars
ms.audience: Admin
ms.topic: article
ms.service: O365-seccomp
localization_priority: Normal
ms.collection: 
- Strat_O365_IP
- M365-security-compliance
search.appverid: 
- MOE150
- MET150
ms.assetid: aaca8987-5b62-458b-9882-c28476a66918
description: "Mailbox audit logging is turned on by default in Microsoft 365 (also called default mailbox auditing or mailbox auditing on by default). This means that certain actions performed by mailbox owners, delegates, and administrators are automatically logged in a mailbox audit log, where you can search for activities performed on the mailbox."
---

# Manage mailbox auditing
  
Starting in January 2019, Microsoft is turning on mailbox audit logging by default for all Microsoft 365 organizations. This means that certain actions performed by mailbox owners, delegates, and administrators are automatically logged, and the corresponding mailbox audit records will be available when you search for them in the mailbox audit log. Before mailbox auditing was turned off by default, you had to manually enable it for every user mailbox in your organization. 

Here are some benefits of mailbox auditing on by default:

- Auditing will be enabled by default when you create a new mailbox. You won't have to manually enable it for new users. 

- You won't have manage the mailbox actions that are audited. A defined set of mailbox actions are audited by default for each type of logon. These [logon types](#mailbox-actions-logged-by-default) are Owner, Delegate, and Admin.

- New mailbox actions released by Microsoft will be audited by default. When Microsoft releases a new mailbox action (particularly ones that help protect your organization and help with forensic investigations), it will automatically be added to the list of mailbox actions audited by default. This means you don't have to add new actions to the list of mailbox actions performed by owners, delegates, or admins. 

- Ensure that you're auditing the same actions for all mailboxes so you have a consistent mailbox auditing policy across your organization.

> [!TIP]
> The important thing to remember is that with the release of mailbox auditing on by default, you don't have to do anything to manage mailbox auditing. However, if you want to learn more, change the behavior from the default settings, or turn it off altogether, this article can help you with that.

## Verify mailbox auditing on by default is turned on

To verify that mailbox auditing on by default is turned on for your organization, run the following command in  [Exchange Online PowerShell](https://docs.microsoft.com/powershell/exchange/exchange-online/connect-to-exchange-online-powershell/connect-to-exchange-online-powershell):

```
Get-OrganizationConfig | FL AuditDisabled
``` 

A value of **False** indicates that mailbox auditing on by default is enabled for your organization. 

When mailbox auditing on by default is turned on (when the *AuditDisabled* property is set to **False**), the organizational setting will override the mailbox auditing setting for a specific mailbox. For example, if the *AuditEnabled* property for a mailbox is set to **False**, but mailbox auditing on by default is enabled for your organization, the default mailbox actions will be audited for that mailbox. If mailbox auditing was explicitly disabled for a specific mailbox and you still want it disabled, you can set up mailbox auditing bypass for the mailbox owner and other users who have been delegated access to the mailbox. For more information, see the [Bypass mailbox audit logging](#bypass-mailbox-audit-logging) section in this article.

> [!NOTE]
> When mailbox auditing on by default is turned on, the *AuditEnabled* property for a mailbox won't be changed to **True** if it was currently set to **False**. In other words, mailbox auditing on by default ignores the *AuditEnabled* property for a mailbox.

## Supported mailbox types

The following table shows the mailbox types that are currently supported by mailbox auditing on by default:

|Mailbox type|Supported|Not supported|
|:---------|:---------:|:---------:|
|User mailboxes    |![Check mark](media/f3b4c351-17d9-42d9-8540-e48e01779b31.png)       |         |
|Shared mailboxes    |![Check mark](media/f3b4c351-17d9-42d9-8540-e48e01779b31.png)        |       |
|Office 365 Group mailboxes    |![Check mark](media/f3b4c351-17d9-42d9-8540-e48e01779b31.png)         |         |
|Resource mailboxes    |      |![Check mark](media/f3b4c351-17d9-42d9-8540-e48e01779b31.png)        |
|Public folder mailboxes    |       |![Check mark](media/f3b4c351-17d9-42d9-8540-e48e01779b31.png)  |
||||

## Mailbox actions logged by default

A set of mailbox actions are logged by default for each of the following logon types:  

   - **Owner** - The mailbox owner. 
   
   - **Delegate** - Another user who's been assigned the SendAs, SendOnBehalf, or FullAccess permission to a person's mailbox. Note that an administrator who's been assigned the FullAccess permission to a user's mailbox is also considered a delegate user.
   
    - **Admin** - Mailboxes are considered to be accessed by an admin logon type only in the following scenarios:
    
       - When a mailbox is searched with one of the following Microsoft eDiscovery tools: 

         - Content Search in the Compliance center.
       
         -  eDiscovery or Advanced eDiscovery in the Compliance center.
       
         - In-Place eDiscovery in Exchange Online.
       - When [Microsoft Exchange Server MAPI Editor](https://go.microsoft.com/fwlink/p/?linkId=204086) is used to access the mailbox.     

The following table lists the mailbox actions that are currently logged by default for each logon type.

|Admin actions|Delegate actions|Owner actions|
|:---------|:---------|:---------|
|Create    |Create       | HardDelete        |
|HardDelete    |HardDelete        |MoveToDeletedItems       |
|MoveToDeletedItems    |MoveToDeletedItems         |SoftDelete         |
|SendAs    |SendAs      |    Update     |
|SendOnBehalf    |SendOnBehalf       |UpdateCalendarDelegation        |
|SoftDelete     |SoftDelete      | UpdateFolderPermissions        |
|Update    |Update       |UpdateInboxRules         |
|UpdateCalendarDelegation    | UpdateFolderPermissions        |         |
|UpdateFolderPermissions     | UpdateInboxRules        |         |
|UpdateInboxRules     |         |         |
||||

Here are descriptions for these mailbox actions. 

|Mailbox action|Description|
|:---------|:---------|
|**Create** <br/> |An item was created in the Calendar, Contacts, Notes, or Tasks folder in the mailbox; for example, a new meeting request is created. Note that creating, sending, or receiving a message isn't audited. Also, creating a mailbox folder is not audited.  <br/> |
|**HardDelete** <br/> |A message was purged from the Recoverable Items folder.  <br/> |
|**MoveToDeletedItems** <br/> |A message was deleted and moved to the Deleted Items folder.  <br/> |
|**SendAs** <br/> |A message was sent using the SendAs permission. This means another user sent the message as though it came from the mailbox owner.  <br/> |
|**SendOnBehalf** <br/> |A message was sent using the SendOnBehalf permission. This means another user sent the message on behalf of the mailbox owner. The message indicates to the recipient who the message was sent on behalf of and who actually sent the message.  <br/> |
|**SoftDelete** <br/> |A message was permanently deleted or deleted from the Deleted Items folder. Soft-deleted items are moved to the Recoverable Items folder.  <br/> |
|**Update** <br/> |A message or its properties was changed.  <br/> |
|**UpdateCalendarDelegation** <br/> |A calendar delegation was assigned to a mailbox. Calendar delegation gives someone else in the same organization permissions to manage the mailbox owner's calendar.  <br/> |
|**UpdateFolderPermissions** <br/> |A folder permission was changed. Folder permissions control which users in your organization can access folders in a mailbox and the messages located in those folders.  <br/> |
|**UpdateInboxRules** <br/> |An inbox rule was added, removed, or changed. Inbox rules are used to process messages in the user's Inbox based on the specified conditions and take actions when the conditions of a rule are met, such as moving a message to a specified folder or deleting a message.  <br/> |
|||

For a complete list of mailbox actions, including actions that are available but aren't included in the set of default actions, see the [Mailbox auditing actions](#mailbox-auditing-actions) section in this article.

> [!IMPORTANT]
> If you have explicitly configured the mailbox actions to audit for any logon type prior to mailbox auditing on by default being turned on for organization, the existing configuration for the mailbox will take precedence and won't be overwritten by the default mailbox actions described in this section. If at any time you want to revert to the default mailbox actions, you can do that by running the **Set-Mailbox -DefaultAuditSet** command. For more information about doing this, see the [Restore the default mailbox actions](#restore-the-default-mailbox-actions) section in this article.

### Verify that default mailbox actions are being logged for each logon type

With the release of mailbox auditing on by default, a new mailbox property named *DefaultAuditSet* has been added. This property indicates whether or not the default mailbox actions (managed by Microsoft) are being audited for each logon type for a specified mailbox. You can run the following command to display the values of this property:

```
Get-Mailbox <username> | FL DefaultAuditSet
```

A value of `Admin, Delegate, Owner` indicates that the default mailbox actions for all three logon types are being audited and that an administrator in your organization *has not* changed the actions for any logon type. Note this is the default state after mailbox auditing on by default is initially turned on in your organization. 

If an administrator in your organization has changed the mailbox actions that are audited for a logon type (by using the **Set-Mailbox** cmdlet with the *AuditAdmin*, *AuditDelegate*, or *AuditOwner* parameters), then the value for the *DefaultAuditSet* property will be different that the default value. For example, a value of `Owner` indicates that the only the default mailbox actions for the mailbox owner are being audited, and that the actions for `Delegate` and  `Admin` have been changed. If there are no values displayed for the *DefaultAuditSet* property (also called a *null* value) then the mailbox actions for all three logon types have been changed.

See the [Change or restore mailbox actions logged by default](#change-or-restore-mailbox-actions-logged-by-default) section in this article for more information about changing the mailbox actions that are audited.

### Display a list of mailbox actions logged by default

You can run the following commands in Exchange Online PowerShell to display the list of mailbox actions that are currently being for a mailbox for each logon type:

**Owner actions**

```
Get-Mailbox <username> | Select-Object -ExpandProperty AuditOwner
```

**Delegate actions**

```
Get-Mailbox <username> | Select-Object -ExpandProperty AuditDelegate
```

**Admin actions**

```
Get-Mailbox <username> | Select-Object -ExpandProperty AuditAdmin
```

## Change or restore mailbox actions logged by default

As previously explained, one of the key benefits of mailbox auditing on by default is that you don't have to manage the mailboxes actions that are audited. Microsoft does this for you and will automatically add new mailbox actions to be audited by default when they are released. However, your organization may have reasons to audit a set of mailbox actions that are different than the default ones. This section shows you how to change the mailbox actions that are audited for each of the logon type, and how to revert back to the Microsoft-managed default actions.

> [!IMPORTANT]
> If you make any change to the mailbox actions for a user that are logged by default (as described in the next section), then any new mailbox actions released by Microsoft will not be audited for those mailboxes. You'll have to explicitly add a new mailbox action to the list of actions that are audited for a logon type.

### Change the mailbox actions to audit

You can use the **Set-Mailbox** cmdlet with the *AuditAdmin*, *AuditDelegate*, or *AuditOwner* parameters to change the mailbox actions that are audited, depending on the logon type. Because these auditing-related parameters are multi-value parameters (meaning they can have more than one value), there are two different ways to change them.

- You can specify multiple mailbox actions that overwrite the existing actions by using the following syntax: `action1,action2,...actionN`.

- You can add or remove one or more mailbox action without affecting any existing records by using the following syntax: `@{Add="action1","value2"}` or `@{Remove="action1","action2"}`.

Regardless of which method you use to change the mailbox actions that are audited, the mailbox actions audited by default (for the logon type that you changed) will no longer be managed by Microsoft. Additionally, the value of the logon type that you changed won't be displayed in the *DefaultAuditSet* mailbox parameter that was [previously described](#verify-that-default-mailbox-actions-are-being-logged-for-each-logon-type).

Here are some examples of using one of these methods to change the mailbox actions to audit for each of the different logon types. 

This example changes the admin mailbox actions by overwriting the default actions with SoftDelete and HardDelete. 

```
Set-Mailbox <username> -AuditAdmin HardDelete,SoftDelete
```

This example adds the MailboxLogin owner action. 

```
Set-Mailbox <username> -AuditOwner @{Add="MailboxLogin"}
```

This example removes the MoveToDeletedItems delegate action.

```
Set-Mailbox <username> -AuditDelegate @{Remove="MoveToDeletedItems"}
```

#### Checking the DefaultAuditSet property

After you change the default mailbox actions for a logon type, the *DefaultAuditSet* property on the mailbox will be automatically updated to reflect this change. For example, if you run `Get-Mailbox <username> | FL DefaultAuditSet` after the first time you add or remove a mailbox owner action, the command will only return a value of `Admin, Delegate`. This indicates that the default mailbox actions for the owner have been changed This also means that any new mailbox owner actions released by Microsoft will not be automatically added to this mailbox. The same is true for changing the mailbox actions for the admin or delegate logon type.

### Restore the default mailbox actions

If you made changes to the mailbox actions that are audited for a logon type, you can restore the default mailbox actions that are audited by running the `Set-Mailbox -DefaultAuditSet` command. When you do this, the following things will happen:

- The current list of mailbox actions will be replaced with the default mailbox actions for the appropriate logon type.
 
- Any new mailbox actions released by Microsoft will be automatically added to the list for the appropriate logon type.

- The [DefaultAuditSet mailbox property](#checking-the-defaultauditset-property) will be updated to include the appropriate logon type.

To restore the default mailbox actions for all logon types, run the following command:

```
Set-Mailbox <username> -DefaultAuditSet Admin,Delegate,Owner
```

You can use this command to restore the default mailbox actions for any of the logon types (by using the **Admin**, **Delegate**, or **Owner** values for the *DefaultAuditSet* parameter.)

## Turn off mailbox auditing on by default for your organization

If for some reason your organization decides that it doesn't want to audit mailbox actions, you can turn off mailbox auditing on by default for your entire organization by running the following command in Exchange Online PowerShell:

```
Set-OrganizationConfig -AuditDisabled $true
```

When mailbox auditing on by default is turned off (the *AuditDisabled* property is set to **True**) for the organization, the following things will happen:

- Mailbox auditing is disabled for your organization.

- No mailbox actions will be audited (starting from the time when auditing is disabled for the organization), even if the *AuditEnabled* property on a mailbox is set to **True**.

- Mailbox auditing won't be enabled for new mailboxes and setting the *AuditEnabled* property on a new (or existing) mailbox to **True** will be ignored.

- Any mailbox audit bypass association settings (configured by using the **Set-MailboxAuditBypassAssociation** cmdlet) will be ignored.

- Existing mailbox audit records be retained until the audit log age limit for the the record expires.

### Turn on mailbox auditing on by default

To turn mailbox auditing back on for your organization, simply run the following command in Exchange Online PowerShell:

```
Set-OrganizationConfig -AuditDisabled $false
```

## Bypass mailbox audit logging

Currently, you can't disable mailbox auditing for specific mailboxes when mailbox auditing on by default is turned on in your organization. For example, setting the *AuditEnabled* mailbox property to **False** is ignored.  However, you can still use the **Set-MailboxAuditBypassAssociation** cmdlet in Exchange Online PowerShell to prevent mailbox actions performed by specific users from being logged. When you bypass mailbox auditing, the mailbox actions performed by a specific user aren't audited, regardless of which mailbox those actions are being performed on. If you bypass mailbox auditing for a specific user, then the mailbox owner actions performed by that user won't be logged. And if that same user is assigned permissions to another user's mailbox (or a shared mailbox), then the delegate actions performed by the first user also won't be logged.

To bypass mailbox audit logging for a specific user, run the following command:

```
Set-MailboxAuditBypassAssociation -Identity <username> -AuditByPassEnabled $true
```

To verify that auditing is bypassed for the specified user, run the following command:

```
Get-MailboxAuditBypassAssociation -Identity <username> | FL AuditByPassEnabled
```

A value of **True** indicates that mailbox audit logging is bypassed for that user.

## Mailbox auditing actions
  
The following table summarizes the actions that are audited for each user logon type. In the table, an asterisk ( **\*** ) indicates that the action is logged by default. A **No** indicates that an action can't be logged for that logon type. Note that an administrator who has been assigned the Full Access permission to a user's mailbox is considered a delegate user. 
  
|**Action**|**Description**|**Admin**|**Delegate**|**Owner**|
|:-----|:-----|:-----|:-----|:-----|
|**Copy** <br/> |A message was copied to another folder.  <br/> |Yes  <br/> |No  <br/> |No  <br/> |
|**Create** <br/> |An item is created in the Calendar, Contacts, Notes, or Tasks folder in the mailbox; for example, a new meeting request is created. Note that creating, sending, or receiving a message isn't audited. Also, creating a mailbox folder is not audited.  <br/> |Yes\*  <br/> |Yes\*  <br/> |Yes  <br/> |
|**FolderBind**\** <br/> |A mailbox folder was accessed. This action is also logged when the admin or delegate opens the mailbox.  <br/> |Yes  <br/> |Yes  <br/> |No  <br/> |
|**HardDelete** <br/> |A message was purged from the Recoverable Items folder.  <br/> |Yes\*  <br/> |Yes\*  <br/> |Yes\*  <br/> |
|**MailboxLogin** <br/> |The user signed into their mailbox.  <br/> |No  <br/> |No  <br/> |Yes  <br/> |
|**MessageBind**\*** <br/> |A message was viewed in the preview pane or opened.  <br/> |Yes  <br/> |No  <br/> |No  <br/> |
|**Move** <br/> |A message was moved to another folder.  <br/> |Yes  <br/> |Yes  <br/> |Yes  <br/> |
|**MoveToDeletedItems** <br/> |A message was deleted and moved to the Deleted Items folder.  <br/> |Yes\*  <br/> |Yes\*  <br/> |Yes\*  <br/> |
|**SendAs** <br/> |A message was sent using the SendAs permission. This means another user sent the message as though it came from the mailbox owner.  <br/> |Yes\*  <br/> |Yes\*  <br/> |No  <br/> |
|**SendOnBehalf** <br/> |A message was sent using the SendOnBehalf permission. This means another user sent the message on behalf of the mailbox owner. The message indicates to the recipient who the message was sent on behalf of and who actually sent the message.  <br/> |Yes\*  <br/> |Yes\*  <br/> |No  <br/> |
|**SoftDelete** <br/> |A message was permanently deleted or deleted from the Deleted Items folder. Soft-deleted items are moved to the Recoverable Items folder.  <br/> |Yes\*  <br/> |Yes\*  <br/> |Yes\*  <br/> |
|**Update** <br/> |A message or its properties was changed.  <br/> |Yes\*  <br/> |Yes\*  <br/> |Yes\*  <br/> |
|**UpdateCalendarDelegation** <br/> |A calendar delegation was assigned to a mailbox. Calendar delegation gives someone else in the organization permissions to manage the mailbox owner's calendar.  <br/> |Yes\*  <br/> |No  <br/> |Yes\*  <br/> |
|**UpdateFolderPermissions** <br/> |A folder permission was changed. Folder permissions control which users in your organization can access folders in a mailbox and the messages located in those folders.  <br/> |Yes\*  <br/> |Yes\*  <br/> |Yes\*  <br/> |
|**UpdateInboxRules** <br/> |An inbox rule has been added, removed, or changed. Inbox rules are used to process messages in the user's Inbox based on the specified conditions and take actions when the conditions of a rule are met, such as moving a message to a specified folder or deleting a message.  <br/> |Yes\*  <br/> |Yes\*  <br/> |Yes\*  <br/> |
   
> [!NOTE]
> <sup>\*</sup> Audited by default when default mailbox auditing is enabled for the logon type. <br/><br/>  <sup>\*\*</sup> Audit records for folder bind actions performed by delegates are consolidated. One audit record is generated for individual folder access within a time span of 24 hours. <br/><br/> <sup>\*\*\* </sup> The MessageBind action has been deprecated in Exchange Online, and is no longer available to add to the list of mailbox actions for the admin logon type. 

## More information

- By default, mailbox audit log records are retained for 90 days and then deleted. You can change the age limit for audit log records by using the **Set-Mailbox -AuditLogAgeLimit** command in Exchange Online PowerShell. Note that increasing the default age limit for mailbox auditing records doesn't affect the 90-day age limit for mailbox audit log records in the Microsoft 365 audit log. For example, if you increase the age limit for mailbox audit log records to 365 days, a mailbox audit record will be searchable in the Microsoft 365 audit log for only 90 days after the corresponding event occurred. In this case, you would have to search the user's mailbox audit log for records older than 90 days. For more information about searching mailbox audit logs, see [Search-MailboxAuditLog](https://docs.microsoft.com/powershell/module/exchange/policy-and-compliance-audit/search-mailboxauditlog).

- If you've changed the *AuditLogAgeLimit* property for a mailbox prior to mailbox auditing on by default being turned on for organization, the existing audit log age limit for that mailbox will not be changed; in other words, mailbox auditing on by default doesn't effect the current age limit for mailbox audit records.

- Mailbox audit log records are stored in a subfolder (named *Audits*) in the Recoverable Items folder in each user's mailbox. Keep the following things in mind about mailbox audit records and the Recoverable Items folder.
   
    - Mailbox audit records count against the storage quota of the Recoverable Items folder, which is 30GB by default (the Warning quota is 20 GB). Note that the storage quota for the Recoverable Items folder is automatically increased from to 100 GB (90 MB Warning quota) when a hold is placed on a mailbox or the mailbox is assigned to a retention policy in the Compliance Center.

    - Mailbox audit records also counts against the [folder limit for the Recoverable Items folder](https://docs.microsoft.com/office365/servicedescriptions/exchange-online-service-description/exchange-online-limits#mailbox-folder-limits). The maximum number of items (which are audit records in this case) that can be stored in the Audits subfolder is 3 million items. 

      > [!NOTE]
      > It's unlikely that mailbox auditing on by default will impact the storage quota or the folder limit for the Recoverable Items folder. 

    - You can run the following command in Exchange Online PowerShell to display the size and number of items in the Audits subfolder in the Recoverable Items folder: 
       ```
       Get-MailboxFolderStatistics <username> -FolderScope RecoverableItems | Where-Object {$_.Name -eq 'Audits'} | FL FolderPath,FolderSize,ItemsInFolder
       ```

     - You can't directly access an audit log record in the Recoverable Items folder; instead, you use the **Search-MailboxAuditLog** cmdlet or search the Microsoft 365 audit log to find and view mailbox audit records.

- If a mailbox is placed on hold or assigned to a retention policy in the Compliance Center, audit log records are still retained for the duration defined by the *AuditLogAgeLimit* property for the mailbox (which is set to 90 days by default). To retain audit log records longer for mailboxes on hold, you have to increase the retention period by increasing the value for the *AuditLogAgeLimit* property.
