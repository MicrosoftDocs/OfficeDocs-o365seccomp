---
title: "Manage jobs in Data Investigations"
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

# Manage jobs in Data Investigations (Preview)

Here's a list of the jobs (which are typically long-running processes) that are tracked on the **Jobs** tab of an investigation in Data Investigations (Preview). These jobs are triggered by user actions when using and managing investigations.

| Job type           | Description     |
| :----------------- | :----------     |
|Adding data to an evidence set | A user adds the results of a search to an evidence set.  For more information, see [Search for data in an investigation](search-for-data.md). |
|Adding data to another evidence set | A user adds documents from one evidence set to a different evidence set in the same case.|
|Adding non-Office 365 data to an evidence set | A user uploads non-Office 365 data to an evidence set. The data is also indexed during this process. For example, files from an on-premises file server or a client computer are uploaded to an evidence set. For more information, see [Load non-Office 365 data into evidence](load-non-office365-data.md).| 
|Adding remediated data to an evidence set | Data with processing errors is remediated and loaded back into an evidence set. For more information, see [Error remediation when processing data for an investigation](error-remediation.md). | 
|Comparing load sets | A user looks at the differences between different load sets in an evidence set. A load set is an instance of adding data to an evidence set. For example, if you add the results of two different searches to the same evidence set, each would represent a load set. For more information, see [Manage load sets](manage-load-sets.md). |
|Converting redacted documents to PDF|After a user annotates a document in an evidence set and redacts a portion of it, they can choose to convert the redacted document to a PDF file. This ensures that the redacted portion will not be visible when the document is exported for presentation. For more information, see [Review data in evidence](review-data-in-evidence.md). |
|Estimating search results | After a user creates and runs a new search (or re-runs an existing search), the search tool searches the index for items that match the search query and prepares a estimate that includes the number and total size of all items by the search, and the number of data sources searched.  For more information, see [Search for data in an investigation](search-for-data.md). | 
|Preparing data for export | A user exports documents from an evidence set. When the export process is complete, they can download the exported data to a local computer. For more information, see [Export data from an investigation](export-data.md). | 
|Preparing for error resolution |When a user selects a file and creates a new error remediation in the Error view on the **Processing** tab of an investigation, the first step in the process is to upload the file that has the processing error to an Azure storage location in the Microsoft cloud. This job tracks the progress of the upload process. For more information about the error remediation workflow, see [Error remediation when processing data for an investigation](error-remediation.md).| 
|Preparing search preview | After a  user creates and runs a new search (or re-runs an existing search), the search tool prepare a sample subset of items (that match the search query) that can be previewed. Previewing search results can help you determine the effectiveness of the search.  For more information, see [Search for data in an investigation](search-for-data.md). | 
|Re-indexing data of people of interest | When you add a person of interest to an investigation, all partially indexed items in the person of interest's selected data sources are re-indexed by a process called *Advanced indexing*. This job is also triggered when you click **Update index** in Index view on the **Processing** tab of an investigation. For more information, see [Advanced indexing of data for an investigation](index-data-people-of-interest.md).
|Running analytics | A user analyzes data in an evidence set by running analytics tools such as near duplicate detection, email threading analysis, and themes analysis. For more information, see [Run analytics to investigate faster](run-analytics-to-investigate-faster.md). | 
|Tagging documents | This job is triggered when a user clicks **Start tagging job** in the **Tagging panel** when reviewing documents in an evidence set. A user can start this job after tagging documents in an evidence set and then bulk-selecting them in the view document panel. For more information, see [Tag documents in evidence](tag-documents.md). | 
|||
