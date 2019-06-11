---
title: "Load non-Office 365 data into a review set"
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

# Load non-Office 365 data into a review set

Not all documents that you may need to analyze with Office 365 Advanced eDiscovery will live in Office 365. With the Non-Office 365 content import feature in Advanced eDiscovery you can upload documents that don't live in Office 365 into a review set so it is analyzed with Advanced eDiscovery. This procedure shows you how to bring your non-Office 365 documents into Advanced eDiscovery for analysis.

>[!Note]
>Advanced eDiscovery requires an Office 365 E3 with the Advanced Compliance add-on or an E5 subscription for your organization. If you don't have that plan and want to try Advanced eDiscovery, you can sign up for a trial of Office 365 Enterprise E5.

## Before you begin

Using the upload Non-Office 365 feature as described in this article requires that you have the following:

- An Office 365 or Microsoft 365 E5 subscription or an E3 subscription with the Advanced Compliance add-on subscription.

- All custodians whose non-Office 365 content will be uploaded must have E3 license with an Advanced Compliance add-on license or have an E5 license.

- An existing Advanced eDiscovery case.

- Custodians must be added to the case before you upload the non-Office 365 data that's associated to them.

- All files that will be uploaded must be located in folders, where each folder is associated with a specific custodian. The names for these folders must use the following naming format: *alias@domainname*. The *alias@domainname* must be the user's Office 365 alias and domain. You can collect all the *alias@domainname* folders into a root folder. The root folder can only contain the *alias@domainname* folders; loose files aren't allowed in the root folder.

   For example, the folder structure for the non-Office 365 data that you want to upload would be similar to the following:

   - c:\nonO365\abraham.mcmahon@contoso.com
   - c:\nonO365\jewell.gordon@contoso.com
   - c:\nonO365\staci.gonzalez@contoso.com

   Where abraham.mcmahon@contoso.com, jewell.gordon@contoso.com, and staci.gonzalez@contoso.com are the SMTP addresses of custodians in the case.

   ![Non-Office 365 data upload folder structure](../media/3f2dde84-294e-48ea-b44b-7437bd25284c.png)

- An account that is either an eDiscovery Manager or eDiscovery Administrator

- Microsoft Azure Storage Tools installed on a computer that has access to the non-Office 365 content folder structure.

- Install AzCopy, which you can do from here: https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy

## Upload non-Office 365 content into Advanced eDiscovery

1. As an eDiscovery Manager or eDiscovery Administrator, open Advanced eDiscovery, then the case that the non-Office 365 data will be uploaded to.  Click the **review sets** tab, then select the review set you wish to load the Non-Office 365 data to.  If you have not already created a review set, you can do so now.  Finally, click **Manage review set** and then click **View uploads** in the **Non-Office 365 data tile.

2. Click the **Upload files** button to start the Non-Office 365 data import wizard.

   ![Upload files](../media/574f4059-4146-4058-9df3-ec97cf28d7c7.png)

3. The first step in the wizard simply prepares a secure Azure blob for the files to be uploaded.  Once preparation is completed, click the **Next: Upload files** button.

   ![Non-Office 365 Import - Prepare](../media/0670a347-a578-454a-9b3d-e70ef47aec57.png)
 
4. In the **Upload files** step, specify the **Path to location of files**, this is where the Non-Office 365 data you plan on importing is located.  Setting the correct location ensures the AzCopy command is properly updated.

   > [!NOTE]
   > If you have not already installed AzCopy, you can do this from here: https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy

5. Copy the predefined command by clicking the **Copy to clipboard** link. Start a windows command prompt, paste the command and press enter.  The files will be uploaded to the secure Azure blob storage for the next step.

   ![Non-Office 365 Import - Upload files](../media/3ea53b5d-7f9b-4dfc-ba63-90a38c14d41a.png)

   ![Non-Office 365 Import - AzCopy](../media/504e2dbe-f36f-4f36-9b08-04aea85d8250.png)

   > [!NOTE]
   > If the supplied AzCopy command fails, refer to [Troubleshoot AzCopy in Advanced eDiscovery](troubleshooting-azcopy.md)

6. Finally, return back to the Security & Compliance and click the **Next: Process files** button.  This will initiate processing, text extraction and indexing of the uploaded files.  You can track the progress of processing here or in the **Jobs** tab.  Once completed, the new files will be available in the review set.  Once processing is complete, you can dismiss the wizard.

   ![Non-Office 365 Import - Process files](../media/218b1545-416a-4a9f-9b25-3b70e8508f67.png)

