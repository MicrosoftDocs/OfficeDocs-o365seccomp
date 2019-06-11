---
title: "Download export jobs"
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

# Download export jobs

All exported data is added to a Microsoft Azure blob. This provides multiple options to handle the data downstream. There are several ways to access an Azure blob. One method is to use Azure Storage Explorer. This method supports simple connection, browsing and downloading. For more information, visit <https://docs.microsoft.com/en-us/azure/storage/blobs/storage-quickstart-blobs-storage-explorer>

1.  To download content after an export job is complete, go to the Exports tab and select an export job.

2.  Copy the text in the “Locations” section of the flyout.

![](../media/eDiscoExportJob.png)

3.  Open Azure Storage Explorer and click the “Connect” button

![](../media/AzureStorageConnect.png)

4.  Select “Use a shared access signature URI” and click next

![](../media/AzureStorageConnect2.png)

5.  Paste the Location text in the URI text box and click next

![](../media/AzureStorageConnect3.png)

6.  Click Connect

![](../media/AzureStorageConnect4.png)

This will add the export as an object in Storage Accounts/SAS-Attached Services/Blob Containers. You will be able to explore the export and download all or portions of the export.

![](../media/AzureStorageConnect5.png)
