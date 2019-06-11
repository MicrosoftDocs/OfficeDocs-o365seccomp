---
title: "Create custom sensitive information types with Exact Data Match"
ms.reviewer: 
ms.author: deniseb
author: denisebmsft
manager: laurawi
audience: Admin
ms.topic: article
ms.service: O365-seccomp
ms.date: 05/15/2019
localization_priority: Priority
ms.collection: 
- M365-security-compliance
search.appverid: 
- MOE150
- MET150
description: "Create custom sensitive information types with Exact Data Match based classification."
---

# Create custom sensitive information types with Exact Data Match based classification (Preview)

## Overview

[Custom sensitive information types](custom-sensitive-info-types.md) are used to help prevent inadvertent or inappropriate sharing of sensitive information. As an administrator, you can use the [Security & Compliance Center](create-a-custom-sensitive-information-type.md) or [PowerShell](create-a-custom-sensitive-information-type-in-scc-powershell.md) to define a custom sensitive information type based on patterns, evidence (keywords such as *employee*, *badge*, *ID*, and so on), character proximity (how close evidence is to characters in a particular pattern), and confidence levels. Such custom sensitive information types meet business needs for many organizations.

But what if you wanted a custom sensitive information type that uses exact data values, instead of patterns and proximity? With Exact Data Match (EDM)-based classification, you can create a custom sensitive information type that is designed to:
- be dynamic and refreshable;
- be more scalable;
- result in fewer false-positives;
- work with structured sensitive data;
- handle sensitive information more securely; and
- be used with several Microsoft cloud services.

![EDM-based classification](media/EDMClassification.png)

EDM-based classification enables you to create custom sensitive information types that refer to exact values in a database of sensitive information. The database can be refreshed daily or weekly, and it can contain up to 10 million rows of data. So as employees, patients, or clients come and go, and records change, your custom sensitive information types remain current and applicable. And, you can use EDM-based classification with policies, such as [data loss prevention policies](data-loss-prevention-policies.md) (DLP) or [Microsoft Cloud App Security file policies](https://docs.microsoft.com/cloud-app-security/data-protection-policies).

## Required licenses and permissions

- You must be a global admin, compliance administrator, or Exchange Online administrator to perform the tasks described in this article. To learn more about DLP permissions, see [Permissions](data-loss-prevention-policies.md#permissions).

- When generally available, EDM-based classification will be included in the following subscriptions:
    - Office 365 E5
    - Microsoft 365 E5
    - Microsoft 365 Information Protection and Compliance
    - Office 365 Advanced Compliance

> [!NOTE]
> **EDM-based classification is currently in preview** for [DLP in Office 365](data-loss-prevention-policies.md) (with Exchange Online and Microsoft Teams) and [Cloud App Security](https://docs.microsoft.com/cloud-app-security). If your organization has [DLP capabilities](https://docs.microsoft.com/office365/servicedescriptions/exchange-online-protection-service-description/messaging-policy-and-compliance-servicedesc#data-loss-prevention-dlp), you can try EDM-based classification. If you are not already participating in the preview, [contact Microsoft](https://resources.office.com/us-landing-spe-contactus.html?LCID=EN-US) to get started. 

## The work flow at a glance

|Phase  |What's needed  |
|---------|---------|
|[Part 1: Set up EDM-based classification](#part-1-set-up-edm-based-classification)<br/><br/>(As needed)<br/>- [Edit the database schema](#editing-the-schema-for-edm-based-classification) <br/>- [Remove the schema](#removing-the-schema-for-edm-based-classification) |- Read access to the sensitive data<br/>- Database schema in .xml format (example provided)<br/>- Rule package in .xml format (example provided)<br/>- Admin permissions to the Security & Compliance Center (using PowerShell) |
|[Part 2: Index and upload the sensitive data](#part-2-index-and-upload-the-sensitive-data)<br/><br/>(As needed)<br/>[Refresh the data](#refreshing-your-sensitive-information-database) |- Custom security group and user account<br/>- Local admin access to machine with EDM Upload Agent<br/>- Read access to the sensitive data<br/>- Process and schedule for refreshing the data|
|[Part 3: Use EDM-based classification with your Microsoft cloud services](#part-3-use-edm-based-classification-with-your-microsoft-cloud-services) |- Office 365 subscription with DLP<br/>- EDM-based classification feature enabled (in preview) |

## Part 1: Set up EDM-based classification

Setting up and configuring EDM-based classification involves saving sensitive data in .csv format, defining a schema for your database of sensitive information, creating a rule package, and then uploading the schema and rule package.

### Define the schema for your database of sensitive information

1. Identify the sensitive information you want to use. Export the data to an app, such as Microsoft Excel, and save the file in .csv format. The data file can include:

    - Up to 10 million rows of sensitive data
    - Up to 32 columns (fields) per data source

2. Structure the sensitive data in the .csv file such that the first row includes the names of the fields used for EDM-based classification. In your .csv file, you might have field names, such as "ssn", "birthdate", "firstname", "lastname", and so on. As an example, our .csv file is called *PatientRecords.csv*, and its columns include *PatientID*, *MRN*, *lastname*, *FirstName*, *SSN* and more.

3. Define the schema for the database of sensitive information in .xml format (similar to our example below). Name this schema file `edm.xml`, and configure it such that for each column in the database, there is a line that uses the syntax `<Field name="" unique="" searchable=""/>`. 

    - Use column names for *Field name* values.
    - Use *unique="true"* for the fields that contain unique values (Social Security numbers, identification numbers, etc.); otherwise, use *unique="false"*.
    - Use *searchable="true"* for the fields that you want to be searchable. Do not specify more than five fields per database to be searchable. All the rest should have *searchable="false"*.  

    As an example, the following .xml file defines the schema for a patient records database, with five fields specified as searchable: *PatientID*, *MRN*, *SSN*, *Phone*, and *DOB*. 
    
    (You can copy, modify, and use our example.)
    
    ```<?xml version="1.0" encoding="utf-8"?>
    <EdmSchema xmlns="http://schemas.microsoft.com/office/2018/edm">
    	<DataStore name="PatientRecords" description="Schema for patient records" version="1">
    		<Field name="PatientID" unique="false" searchable="true" />
    		<Field name="MRN" unique="false" searchable="true" />
    		<Field name="FirstName" unique="false" searchable="false" />
    		<Field name="LastName" unique="false" searchable="false" />
    		<Field name="SSN" unique="false" searchable="true" />
    		<Field name="Phone" unique="false" searchable="true" />
    		<Field name="DOB" unique="false" searchable="true" />
    		<Field name="Gender" unique="false" searchable="false" />
    		<Field name="Address" unique="false" searchable="false" />
    	</DataStore>
    </EdmSchema>
    ```

4. [Connect to Office 365 Security & Compliance Center PowerShell](https://docs.microsoft.com/powershell/exchange/office-365-scc/connect-to-scc-powershell/connect-to-scc-powershell?view=exchange-ps).

5. To upload the database schema, run the following cmdlets, one at a time:

    `$edmSchemaXml=Get-Content .\edm.xml -Encoding Byte -ReadCount 0`

    `New-DlpEdmSchema -FileData $edmSchemaXml -Confirm:$true`

    You will be prompted to confirm, as follows:

       Confirm
       Are you sure you want to perform this action?
       New EDM Schema for the data store 'patientrecords' will be imported.
       [Y] Yes  [A] Yes to All  [N] No  [L] No to All  [?] Help (default is "Y"):

    > [!TIP]
    > If you want your changes to occur without confirmation, in Step 5, use this cmdlet instead: `New-DlpEdmSchema -FileData $edmSchemaXml`
    
Now that the schema for your database of sensitive information is defined, the next step is to set up a rule package. Proceed to the section [Set up a rule package](#set-up-a-rule-package).

#### Editing the schema for EDM-based classification 

(As needed) If you want to make changes to your edm.xml file, such as changing which fields are used for EDM-based classification, follow these steps:

1. Edit your edm.mxl file (this is the file discussed in the [Define the schema](#define-the-schema-for-your-database-of-sensitive-information) section of this article).

2. [Connect to Office 365 Security & Compliance Center PowerShell](https://docs.microsoft.com/powershell/exchange/office-365-scc/connect-to-scc-powershell/connect-to-scc-powershell?view=exchange-ps).

3. To update your database schema, run the following cmdlets, one at a time:

    `$edmSchemaXml=Get-Content .\edm.xml -Encoding Byte -ReadCount 0`

    `Set-DlpEdmSchema -FileData $edmSchemaXml -Confirm:$true`

    You will be prompted to confirm, as follows:

       Confirm
       Are you sure you want to perform this action?
       EDM Schema for the data store 'patientrecords' will be updated.
       [Y] Yes  [A] Yes to All  [N] No  [L] No to All  [?] Help (default is "Y"):

    > [!TIP]
    > If you want your changes to occur without confirmation, in Step 3, use this cmdlet instead: `Set-DlpEdmSchema -FileData $edmSchemaXml`

#### Removing the schema for EDM-based classification

(As needed) If you want to remove the schema you're using for EDM-based classification, follow these steps:

1. [Connect to Office 365 Security & Compliance Center PowerShell](https://docs.microsoft.com/powershell/exchange/office-365-scc/connect-to-scc-powershell/connect-to-scc-powershell?view=exchange-ps).

2. Run the following PowerShell cmdlet, substituting the data store name of "patientrecords" with the one you want to remove:

    `Remove-DlpEdmSchema -Identity patientrecords`

     You will be prompted to confirm, as follows:
    
       Confirm
       Are you sure you want to perform this action?
       EDM Schema for the data store 'patientrecords' will be removed.
       [Y] Yes  [A] Yes to All  [N] No  [L] No to All  [?] Help (default is "Y"):
    
    > [!TIP]
    > If you want your changes to occur without confirmation, in Step 2, use this cmdlet instead: `Remove-DlpEdmSchema -Identity patientrecords -Confirm:$false`

### Set up a rule package

1. Create a rule package in .xml format (with Unicode encoding), similar to the following example. (You can copy, modify, and use our example.) 

   Recall from the previous procedure that our PatientRecords schema defines five fields as searchable: *PatientID*, *MRN*, *SSN*, *Phone*, and *DOB*. Our example rule package includes those fields and references the database schema file (edm.xml), with one *ExactMatch* items per searchable field. Consider the following ExactMatch item:

   ```
    <ExactMatch id = "E1CC861E-3FE9-4A58-82DF-4BD259EAB371" patternsProximity = "300" dataStore ="PatientRecords" recommendedConfidence = "65" >
      <Pattern confidenceLevel="65">
        <idMatch matches = "SSN" classification = "U.S. Social Security Number (SSN)" />
      </Pattern>
    </ExactMatch>
   ```

    In this example, note the following:

    - The dataStore name references the .csv file we created earlier: **dataStore = "PatientRecords"**.
    - The idMatch value references a searchable field that is listed in the database schema file: **idMatch matches = "SSN"**.
    - The classification value references an existing or custom sensitive information type: **classification = "U.S. Social Security Number (SSN)"**. (In this case, we use the existing sensitive information type of U.S. Social Security Number.)

    When you set up your rule package, make sure to correctly reference your .csv file and edm.xml file. (You can copy, modify, and use our example.) 

    ```<?xml version="1.0" encoding="utf-8"?>
    <RulePackage xmlns="http://schemas.microsoft.com/office/2018/edm">
      <RulePack id="fd098e03-1796-41a5-8ab6-198c93c62b11">
        <Version build="0" major="2" minor="0" revision="0" />
        <Publisher id="eb553734-8306-44b4-9ad5-c388ad970528" />
        <Details defaultLangCode="en-us">
          <LocalizedDetails langcode="en-us">
            <PublisherName>IP DLP</PublisherName>
            <Name>Health Care EDM Rulepack</Name>
            <Description>This rule package contains the EDM sensitive type for health care sensitive types.</Description>
          </LocalizedDetails>
        </Details>
      </RulePack>
      <Rules>
        <ExactMatch id = "E1CC861E-3FE9-4A58-82DF-4BD259EAB371" patternsProximity = "300" dataStore ="PatientRecords" recommendedConfidence = "65" >
          <Pattern confidenceLevel="65">
            <idMatch matches = "SSN" classification = "U.S. Social Security Number (SSN)" />
          </Pattern>
          <Pattern confidenceLevel="75">
            <idMatch matches = "SSN" classification = "U.S. Social Security Number (SSN)" />
            <Any minMatches ="3" maxMatches ="100">
              <match matches="PatientID" />
              <match matches="MRN"/>
              <match matches="FirstName"/>
              <match matches="LastName"/>
              <match matches="Phone"/>
              <match matches="DOB"/>
            </Any>
          </Pattern>
        </ExactMatch>
        <LocalizedStrings>
          <Resource idRef="E1CC861E-3FE9-4A58-82DF-4BD259EAB371">
            <Name default="true" langcode="en-us">Patient SSN Exact Match.</Name>
            <Description default="true" langcode="en-us">EDM Sensitive type for detecting Patient SSN.</Description>
          </Resource>
        </LocalizedStrings>
      </Rules>
    </RulePackage>
    ```
    
2. Upload the rule package by running the following PowerShell cmdlets, one at a time:

    `$rulepack=Get-Content .\rulepack.xml -Encoding Byte -ReadCount 0`

    `New-DlpSensitiveInformationTypeRulePackage -FileData $rulepack`

At this point, you have set up EDM-based classification. The next step is to index the sensitive data, and then upload the indexed data. 

## Part 2: Index and upload the sensitive data

During this phase, you set up a custom security group and user account, and set up the EDM Upload Agent tool. Then, you use the tool to index the sensitive data, and upload the indexed data.

### Set up the security group and user account

1. As a global administrator, go to the admin center ([https://admin.microsoft.com](https://admin.microsoft.com)) and [create a security group](https://docs.microsoft.com/office365/admin/email/create-edit-or-delete-a-security-group?view=o365-worldwide) called `EDM_DataUploaders`. 

2. Add one or more users to the *EDM_DataUploaders* security group. (These users will manage the database of sensitive information.)

3. Make sure each user who is managing the sensitive data is a local admin on the machine used for the EDM Upload Agent.

### Set up the EDM Upload Agent

> [!NOTE]
> Before you begin this procedure, make sure that you are a member of the *EDM_DataUploaders* security group and a local admin on your machine.

1. Download and install the EDM Upload Agent at [https://go.microsoft.com/fwlink/?linkid=2088639](https://go.microsoft.com/fwlink/?linkid=2088639). By default, the installation location should be `C:\Program Files\Microsoft\EdmUploadAgent`. 

2. To authorize the EDM Upload Agent, open Windows Command Prompt (as an administrator), and then run the following command:

    `EdmUploadAgent.exe /Authorize`

3. Sign in with your work or school account for Office 365.

The next step is to use the EDM Upload Agent to index the sensitive data, and then upload the indexed data.

### Index and upload the sensitive data

1. Save the sensitive data file (recall our example is *PatientRecords.csv*) to the local drive on the machine. (We saved our example *PatientRecords.csv* file to `C:\Edm\Data`.)

2. To index the sensitive data, run the following command in Windows Command Prompt:

    `EdmUploadAgent.exe /CreateHash /DataStoreName <DataStoreName> /DataFile <DataFilePath> /HashLocation <HashedFileLocation>`

    Example: **EdmUploadAgent.exe /CreateHash /DataStoreName PatientRecords /DataFile C:\Edm\Data\PatientRecords.csv /HashLocation C:\Edm\Hash** 

3. To upload the indexed data, run the following command in Windows Command Prompt:

    `EdmUploadAgent.exe /UploadHash /DataStoreName <DataStoreName> /HashFile <HashedSourceFilePath>`

    Example: **EdmUploadAgent.exe /UploadHash /DataStoreName PatientRecords /HashFile C:\Edm\Hash\PatientRecords.EdmHash** 

4. To verify your sensitive data has been uploaded, run the following command in Windows Command Prompt:

    `EdmUploadAgent.exe /GetDataStore`

    You'll see a list of data stores and when they were last updated, similar to the following: <br/>![Example of GetDataStore cmdlet and results](media/EDM-GetDataStore-example.png)

5. Proceed to set up your process and schedule for [Refreshing your sensitive information database](#refreshing-your-sensitive-information-database).

At this point, you are ready to use EDM-based classification with your Microsoft cloud services. For example, you can [set up a DLP policy using EDM-based classification](#to-create-a-dlp-policy-with-edm). 

### Refreshing your sensitive information database

You can refresh your sensitive information database daily or weekly, and the EDM Upload Tool can reindex the sensitive data and then reupload the indexed data. 

1. Determine your process and frequency (daily or weekly) for refreshing the database of sensitive information.

2. Re-export the sensitive data to an app, such as Microsoft Excel, and save the file in .csv format. Keep the same file name and location you used when you followed the steps described in [Index and upload the sensitive data](#index-and-upload-the-sensitive-data).

    > [!NOTE]
    > If there are no changes to the structure (field names) of the .csv file, you won't need to make any changes to your database schema file when you refresh the data. But if you must make changes, make sure to edit the [database schema](#editing-the-schema-for-edm-based-classification) and your [rule package](#set-up-a-rule-package) accordingly.        

3. Use [Task Scheduler](https://docs.microsoft.com/windows/desktop/TaskSchd/task-scheduler-start-page) to automate steps 2 and 3 in the [Index and upload the sensitive data](#index-and-upload-the-sensitive-data) procedure. You can schedule tasks using several methods:
    
    |Method  |What to do  |
    |---------|---------|
    |Windows PowerShell     |See the [ScheduledTasks](https://docs.microsoft.com/powershell/module/scheduledtasks/?view=win10-ps) documentation and the [example PowerShell script](#example-powershell-script-for-task-scheduler) in this article|
    |Task Scheduler API |See the [Task Scheduler](https://docs.microsoft.com/windows/desktop/TaskSchd/using-the-task-scheduler) documentation |
    |Windows user interface     |In Windows, click **Start**, and type `Task Scheduler`. Then, in the list of results, right-click **Task Scheduler**, and choose **Run as administrator**.          |

#### Example PowerShell script for Task Scheduler

This section includes an example PowerShell script you can use to schedule your tasks for indexing data and uploading the indexed data:

```powershell
param([string]$dataStoreName,[string]$fileLocation)
# Assuming current user is also the user context to run the task
$user = "$env:USERDOMAIN\$env:USERNAME"
$edminstallpath = 'C:\Program Files\Microsoft\EdmUploadAgent\'
$edmuploader = $edminstallpath + 'EdmUploadAgent.exe'
$csvext = '.csv'
$edmext = '.EdmHash'
# Assuming CSV file name is same as data store name
$dataFile = "$fileLocation\$dataStoreName$csvext"
$hashFile = "$fileLocation\$dataStoreName$edmext"
# Assuming location to store hash file is same as the location of csv file
$hashLocation = $fileLocation
$createHashArgs = '/CreateHash /DataStoreName ' + $dataStoreName + ' /DataFile ' + $dataFile + ' /HashLocation ' + $hashLocation
$uploadHashArgs = '/UploadHash /DataStoreName ' + $dataStoreName + ' /HashFile ' + $hashFile
# Set up actions associated with the task
$actions = @()
$actions += New-ScheduledTaskAction -Execute $edmuploader -Argument $createHashArgs -WorkingDirectory $edminstallpath
$actions += New-ScheduledTaskAction -Execute $edmuploader -Argument $uploadHashArgs -WorkingDirectory $edminstallpath
# Set up trigger for the task
$trigger = New-ScheduledTaskTrigger -Weekly -DaysOfWeek Sunday -At 2am
# Set up task settings
$principal = New-ScheduledTaskPrincipal -UserId $user -LogonType S4U -RunLevel Highest
$settings = New-ScheduledTaskSettingsSet -RunOnlyIfNetworkAvailable -StartWhenAvailable -WakeToRun
# Create the scheduled task
$scheduledTask = New-ScheduledTask -Action $actions -Principal $principal -Trigger $trigger -Settings $settings
# Get credentials to run the task
$creds = Get-Credential -UserName $user -Message "Enter credentials to run the task"
$password=[Runtime.InteropServices.Marshal]::PtrToStringAuto([Runtime.InteropServices.Marshal]::SecureStringToBSTR($creds.Password))
# Register the scheduled task
$taskName = 'EDMUpload_' + $dataStoreName
Register-ScheduledTask -TaskName $taskName -InputObject $scheduledTask -User $user -Password $password
```
## Part 3: Use EDM-based classification with your Microsoft cloud services

You can use EDM-based classification with information protection features, such as [Office 365 DLP policies](data-loss-prevention-policies.md) and [Microsoft Cloud App Security file policies](https://docs.microsoft.com/cloud-app-security/data-protection-policies). The following procedure describes how to use EDM with a DLP policy that is created in the Office 365 Security & Compliance Center.

### To create a DLP policy with EDM

1. Go to the Security & Compliance Center ([https://protection.office.com](https://protection.office.com)).

2. Choose **Data loss prevention** > **Policy**.

3. Choose **Create a policy** > **Custom** > **Next**.

4. On the **Name your policy** tab, specify a name and description, and then choose **Next**.

5. On the **Choose locations** tab, select **Let me choose specific locations**, and then choose **Next**.<br/>![Choose locations option](media/DLP-EDM-newpolicy-chooselocations.png)<br/>

6. In the **Status** column, select **Exchange email** only, and then choose **Next**. <br/>![EDM policy with Exchange only](media/EDM-DLPpolicy-ExchangeOnly.png)<br/>

7. On the **Policy settings** tab, choose **Use advanced settings**, and then choose **Next**.<br/>![Use advanced settings](media/edm-dlp-policy-advancedsettings.png)<br/>

8. Choose **+ New rule**.<br/>![Create a rule](media/edm-dlp-newrule.png)<br/>

9. In the **Name** section, specify a name and description for the rule.<br/>![New rule fields](media/edm-dlp-newruleform.png)<br/>

10. In the **Conditions** section, in the **+ Add a condition** list, choose **Content contains sensitive type**.<br/>![Content contains sensitive info types](media/edm-dlp-newrule-conditions.png)<br/>

11. Search for the sensitive information type you created when you set up your rule package, and then choose **+ Add**.<br/>![Find the sensitive info type](media/edm-dlp-newrulefindsensitiverulepack.png)<br/>Then choose **Done**.

12. Finish selecting options for your rule, such as **User notifications**, **User overrides**, **Incident reports**, and so on, and then choose **Save**.

13. On the **Policy settings** tab, review your rules, and then choose **Next**.

14. Specify whether to turn on the policy right away, test it out, or keep it turned off. Then choose **Next**.

15. On the **Review your settings** tab, review your policy. Make any needed changes. When you're ready, choose **Create**.

    > [!NOTE]
    > Allow approximately one hour for your new DLP policy to work its way through your data center.

## Related articles

[Built-in sensitive information types and what they look for](what-the-sensitive-information-types-look-for.md)

[Custom sensitive information types](custom-sensitive-info-types.md)

[Overview of DLP policies](data-loss-prevention-policies.md)

[Microsoft Cloud App Security](https://docs.microsoft.com/cloud-app-security)
