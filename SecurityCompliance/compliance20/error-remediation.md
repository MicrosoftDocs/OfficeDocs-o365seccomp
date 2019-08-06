---
title: "Error remediation when processing data"
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

# Error remediation when processing data

Error remediation allows eDiscovery administrators the ability to rectify data issues that prevent Advanced eDiscovery from properly processing the content. For example, files that are password protected can't be processed since the files are locked or encrypted. Using error remediation, eDiscovery administrators can download files with such errors, remove the password protection, and then upload the remediated files.

Use the following workflow to remediate files with errors in Advanced eDiscovery cases.

## Create an error remediation session to remediate files with processing errors

>[!NOTE]
>If the the error remediation wizard is closed at any time during the following procedure, you can return to the error remediation session from the **Processing** tab by selecting **Error remediations** in the **View** drop down menu.

1. On the **Processing** tab in an Advanced eDiscovery case, select **Errors** in the **View** drop-down menu.

2. Select the errors you want to remediate by clicking the radio button next to either the error type or file type.  In the following example, we're remediating a password protected file.

3. Click **New error remediation**.

    ![Error remediation](../media/8c2faf1a-834b-44fc-b418-6a18aed8b81a.png)

    The error remediation session starts with a preparation stage where the files with errors are copied to a Microsoft-provided Azure Storage location so that you can download them to your local computer to remediate.

    ![Preparing error remediation](../media/390572ec-7012-47c4-a6b6-4cbb5649e8a8.png)

4. After the preparation is complete, click **Next: Download files** to proceed with download.

    ![Download files](../media/6ac04b09-8e13-414a-9e24-7c75ba586363.png)

5. To download files, specify the **Destination path for download**. This is a path on your local computer where the file is downloaded.  The default path, %USERPROFILE%\Downloads\errors, points to the logged-in user's downloads folder. You can change this path if necessary. If you do change it, we recommend that you use a local file path for the best performance. Don't use a remote network path.

6. Copy the predefined command by clicking **Copy to clipboard**. Start a windows command prompt, paste the command, and then press **Enter**.  

    The files are downloaded.

    ![Prepare for error remediation](../media/f364ab4d-31c5-4375-b69f-650f694a2f69.png)

    > [!NOTE]
    > You must use AzCopy v8.1 to successfully use the command that's provided on the **Download files** page. You also must use AzCopy v8.1 to upload the files in step 10 below. To install this version of AzCopy, see [Transfer data with the AzCopy v8.1 on Windows](https://docs.microsoft.com/previous-versions/azure/storage/storage-use-azcopy). If the supplied AzCopy command fails, please see [Troubleshoot AzCopy in Advanced eDiscovery](troubleshooting-azcopy.md).

7. After downloading the files, you can remediate them with an appropriate tool. For password-protected files, there several password cracking tools you can use. If you know the passwords for the files, you can open them and remove the password protection.
    > [!NOTE]
    > IT is important that you retain the directory structure and file names of the remediated files in tact.  All naming conventions used in the downloaded files and folders make it possible to associate the remdiated files back to the original.

8. Now, return to Advanced eDiscovery and click **Next: Upload files**.  This will move to the next step where you can now upload the files.

    ![Upload Files](../media/af3d8617-1bab-4ecd-8de0-22e53acba240.png)

9. Specify the location of the remediated files in the **Path to location of files** text box, then click **Copy to clipboard**.

10. Paste the command into a Windows Command Prompt and press **Enter** to upload the files.

    ![ff2ff691-629f-4065-9b37-5333f937daf6.png](../media/ff2ff691-629f-4065-9b37-5333f937daf6.png)

11. Return to Advanced eDiscovery and click **Next: Process files**.

12. When processing is complete. You can return to the review set and see the remediated file.

## What happens when files are remediated

When remediated files are uploaded, the original metadata is preserved except for the following fields: 

- ExtractedTextSize
- HasText
- IsErrorRemediate
- LoadId
- ProcessingErrorMessage
- ProcessingStatus
- Text
- WordCount
- WorkingsetId

For a definition of all metadata fields in Advanced eDiscovery, see [Document metadata fields](document-metadata-fields.md).
