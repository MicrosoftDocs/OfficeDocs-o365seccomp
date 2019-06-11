---
title: "Manage mail users in EOP"
ms.reviewer: 
ms.author: krowley
author: kccross
manager: laurawi
ms.date: 12/9/2016
audience: ITPro
ms.topic: article
ms.service: O365-seccomp
localization_priority: Normal
ms.assetid: 4bfaf2ab-e633-4227-8bde-effefb41a3db
description: "Defining mail users is an important part of managing the Exchange Online Protection (EOP) service."
---

# Manage mail users in EOP

Defining mail users is an important part of managing the Exchange Online Protection (EOP) service. There are several ways that you can manage users in EOP:
  
- Use directory synchronization to manage mail users: If your company has existing user accounts in an on-premises Active Directory environment, you can synchronize those accounts to Azure Active Directory (AD), where a copy of the accounts is stored in the cloud. When you synchronize your existing user accounts to Azure Active Directory, you can view those users in the **Recipients** pane of the Exchange admin center (EAC). Using directory synchronization is recommended. 
    
- Use the EAC to manage mail users: Add and manage mail users directly in the EAC. This is the easiest way to add mail users and is useful for adding one user at a time.
    
- Use remote Windows PowerShell to manage mail users: Add and manage mail users by running remote Windows PowerShell. This method is useful for adding multiple records and creating scripts.
    
> [!NOTE]
> You can add users in the Microsoft 365 admin center, however these users can't be used as mail recipients. 
  
## Before you begin

- Procedures in this topic require specific permissions. See each procedure for its permissions information.
    
- For information about keyboard shortcuts that may apply to the procedures in this topic, see **Keyboard shortcuts in the Exchange admin center**.
    
> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at [Exchange Server](https://go.microsoft.com/fwlink/p/?linkId=60612),[Exchange Online](https://go.microsoft.com/fwlink/p/?linkId=267542), or [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkId=285351). 
  
## Use directory synchronization to manage mail users

This section provides information about managing email users by using directory synchronization.
  
> [!IMPORTANT]
> If you use directory synchronization to manage your recipients, you can still add and manage users in the Microsoft 365 admin center, but they will not be synchronized with your on-premises Active Directory. This is because directory synchronization only syncs recipients from your on-premises Active Directory to the cloud. 
  
> [!TIP]
>  Using directory synchronization is recommended for use with the following features: > **Outlook safe sender and blocked sender lists** - When synchronized to the service, these lists will take precedence over spam filtering in the service. This lets users manage their own safe sender and blocked sender lists on a per-user or per-domain basis. > **Directory Based Edge Blocking (DBEB)** - For more information about DBEB, see [Use Directory Based Edge Blocking to Reject Messages Sent to Invalid Recipients](http://technet.microsoft.com/library/ca7b7416-92ed-40ad-abdb-695be46ea2e4.aspx). > **End user spam quarantine** - In order to access the end user spam quarantine, end users must have a valid Office 365 user ID and password. EOP customers protecting on-premises mailboxes must be valid email users. > **Mail flow rules** - When you use directory synchronization, your existing Active Directory users and groups are automatically uploaded to the cloud, and you can then create mail flow rules (also known as transport rules) that target specific users and/or groups without having to manually add them via the the EAC or Exchange Online Protection PowerShell. Note that [dynamic distribution groups](https://go.microsoft.com/fwlink/?LinkId=507569) can't be synchronized via directory synchronization. 
  
 **Before you begin**
  
Get the necessary permissions and prepare for directory synchronization, as described in [Prepare for directory synchronization](https://go.microsoft.com/fwlink/p/?LinkId=308908).
  
### To synchronize user directories

1. Activate directory synchronization, as described in [Activate directory synchronization](https://go.microsoft.com/fwlink/p/?LinkId=308909).
    
2. Set up your directory synchronization computer, as described in [Set up your directory sync computer](http://go.microsoft.com/fwlink/p/?LinkId=308911).
    
3. Synchronize your directories, as described in [Use the Configuration Wizard to sync your directories](http://go.microsoft.com/fwlink/?LinkId=308912).
    
    > [!IMPORTANT]
    > When you finish the Azure Active Directory Sync Tool Configuration Wizard, the **MSOL_AD_SYNC** account is created in your Active Directory forest. This account is used to read and synchronize your on-premises Active Directory information. In order for directory synchronization to work correctly, make sure that TCP 443 on your local directory synchronization server is open. 
  
4. Activate synced users, as described in [Activate synced users](http://go.microsoft.com/fwlink/p/?LinkId=308913).
    
5. Manage directory synchronization, as described in [Manage directory synchronization](http://go.microsoft.com/fwlink/p/?LinkId=308915).
    
6. Verify that EOP is synchronizing correctly. In the EAC, go to **Recipients** \> **Contacts** and view that the list of users was correctly synchronized from your on-premises environment. 
    
## Use the EAC to manage mail users

This section provides information about adding and managing email users directly in the EAC.
  
 **Before you begin**
  
You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Users, Contacts, and Role Groups" entry in [Feature permissions in EOP](feature-permissions-in-eop.md).
  
### To add a mail user in the EAC

1. Create an email user by going to go to **Recipients** \> **Contacts** in the EAC, and then clicking **New +**.
    
2. On the **New mail user** page, enter the user's information, including the following: 
    
   ****

|**Mail user property**|**Description**|
|:-----|:-----|
|**First name**, **Initials**, and **Last name** <br/> |Type the user's full name in the appropriate boxes.  <br/> |
|**Display name** <br/> |Type a name, using up to 64 characters. By default, this box shows the names in the **First name**, **Initials**, and **Last name** boxes if any. The display name is required.  <br/> |
|**Alias** <br/> |Type a unique alias, using up to 64 characters, for the user. The alias is required.  <br/> |
|**External email address** <br/> |Type the external email address of the user.  <br/> |
|**User id** <br/> |Type the name that the mail user will use to sign in to the service. The user sign-in name consists of a user name on the left side of the at (@) symbol and a suffix on the right side. Typically, the suffix is the domain name in which the user account resides.  <br/> |
|**New password** <br/> |Type the password that the mail user will use to sign in to the service. Make sure that the password you supply complies with the password length, complexity, and history requirements of the domain in which you're creating the user account.  <br/> |
|**Confirm password** <br/> |Retype the password to confirm it.  <br/> |
   
3. Click **Save** to create the new email user. The new user should appear in the list of users. 
    
### To edit or remove a mail user in the EAC

- In the EAC, go to **Recipients** \> **Contacts**. In the list of users, click the user that you want to view or change, and then select **Edit** ![Edit icon](../media/ITPro-EAC-EditIcon.gif) to update the user settings as needed. You can change the user's name, alias, or contact information, and you can record detailed information about the user's role in the organization. You can also select a user and then choose **Remove**![Remove icon](../media/ITPro-EAC-RemoveIcon.gif) to delete it. 
    
## Use remote Windows PowerShell to manage mail users

This section provides information about adding and managing mail users by using remote Windows PowerShell.
  
 **Before you begin**
  
- You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Users, Contacts, and Role Groups" entry in [Feature permissions in EOP](feature-permissions-in-eop.md).
    
- Be aware that when creating mail users by using remote PowerShell cmdlets, you may encounter throttling.
    
- This cmdlet uses a batch processing method that results in a propagation delay of a few minutes before the results of the cmdlet are visible.
    
- To learn how to use Windows PowerShell to connect to Exchange Online Protection, see [Connect to Exchange Online Protection Using Remote PowerShell](http://technet.microsoft.com/library/054e0fd7-d465-4572-93f8-a00a9136e4d1.aspx).
    
 **To add a mail user using remote PowerShell**
  
This example uses the [New-EOPMailUser](http://technet.microsoft.com/library/0520cf33-4ad0-44e4-99a3-1b485739fc05.aspx) cmdlet to create a mail-enabled user account for Jeffrey Zeng in EOP with the following details: 
  
- The first name is Jeffrey and the last name is Zeng.
    
- The name is Jeffrey and the display name is Jeffrey Zeng.
    
- The alias is jeffreyz.
    
- The external email address is jzeng@tailspintoys.com.
    
- The Office 365 sign in name is jeffreyz@contoso.onmicrosoft.com.
    
- The password is Pa$$word1.
    
```Powershell
New-EOPMailUser -LastName Zeng -FirstName Jeffrey -DisplayName "Jeffrey Zeng" -Name Jeffrey -Alias jeffreyz -MicrosoftOnlineServicesID jeffreyz@contoso.onmicrosoft.com -ExternalEmailAddress jeffreyz@tailspintoys.com -Password (ConvertTo-SecureString -String 'Pa$$word1' -AsPlainText -Force)
```

 **To verify that this worked**
  
Run the [Get-User](http://technet.microsoft.com/library/2a33c9e6-33da-438c-912d-28ce3f4c9afb.aspx) cmdlet as follows to display information about new mail user Jeffrey Zeng: 
  
```Powershell
Get-User "Jeffrey Zeng"

```

 **To edit the properties of a mail user using remote PowerShell**
  
Use the [Get-Recipient](http://technet.microsoft.com/library/2ce6250f-0ad3-4b29-870c-e1d6e1e154bc.aspx) and [Set-EOPMailUser](http://technet.microsoft.com/library/834c3de6-1485-4d50-bb96-262a2c0c8619.aspx) cmdlets to view or change properties for mail users. 
  
This example sets the external email address for Pilar Pinilla.
  
```Powershell
Set-EOPMailUser -Identity "Pilar Pinilla" -EmailAddresses pilarp@tailspintoys.com
```

This example sets the Company property for all mail users to Contoso.
  
```Powershell
$Recip = Get-Recipient -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'mailuser')}
$Recip | foreach {Set-EOPUser -Identity $_.Alias -Company Contoso}

```

 **To verify that this worked**
  
In the previous example where we changed the properties for mail user Pilar Pinella, use the [Get-Recipient](http://technet.microsoft.com/library/2ce6250f-0ad3-4b29-870c-e1d6e1e154bc.aspx) cmdlet to verify the changes. (Note that you can view multiple properties for multiple mail contacts.) 
  
```Powershell
Get-Recipient -Identity "Pilar Pinilla" | Format-List 

```

In the previous example where the Company property was set to Contoso for all mail users, run the following command to verify the changes:
  
```Powershell
Get-Recipient -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'mailuser')} | Format-List Name,Company
```

> [!IMPORTANT]
> This cmdlet uses a batch processing method that results in a propagation delay of a few minutes before the results of the cmdlet are visible. 
  
 **To remove a mail user using remote PowerShell**
  
This example uses the [Remove-EOPMailUser](http://technet.microsoft.com/library/cb91dc26-ed22-4d3c-9f64-df9df1754edb.aspx) cmdlet to delete user Jeffrey Zeng: 
  
```Powershell
Remove-EOPMailUser -Identity Jeffrey
```

 **To verify that this worked**
  
Run the [Get-Recipient](http://technet.microsoft.com/library/2ce6250f-0ad3-4b29-870c-e1d6e1e154bc.aspx) cmdlet as follows. You should get an error message since the user no longer exists. 
  
```Powershell
Get-Recipient Jeffrey | fl
```


