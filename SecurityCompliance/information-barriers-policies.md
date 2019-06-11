---
title: "Define information barrier policies"
ms.reviewer: 
ms.author: deniseb
author: denisebmsft
manager: laurawi
ms.date: 05/31/2019
ms.audience: ITPro
ms.topic: article
ms.service: O365-seccomp
ms.collection:
- M365-security-compliance
localization_priority: None
description: "Learn how to define policies for information barriers in Microsoft Teams."
---

# Define policies for information barriers (Preview)

With information barriers, you can define policies that are designed to prevent certain segments of users from communicating with each other, or allow specific segments to communicate only with certain other segments. Information barrier policies can help your organization maintain compliance with relevant industry standards and regulations, and avoid potential conflicts of interest. To learn more, see [Information barriers (Preview)](information-barriers.md). 

> [!IMPORTANT]
> This article describes how to plan, define, implement, and manage information barrier policies. Several steps are involved, and the work flow is divided into several parts. Make sure to read through the [prerequisites](#prerequisites) and the entire process before you begin defining (or editing) information barrier policies.

## Concepts of information barrier policies

Before you plan, define, and implement information barrier policies, get to know the underlying concepts. With information barriers, you'll work with user account attributes, segments, information barrier policies, and a policy application process described in this article. 

- **User account attributes** are defined in Azure Active Directory (or Exchange Online). These attributes can include department, job title, location, team name, etc. 

- **Segments** are defined in the Office 365 Security & Compliance Center using a selected **user account attribute**, such as department, job title, location, team name, or any [supported attribute](information-barriers-attributes.md). Defining segments does not effect users; it just sets the stage for information barrier policies to be defined and then applied.

- **Information barrier policies** are defined and assigned to individual **Segments**. Not all segments will have a policy assigned. In addition, no single segment can be assigned more than one policy. When you define policies, you choose from two kinds of policies:
    - Policies that prevent one segment from communicating with another segment
    - Policies that allow one segment to communicate with only certain other segments

    Ideally, you'll use the minimum number of policies to ensure your organization is compliant with legal and industry requirements.

- **Policy application** is done after all information barrier policies are defined, and you are ready to apply them in your organization.

## The work flow at a glance

|Phase    |What's involved  |
|---------|---------|
|[Make sure prerequisites are met](#prerequisites)     |- Confirm that your subscription includes information barriers<br/>- Verify that you have the necessary permissions to define/edit segments and policies<br/>- Make sure that your directory data reflects your organization's structure<br/>- Make sure that scoped directory search is enabled in Microsoft Teams<br/>- Make sure audit logging is turned on<br/>- Use PowerShell to perform the tasks in this article (example cmdlets are provided)<br/>- Provide admin consent for information barriers in Microsoft Teams (steps are included)          |
|[Part 1: Segment all the users in your organization](#part-1-segment-users)     |- Determine what policies are needed<br/>- Make a list of segments to define<br/>- Identify which attributes to use<br/>- Define segments in terms of policy filters        |
|[Part 2: Define information barrier policies](#part-2-define-information-barrier-policies)     |- Define your policies (do not apply yet)<br/>- Choose from two kinds (block or allow) |
|[Part 3: Apply information barrier policies](#part-3-apply-information-barrier-policies)     |- Set policies to active status<br/>- Run the policy application<br/>- Verify policy status         |
|(As needed) [Edit a segment or a policy](#edit-a-segment-or-a-policy)     |- Edit a segment<br/>- Edit or remove a policy<br/>- Run the policy application<br/>- Verify policy status         |
|(As needed) [Troubleshooting](information-barriers-troubleshooting.md)|- Take action when policies are not working as expected|

## Prerequisites

**Currently, the information barrier feature is in private preview**. When these features are generally available, they'll be included in subscriptions, such as:

- Microsoft 365 E5
- Office 365 E5
- Office 365 Advanced Compliance
- Microsoft 365 E5 Information Protection and Compliance

For more details, see [Compliance Solutions](https://products.office.com/business/security-and-compliance/compliance-solutions).

### Permissions

To define or edit information barrier policies, **you must be assigned an appropriate role**, such as one of the following:
- Microsoft 365 Enterprise Global Administrator
- Office 365 Global Administrator
- Compliance Administrator
- IB Compliance Management (this is a new role!)

To learn more about roles and permissions, see [Permissions in the Office 365 Security & Compliance Center](permissions-in-the-security-and-compliance-center.md).
       
### Directory data

**Make sure that your organization's structure is reflected in directory data**. To do this, make sure that user account attributes, such as group membership, department name, etc. are populated correctly in Azure Active Directory (or Exchange Online). To learn more, see the following resources:
- [Attributes for information barrier policies (Preview)](information-barriers-attributes.md)
- [Add or update a user's profile information using Azure Active Directory](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-users-profile-azure-portal)
- [Configure user account properties with Office 365 PowerShell](https://docs.microsoft.com/office365/enterprise/powershell/configure-user-account-properties-with-office-365-powershell)

### Scoped directory search

**Before you define your organization's first information barrier policy, you must [enable scoped directory search in Microsoft Teams](https://docs.microsoft.com/MicrosoftTeams/teams-scoped-directory-search)**. Wait at least 24 hours after enabling scoped directory search before you set up or define information barrier policies.

### Audit logging

In order to look up the status of a policy application, audit logging must be turned on. We recommend doing this before you begin to define segments or policies. To learn more, see [Turn Office 365 audit log search on or off](turn-audit-log-search-on-or-off.md).

### PowerShell

**Currently, information barrier policies are defined and managed in the Office 365 Security & Compliance Center using PowerShell cmdlets**. Although several scenarios and examples are provided in this article, you'll need to be familiar with PowerShell cmdlets and parameters. 

[Connect to Office 365 Security & Compliance Center PowerShell](https://docs.microsoft.com/powershell/exchange/office-365-scc/connect-to-scc-powershell/connect-to-scc-powershell?view=exchange-ps).

### Provide admin consent for information barriers in Microsoft Teams

Use the following procedure to enable information barrier policies to work as expected in Microsoft Teams. 

For example, when your policies are in place, information barriers can remove people from chat sessions they are not supposed to be in. This helps ensure your organization remains compliant with policies and regulations. 

1. Run the following PowerShell cmdlets:

    ```
    Login-AzureRmAccount 
    $appId="bcf62038-e005-436d-b970-2a472f8c1982" 
    $sp=Get-AzureRmADServicePrincipal -ServicePrincipalName $appId
    if ($sp -eq $null) { New-AzureRmADServicePrincipal -ApplicationId $appId }
    Start-Process  "https://login.microsoftonline.com/common/adminconsent?client_id=$appId"
    ```

2. When prompted, sign in using your work or school account for Office 365.

3. In the **Permissions requested** dialog box, review the information, and then choose **Accept**.

## Part 1: Segment users

During this phase, you determine what policies are needed, make a list of segments to define, and then define your segments.

### Determine what policies are needed

Considering legal and industry regulations, who are the groups within your organization who will need information barrier policies? Make a list. Are there any groups who should be prevented from communicating with another group? Are there any groups that should be allowed to communicate only with one or two other groups? Think about the policies you need as belonging to one of two groups:
- **Blocking policies** that prevent one group from communicating with another group
- **Allow policies** that allow certain groups to communicate with only certain other groups.

When you have your initial list of groups and policies, proceed to identify the segments you'll need.

(See [Example: Contoso's departments and plan](#contosos-departments-and-plan) in this article.)

### Identify segments

In addition to your initial list of policies, make a list of segments for your organization. Every user in your organization should belong to a segment, and no user should belong to two or more segments. Each segment can have only one information barrier policy applied. 

Determine which attributes in your organization's directory data you'll use to define segments. You can use *Department*, *MemberOf*, or any of the supported attributes. Make sure that you have values in the attribute you select for all users. To see a list of supported attributes, refer to [Attributes for information barrier policies (Preview)](information-barriers-attributes.md).

> [!IMPORTANT]
> **Before you proceed to the next section, make sure your directory data has values for attributes that you can use to define segments**. If your directory data does not have values for the attributes you want to use, then all user accounts must be updated to include that information before you proceed with information barriers. To get help with this, see the following resources:<br/>- [Configure user account properties with Office 365 PowerShell](https://docs.microsoft.com/office365/enterprise/powershell/configure-user-account-properties-with-office-365-powershell)<br/>- [Add or update a user's profile information using Azure Active Directory](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-users-profile-azure-portal)

### Define segments using PowerShell

> [!IMPORTANT]
> **Make sure that your segments do not overlap**. Each user in your organization should belong to one (and only one) segment. No user should belong to two or more segments. Segments should be defined for all users in your organization. (See [Example: Contoso's defined segments](#contosos-defined-segments) in this article.)

1. To define an organizational segment, use the **New-OrganizationSegment** cmdlet with the **UserGroupFilter** parameter that corresponds to the [attribute](information-barriers-attributes.md) you want to use. 

    Syntax: `New-OrganizationSegment -Name "segmentname" -UserGroupFilter "attribute -eq 'attributevalue'"`

    Example: `New-OrganizationSegment -Name "HR" -UserGroupFilter "Department -eq 'HR'"`

    In this example, a segment called *HR* is defined using *HR*, a value in the Department attribute.

2. Repeat step 1 for each segment you want to define.

    After you run each cmdlet, you should see a list of details about the new segment. Details include the segment's type, who created or last modified it, and so on. 

After you have defined your segments, proceed to define information barrier policies.

## Part 2: Define information barrier policies

With your list of user segments and the information barrier policies you want to define, select a scenario, and then follow the steps. 

> [!IMPORTANT]
> **Make sure that as you define policies, you do not assign more than one policy to a segment**. For example, if you define one policy for a segment called *Sales*, do not define an additional policy for *Sales*. 

Determine whether you need to prevent communications between certain segments, or limit communications to certain segments. Choose between the scenarios below to define your policies.

- [Scenario 1: Block communications between segments](#scenario-1-block-communications-between-segments)
- [Scenario 2: Allow a segment to communicate only with one other segment](#scenario-2-allow-a-segment-to-communicate-only-with-one-other-segment)

> [!NOTE]
> As you define information barrier policies, make sure to set those policies to inactive status until you are ready to apply them. Defining (or editing) policies does not affect users until those policies are set to active status and then applied.

(See [Example: Contoso's information barrier policies](#contosos-information-barrier-policies) in this article.)

### Scenario 1: Block communications between segments

When you want to block segments from communicating with each other, you define two policies: one for each direction. Each policy blocks communication one way only.

For example, suppose you want to block communications between Segment A and Segment B. In this case, you define one policy preventing Segment A from communicating with Segment B, and then define a second policy to prevent Segment B from communicating with Segment A.

1. To define your first blocking policy, use the **New-InformationBarrierPolicy** cmdlet with the **SegmentsBlocked** parameter. 

    Syntax: `New-InformationBarrierPolicy -Name "policyname" -AssignedSegment "segmentname" -SegmentsBlocked "segmentname"`

    Example: `New-InformationBarrierPolicy -Name "Sales-Research" -AssignedSegment "Sales" -SegmentsBlocked "Research" -State Inactive`

    In this example, we defined a policy called *Sales-Research* for a segment called *Sales*. When active and applied, this policy prevents people in *Sales* from communicating with people in a segment called *Research*.

2. To define your second blocking segment, use the **New-InformationBarrierPolicy** cmdlet with the **SegmentsBlocked** parameter again, this time with the segments reversed.

    Example: `New-InformationBarrierPolicy -Name "Research-Sales" -AssignedSegment "Research" -SegmentsBlocked "Sales" -State Inactive`

    In this example, we defined a policy called *Research-Sales* to prevent Research from communicating with Sales.
 
2. Proceed to one of the following:

   - (If needed) [Define a policy to allow a segment to communicate only with one other segment](#scenario-2-allow-a-segment-to-communicate-only-with-one-other-segment) 
   - (After all your policies are defined) [Apply information barrier policies](#part-3-apply-information-barrier-policies)

### Scenario 2: Allow a segment to communicate only with one other segment

1. To allow one segment to communicate with only one other segment, use the **New-InformationBarrierPolicy** cmdlet with the **SegmentsAllowed** parameter. 

    Syntax: `New-InformationBarrierPolicy -Name "policyname" -AssignedSegment "segmentname" -SegmentsAllowed "segmentname"`

    Example: `New-InformationBarrierPolicy -Name "Manufacturing-HR" -AssignedSegment "Manufacturing" -SegmentsAllowed "HR" -State Inactive`

    In this example, we defined a policy called *Manufacturing-HR* for a segment called *Manufacturing*. When active and applied, this policy allows people in *Manufacturing* to communicate only with people in a segment called *HR*. (In this case, Manufacturing cannot communicate with users who are not part of HR.)

    **If needed, you can specify multiple segments with this cmdlet, as shown in the following two examples.**

    Syntax: `New-InformationBarrierPolicy -Name "policyname" -AssignedSegment "segmentname" -SegmentsAllowed "segmentname, segmentname"`

    **Example 1: Define a policy to allow multiple segments to communicate with only one other segment**

    `New-InformationBarrierPolicy -Name "ResearchManufacturing-HR" -AssignedSegment "Research, Manufacturing" -SegmentsAllowed "HR" -State Inactive`

    In this example, we defined a policy that allows the *Research* and *Manufacturing* segments to communicate only with *HR*.

    **Example 2: Define a policy to allow multiple segments to communicate with only certain other segments**    

    `New-InformationBarrierPolicy -Name "SalesMarketing-HRManufacturing" -AssignedSegment "Sales, Marketing" -SegmentsAllowed "HR, Manufacturing" -State Inactive`

    In this example, we defined a policy that allows the *Sales* and *Marketing* segments to communicate with only *HR* and *Manufacturing*.

    Repeat this step for each policy you want to define to allow specific segments to communicate with only certain other specific segments.

2. Proceed to one of the following:

   - (If needed) [Define a policy to block communications between segments](#scenario-1-block-communications-between-segments) 
   - (After all your policies are defined) [Apply information barrier policies](#part-3-apply-information-barrier-policies)

## Part 3: Apply information barrier policies

Information barrier policies are not in effect until you set them to active status, and then apply the policies.

1. Use the **Get-InformationBarrierPolicy** cmdlet to see a list of policies that have been defined. Note the status and identity (GUID) of each policy.

    Syntax: `Get-InformationBarrierPolicy`

2. To set a policy to active status, use the **Set-InformationBarrierPolicy** cmdlet with an **Identity** parameter, and the **State** parameter set to **Active**. 

    Syntax: `Set-InformationBarrierPolicy -Identity GUID -State Active`

    Example: `Set-InformationBarrierPolicy -Identity 43c37853-ea10-4b90-a23d-ab8c93772471 -State Active`
    
    In this example, we set an information barrier policy that has the GUID *43c37853-ea10-4b90-a23d-ab8c93772471* to active status.

    Repeat this step as appropriate for each policy.

3. When you have finished setting your information barrier policies to active status, use the **Start-InformationBarrierPoliciesApplication** cmdlet in the Office 365 Security & Compliance Center.

    Syntax: `Start-InformationBarrierPoliciesApplication`

    After approximately a half hour, policies are applied, user by user, for your organization. If your organization is large, it can take 24 hours (or more) for this process to complete. (As a general guideline, it takes about an hour to process 5,000 user accounts.)

## Verify status of user accounts, segments, policies, or policy application

Using PowerShell, you can verify status of user accounts, segments, policies, and policy application, as listed in the following table.

|To verify this  |Do this  |
|---------|---------|
|User accounts     |Use the **Get-InformationBarrierRecipientStatus** cmdlet with Identity parameters. <p>Syntax: `Get-InformationBarrierRecipientStatus -Identity <value> -Identity2 <value>` <p>You can use any value that uniquely identifies each user, such as name, alias, distinguished name, canonical domain name, email address, or GUID. <p>Example: `Get-InformationBarrierRecipientStatus -Identity meganb -Identity2 alexw` <p>In this example, we refer to two user accounts in Office 365: *meganb* for *Megan*, and *alexw* for *Alex*. <p>(You can also use this cmdlet for a single user: `Get-InformationBarrierRecipientStatus -Identity <value>`) <p>This cmdlet returns information about users, such as attribute values and any information barrier policies that are applied.|
|Segments     |Use the **Get-OrganizationSegment** cmdlet.<p>Syntax: `Get-OrganizationSegment` <p>This will display a list of all segments defined for your organization.         |
|Information barrier policies     |Use the **Get-InformationBarrierPolicy** cmdlet. <p> Syntax: `Get-InformationBarrierPolicy` <p>This will display a list of information barrier policies that were defined, and their status.       |
|The most recent information barrier policy application     | Use the **Get-InformationBarrierPoliciesApplicationStatus** cmdlet. <p>Syntax: `Get-InformationBarrierPoliciesApplicationStatus`<p>    This will display information about whether policy application completed, failed, or is in progress.       |
|All information barrier policy applications|Use `Get-InformationBarrierPoliciesApplicationStatus -All $true`<p>This will display information about whether policy application completed, failed, or is in progress.|

## Stop a policy application

If, after you have started applying information barrier policies, you want to stop those policies from being applied, use the following procedure. Keep in mind that it will take approximately 30-35 minutes for the process to begin.

1. To view the status of the most recent information barrier policy application, use the **Get-InformationBarrierPoliciesApplicationStatus** cmdlet.

    Syntax: `Get-InformationBarrierPoliciesApplicationStatus`

    Note the application's GUID.

2. Use the **Stop-InformationBarrierPoliciesApplication** cmdlet with an Identity parameter.

    Syntax:  `Stop-InformationBarrierPoliciesApplication -Identity GUID`

    Example: `InformationBarrierPoliciesApplication -Identity 46237888-12ca-42e3-a541-3fcb7b5231d1`

## Edit a segment or a policy

### Edit a segment

1. To view all existing segments, use the **Get-OrganizationSegment** cmdlet.
    
    Syntax: `Get-OrganizationSegment`

    You will see a list of segments and details for each, such as segment type, its UserGroupFilter value, who created or last modified it, GUID, and so on.

    > [!TIP]
    > Print or save your list of segments for reference later. For example, if you want to edit a segment, you will need to know its name or identify value (this is used with the Identity parameter).

2. To edit a segment, use the **Set-OrganizationSegment** cmdlet with the **Identity** parameter and relevant details. 

    Syntax: `Set-OrganizationSegment -Identity GUID -UserGroupFilter "attribute -eq 'attributevalue'"`

    Example: `Set-OrganizationSegment -Identity c96e0837-c232-4a8a-841e-ef45787d8fcd -UserGroupFilter "Department -eq 'HRDept'"`

    In this example, for the segment that has the GUID *c96e0837-c232-4a8a-841e-ef45787d8fcd*, we updated the department name to "HRDept".

When you have finished editing segments for your organization, you can proceed to [define](#part-2-define-information-barrier-policies) or [edit](#edit-a-policy) information barrier policies.

### Edit a policy

1. To view a list of current information barrier policies, use the **Get-InformationBarrierPolicy** cmdlet.

    Syntax: `Get-InformationBarrierPolicy`

    In the list of results, identify the policy that you want to change. Note the policy's GUID and name.

2. Use the **Set-InformationBarrierPolicy** cmdlet with an **Identity** parameter, and specify the changes you want to make.

    Syntax (blocking segments from communicating with other segments): 

    `Set-InformationBarrierPolicy -Identity GUID -SegmentsBlocked "segmentname, segmentname"` 

    Syntax (enabling segments to communicate only with certain other segments):
    
    ``Set-InformationBarrierPolicy -Identity GUID -SegmentsAllowed "segmentname, segmentname"``

    Example: Suppose a policy was defined to block Research from communicating with Sales and Marketing. The policy was defined by using this cmdlet: `New-InformationBarrierPolicy -Name "Research-SalesMarketing" -AssignedSegment "Research" -SegmentsBlocked "Sales, Marketing"`
    
    Suppose we want to change it so that people in Research can only communicate with people in HR. To make this change, we use this cmdlet: `Set-InformationBarrierPolicy -Identity 43c37853-ea10-4b90-a23d-ab8c93772471 -SegmentsAllowed "HR"`

3. When you are finished editing a policy, make sure to apply your changes. (See [Apply information barrier policies](#part-3-apply-information-barrier-policies).)

### Remove a policy

1. To view a list of current information barrier policies, use the **Get-InformationBarrierPolicy** cmdlet.

    Syntax: `Get-InformationBarrierPolicy`

    In the list of results, identify the policy that you want to remove. Note the policy's GUID and name. Make sure the policy is set to inactive status.

2. Use the **Remove-InformationBarrierPolicy** cmdlet with an Identity parameter.

    Syntax: `Remove-InformationBarrierPolicy -Identity GUID`

    Example: Suppose we want to remove a policy that has GUID *43c37853-ea10-4b90-a23d-ab8c93772471*. To do this, we use this cmdlet:
    
    `Remove-InformationBarrierPolicy -Identity 43c37853-ea10-4b90-a23d-ab8c93772471`

    When prompted, confirm the change.

3. Repeat steps 1-2 for each policy you want to remove.

4. When you are finished removing policies, apply your changes. To do this, use the **Start-InformationBarrierPoliciesApplication** cmdlet.

    Syntax: `Start-InformationBarrierPoliciesApplication`

    Changes are applied, user by user, for your organization. If your organization is large, it can take 24 hours (or more) for this process to complete.

### Set a policy to inactive status

1. To view a list of current information barrier policies, use the **Get-InformationBarrierPolicy** cmdlet.

    Syntax: `Get-InformationBarrierPolicy`

    In the list of results, identify the policy that you want to change (or remove). Note the policy's GUID and name.

2. To set the policy's status to inactive, use the **Set-InformationBarrierPolicy** cmdlet with an Identity parameter and the State parameter set to Inactive.

    Syntax: `Set-InformationBarrierPolicy -Identity GUID -State Inactive`

    `Set-InformationBarrierPolicy -Identity 43c37853-ea10-4b90-a23d-ab8c9377247 -State Inactive`

    In this example, we set an information barrier policy that has GUID *43c37853-ea10-4b90-a23d-ab8c9377247* to an inactive status.

3. To apply your changes, use the **Start-InformationBarrierPoliciesApplication** cmdlet.

    Syntax: `Start-InformationBarrierPoliciesApplication`

    Changes are applied, user by user, for your organization. If your organization is large, it can take 24 hours (or more) for this process to complete. (As a general guideline, it takes about an hour to process 5,000 user accounts.)

At this point, one or more information barrier policies are set to inactive status. From here, you can do any of the following:
- Leave it as is (a policy set to inactive status has no effect on users)
- [Edit a policy](#edit-a-policy) 
- [Remove a policy](#remove-a-policy)

## Example: Contoso's departments, segments, and policies

To see how an organization might approach defining segments and policies, consider the following example.

### Contoso's departments and plan

Contoso has five departments: HR, Sales, Marketing, Research, and Manufacturing. In order to remain compliant with industry regulations, people in some departments are not supposed to communicate with other departments, as listed in the following table:

|Segment  |Can talk to  |Cannot talk to  |
|---------|---------|---------|
|HR     |Everyone         |(no restrictions)         |
|Sales     |HR, Marketing, Manufacturing         |Research         |
|Marketing     |Everyone         |(no restrictions)         |
|Research     |HR, Marketing, Manufacturing        |Sales     |
|Manufacturing |HR, Marketing |Anyone other than HR or Marketing |

With this in mind, Contoso's plan includes three information barrier policies:

1. A policy designed to prevent Sales from communicating with Research (and another policy to prevent Research from communicating with Sales)
2. A policy designed to allow Manufacturing to communicate with HR and Marketing only 

It's not necessary to define policies for HR or Marketing.

### Contoso's defined segments

Contoso will use the Department attribute in Azure Active Directory to define segments, as follows:

|Department  |Segment Definition  |
|---------|---------|
|HR     | `New-OrganizationSegment -Name "HR" -UserGroupFilter "Department -eq 'HR'"`        |
|Sales     | `New-OrganizationSegment -Name "Sales" -UserGroupFilter "Department -eq 'Sales'"`        |
|Marketing     | `New-OrganizationSegment -Name "Marketing" -UserGroupFilter "Department -eq 'Marketing'"`        |
|Research     | `New-OrganizationSegment -Name "Research" -UserGroupFilter "Department -eq 'Research'"`        |
|Manufacturing     | `New-OrganizationSegment -Name "Manufacturing" -UserGroupFilter "Department -eq 'Manufacturing'"`        |

With the segments defined, Contoso proceeds to define policies. 

### Contoso's information barrier policies

Contoso defines three polices, as described in the following table:

|Policy  |Policy Definition  |
|---------|---------|
|Policy 1: Prevent Sales from communicating with Research     | `New-InformationBarrierPolicy -Name "Sales-Research" -AssignedSegment "Sales" -SegmentsBlocked "Research" -State Inactive` <p> In this example, the information barrier policy is called *Sales-Research*. When this policy is active and applied, it will help prevent users who are in the Sales segment from communicating with users in the Research segment. This is a one-way policy; it won't prevent Research from communicating with Sales. For that, Policy 2 is needed.      |
|Policy 2: Prevent Research from communicating with Sales     | `New-InformationBarrierPolicy -Name "Research-Sales" -AssignedSegment "Research" -SegmentsBlocked "Sales" -State Inactive` <p> In this example, the information barrier policy is called *Research-Sales*. When this policy is active and applied, it will help prevent users who are in the Research segment from communicating with users in the Sales segment.       |
|Policy 3: Allow Manufacturing to communicate with HR and Marketing only     | `New-InformationBarrierPolicy -Name "Manufacturing-HRMarketing" -AssignedSegment "Manufacturing" -SegmentsAllowed "HR, Marketing" -State Inactive` <p>In this case, the information barrier policy is called *Manufacturing-HRMarketing*. When this policy is active and applied, Manufacturing can communicate only with HR and Marketing. Note that HR and Marketing are not restricted from communicating with other segments. |

With segments and policies defined, Contoso applies the policies by running the **Start-InformationBarrierPoliciesApplication** cmdlet. 

When that finishes, Contoso is compliant with legal and industry requirements.

## Related articles

[Get an overview of information barriers](information-barriers.md)

[Learn more about information barriers in Microsoft Teams](https://docs.microsoft.com/MicrosoftTeams/information-barriers-in-teams)

[Attributes for information barrier policies (Preview)](information-barriers-attributes.md)

[Troubleshooting information barriers (Preview)](information-barriers-troubleshooting.md)
