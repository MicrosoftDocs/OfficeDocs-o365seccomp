---
title: "Manage a data spillage incident in Microsoft 365"
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

description: "This article describes using the new Data Investigations (Preview) tool in the Security & Compliance Center to manage a data spillage incident."
---

# Manage a data spillage incident in Microsoft 365

Data spillage is when a document containing confidential, sensitive or malicious information is released into an untrusted environment. When a data spillage incident is detected, it's important to quickly contain the environment, assess the size and locations of the spillage, examine user activities around it, and then delete the spilled data from the service. Using the Data Investigations (Preview) tool, you can search for sensitive, malicious or misplaced data across Office 365, investigate to find out what happened, and then take appropriate actions.  

## Scope of this article

This article provides a list of instructions on how to permanently delete items from Office 365 mailboxes so they are no longer accessible or recoverable by users or admins. 

> [!NOTE]
> When you delete items located in a SharePoint or OneDrive for Business site, they are retained for 93 days from the time you delete them from their original location.

## Scenario

You're informed of a data spillage incident where an employee unknowingly shared a highly-confidential document with multiple people through email. You want to quickly assess who received this document, both inside and outside of your organization. After you've investigate the incident, you plan to share your findings with other investigators to review, and then permanently remove the spilled data from your Office 365 organization. After the investigation is complete, you want to remove all evidence. 

> [!IMPORTANT]
> While you'll be able to permanently remove the spilled data within your own organization, any data spilled outside your organization can't be removed with these capabilities.

## Workflow

Here's the workflow for using Data Investigations (Preview) to manage a data spillage incident:

1.	Create a data investigation.

2.	Search for sensitive, malicious, or misplaced data and collect them as evidence.

3.	Review and investigate the evidence.

4.	Permanently delete the spilled data.

5.	Close or delete the investigation.


## Before you begin

- You'll use the Data Investigations (Preview) tool in the Security & Compliance Center to create an investigation, search for the spilled data, and review and analyze it. Then you'll use Security & Compliance Center PowerShell to permanently delete the spilled data from Office 365. 

- To create an investigation, you have to be a member of the Compliance Administrator role group in the Security & Compliance Center.

- To delete messages, you have to be a member of a role group in the Security & Compliance Center that's assigned the Search and Purge role. By default, this role is assigned to the Organization Management role group. For information about adding users to a role group, see [Permissions in the Security & Compliance Center](../permissions-in-the-security-and-compliance-center.md). 

- To control which user mailboxes and OneDrive accounts an investigator can search, your organization can set up compliance boundaries. For more information, [Set up compliance boundaries for eDiscovery investigations](../set-up-compliance-boundaries.md). 

## Step 1: Create a data investigation

To create an investigation in the Data Investigations (Preview) tool:

1. Go to [https://compliance.microsoft.com](https://compliance.microsoft.com).
    
2. Sign in to Office 365 using your work or school account.
    
3. In the compliance center, click **Data Investigations**.
 
4. On the **Data Investigations (Preview)** page, click **Create new investigation**.
    
5. On the **New data investigation** flyout page, give the investigation a name (required), and then type an optional investigation number and description. Note that the name must be unique in your organization.

6. Under **Do you want to configure additional settings after creating this investigation?**, do one of the following:

    - Click **Yes** to create the investigation, and display the **Settings** page in the new case. This allows you to add members to the investigation.
    
    - Click **No** to just create the investigation and display it in the list of cases on the **Data Investigations (Preview)** page. If you choose this option, you will be added as the only member of the investigation and the default search and analytics settings will be used. You can add members or change settings any time after the investigation is created.

7. Click **Save** to create the investigation.

    The new investigation is displayed in the list on the **Data Investigations (Preview)** page. 

8. To open an investigation, click the name of the investigation. 

    The **Home** tab for the investigation is displayed. 

> [!TIP]
> Consider establishing a naming convention for investigations and provide as much information as you can in the name and description so you can locate and refer to in the future if necessary.
 
## Step 2: Search for the spilled data 
 
If you know which users you want to search for spilled data, you can add them as people of interest to map their data sources to the investigation and quickly search their mailbox and OneDrive account. To add people of interest to the investigation, click **People of interest**, and then click **Add people of interest**. For more information, see [Manage people of interest](manage-people-of-interest.md).

On the **Searches** tab, you can create searches to find the spilled data. You will use the same search query that you used to find the spilled data to delete those same messages in [Step 4](#step-4-delete-the-spilled-data). For more information about creating searches, see [Search for data in an investigation](search-for-data.md).

After you run the search, you can preview samples of search results and view search statistics to evaluate the effectiveness of your search query. Once you identify the items that you want to delete from Office 365, you can click the **Evidence** tab, and then create an evidence set and add search results that contain those items. 

To do this, click the search that you want to investigate. On the flyout page, click **Add results to evidence** and follow the instructions. Then in the evidence, you can review individual documents, investigate who had access to documents, and export the documents. To simply delete the documents instead of reviewing them, go to [Step 4](#step-4-delete-the-spilled-data). 

> [!IMPORTANT]
> The keywords that you use in the search query may contain the actual spilled data that you're searching for. For example, if you search for documents containing a social security number and you use it as a keyword in the search query, you must delete the query afterwards to avoid further spillage. You can delete the search or delete the entire investigation in [Step 5](#step-5-close-or-delete-the-investigation). 

## Step 3: Review and investigate 

In the investigation, go to **Evidence** tab and click on the evidence set that you created in the previous step. After the processing job is completed and the search results are added to the evidence, you can review individual documents in their native format, text format, or a near-native format. You can create additional queries to narrow the list of documents, and tag documents to indicate findings from your investigation. For more information, see [Review data in evidence](review-data-in-evidence.md)

To group documents and get more assistance for your review, click **Manage evidence**. In the **Analytics** tile, click **Analyze**. This will run advanced analytics such as duplicate detection, email threading, and theme analysis. For more information, see:

- [Run analytics to investigate faster](run-analytics-to-investigate-faster.md)
- [Near duplicate detection](near-duplicates.md)
- [Email threading](email-threading.md)
- [Themes](themes.md)

To determine which users are involved in the data spillage, you can create a new query in the evidence set and then use the Sender/Author and Recipients conditions. This will create a list of all senders, recipients, and authors found in collected data that was added to the evidence. Be sure to examine the list to determine if there are any external users. For more information about using conditions to narrow search results, see [Search conditions](../keyword-queries-and-search-conditions.md#search-conditions).

## Step 4: Delete the spilled data

### Deleting mailbox items

After you review and validate that the search results contain only the email messages that must be deleted, you can permanently delete them by running the **New-ComplianceSearchAction -Purge -PurgeType HardDelete** command in Security & Compliance Center PowerShell. For instructions, see [Search for and delete email messages](../search-for-and-delete-messages-in-your-organization.md). 

If single item recovery is enabled for mailboxes in your organization, permanently deleted items will be retained in the user's Recoverable items folder (and accessible by admins) until the deleted item retention period ends (the default is 14 days). Additionally, if any mailbox that contains spilled data is on a legal hold or assigned to a retention policy, purged messages will be retained in the Recoverable items folder until the hold duration for the item expires. To hard delete messages immediately, you need to perform addition tasks. For instructions, see [Delete items in the Recoverable Items folder of cloud-based mailboxes on hold](../delete-items-in-the-recoverable-items-folder-of-mailboxes-on-hold.md).  

> [!IMPORTANT]
> Check with your records management or legal departments before removing a hold or retention policy. Your organization may have a policy that defines whether a mailbox on hold or a data spillage incident takes priority. 

### Deleting site items

To permanently delete a document from a SharePoint site or OneDrive account, you have to delete the document and then you have to delete from the site Recycle Bin and then delete it from the site collection Recycle Bin. For more information, see [Delete documents in SharePoint and OneDrive](https://docs.microsoft.com/microsoft-365/compliance/gdpr-dsr-office365#deleting-documents-in-sharepoint-online-and-onedrive-for-business).

Alternatively, you can delete an entire site collection that might contained spilled data. For instructions, see [Delete a site collection](https://docs.microsoft.com/sharepoint/delete-site-collection).

## Step 5: Close or delete the investigation

After you delete documents in the source content locations (mailboxes or sites) in the live service, you will still have copies of these documents that you added to evidence as part of your investigation. To avoid further data spillage, you should consider deleting the investigation itself.

To delete an investigation:

1. On the **Settings** tab, click **Investigation information**.

2. Click  **Delete investigation**. 

If you don't need to delete the investigation or if you want to save the information that you collected during the investigation, you can click **Close case**. Then at a later date, you can re-open closed investigations.
