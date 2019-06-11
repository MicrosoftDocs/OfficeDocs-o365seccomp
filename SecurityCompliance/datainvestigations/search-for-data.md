---
title: "Search for data in an investigation"
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

# Search for data in an investigation

On the **Search** tab in a data investigation, you can search for misplaced, confidential, or sensitive data in content locations in Office 365 using keywords and conditions. 

After you run a search, you can view statistics on the items returned by the search, such as the content locations that had the most items that matched the search query. You can also preview a subset of the results. After you've identified the set of documents that want to further investigate, you can add the results of the search to an evidence set to further process and analyze.

## Create a search

1. In an investigation, click the **Searches** tab, and then click **New search**. 

    A wizard is displayed that will guide you through the process of creating a search.

2. Enter a search name and an optional description for the search.

3. Define your search criteria. You can add conditions for the search by using the pre-built condition cards or by using search property names in the keyword query. For more information, see [Build search queries](build-search-queries.md).

4. Choose the content locations (data sources) to search. You can scope the search by selecting the content locations of specific people of interest (if you added any to the investigation). If you have added people of interest to the investigation, you can add them by following the steps in [Manage people of interest](manage-people-of-interest.md#add-people-of-interest).
 
    In some cases, you may first need to search all content locations in your organization; alternatively, you may need to search locations that aren't owned by a specific person. In this scenarios, you can choose to search your entire organization, or all locations for a specific Office 365 services (such as Exchange, SharePoint, OneDrive of Business, or Teams.

5. Save and run the search.

After the search is created, a flyout page is displayed with details about the search. Note that the **Statistics** and **Preview** buttons are initially grayed out because the search hasn't completed. You can keep track of the progress of by monitoring the **Status** column on the **Searches** tab.

## View statistics and search results

After you create and start a data investigation search, the tool uses the search criteria (the search query and content locations) that you defined and searches an index in the live service for items that match your search criteria. There are three components of a search that are returned when the search is complete: 

- **Estimate** - Because the search only searches an index (rather than the actual content locations), the results of a search are an estimate (based on what was found in the index that matched the search results). A summary of the estimate is displayed on the search flyout page under **Status**. Note that the status for the estimate process for a search is displayed on the **Searches** tab in the **Estimate status** column. When the search estimate is complete, this status is set to **Successful**.

- **Statistics** - Statistics provide more detailed information about the search results. This includes the following:

    - Summary - Statistics similar to the search estimate results displayed on the flyout page.
    - Top locations - Statistics about the number of items that match the search query in each content location that was searched. 
    - Queries - Detailed statistics about the search query, including the number of items that match each condition in a search query.

    Click **Statistics** on the flyout page to view these statistics. Note that this button is inactive until the value of the **Estimate status** on the **Searches** tab is set to **Successful**. For more information about search statistics, see [Search statistics](search-statistics.md).

- **Preview** - When the search is complete, you can view the actual items from a sample subset of the search results returned by the search. YOu can view in the native view of the item type, any you can also view metadata about the item. This is a good way to quickly determine if your search results are what you expected or if you need to edit the search and re-run it. Click  **Preview** on the flyout page to view items from the search results. Note that this button is inactive until the value of the **Preview status** on the **Searches** tab is set to **Successful**.
 
> [!NOTE]
> The status values for the **Estimate status** and **Preview status** columns on the **Searches** tab are **Submitted**, **In progress**, and **Successful**. If there is an error with the search, the status of **Failed** is displayed.

## Add search results to evidence

When you're satisfied with the results of a search and you're ready to analyze and remediate those search results, you can add them to an evidence set in the investigation. When you add items to an evidence set on the **Evidence** tab, the following two things occur:

- All items in the search results are copied from the data source in the live service, and copied to a secure Azure storage location in the Microsoft cloud.

- All items (including the content and metadata) are re-indexed so that all data in the evidence set is fully searchable during your investigation. Re-indexing the data results in thorough and very fast searches when you search the data in the evidence set during your investigation.

One advantage of copying the live data to an evidence set in Azure is that for time-sensitive or critical incidents, you can quickly contain the damage by immediately deleting suspicious content in the original data source in the live service and then investigating the incident by analyzing the evidence that was copied to the quarantined environment of the Azure storage location. 

Copying the original data to the evidence set also facilitates your investigation by providing you with advanced analytics tools such as themes detection, near-duplicate detection, and email thread identification.

If necessary, you can also add data from non-Office 365 data sources to an evidence set so that it's stored along with the data you collect from Office 365.

To add data to an an evidenced set, select a search on the **Searches** tab, and then clicking **Add results to evidence** on the flyout page. Note that you can add data to an existing evidence set or create a new evidence set on the fly.

### Tracking the progress of adding search results to evidence

Adding data to an evidence set is a long-running process. The process includes collecting the items the original data source from Office 365 ( for example, from mailboxes and sites), copying them to the Azure storage location (this copying process is also called *ingestion*), and then re-indexing the items. You can either track the progress on the **Jobs** tab or on the **Searches** tab in the **Added data to evidence** column. After the processing of evidence processing is completed, you can go to the **Evidence** tab, click the evidence set, and then start your investigation by searching, reviewing, tagging, and exporting the relevant data as necessary.
