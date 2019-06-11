---
title: "Troubleshooting information barriers"
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
description: "Use this article as a guide for troubleshooting information barriers."
---

# Troubleshooting information barriers (Preview)

Information barriers can help your organization remain compliant with legal requirements and industry regulations. For example, with information barriers, you can restrict communication between specific groups of users to avoid a conflict of interest or other issues. To learn more, see [Information barriers (Preview)](information-barriers.md).

This article provides guidance you can use to get answers to questions or resolve issues that may arise with information barriers.  

## Before you begin...

To perform the tasks described in this article, you must be assigned an appropriate role, such as one of the following:
- Microsoft 365 Enterprise Global Administrator
- Office 365 Global Administrator
- Compliance Administrator
- IB Compliance Management (this is a new role!)

To learn more about roles and permissions, see [Permissions in the Office 365 Security & Compliance Center](permissions-in-the-security-and-compliance-center.md).

To learn more about prerequisites for information barriers, see [Prerequisites (for information barrier policies)](information-barriers-policies.md#prerequisites).

Also, make sure to [connect to Office 365 Security & Compliance Center PowerShell](https://docs.microsoft.com/powershell/exchange/office-365-scc/connect-to-scc-powershell/connect-to-scc-powershell?view=exchange-ps).

## Issue: People are unexpectedly blocked from communicating in Microsoft Teams 

In this case, people are reporting unexpected issues communicating in Microsoft Teams. Examples:
- A user is unable to find or communicate with another user in Microsoft Teams.
- A user cannot see or select another user in Microsoft Teams.
- A user can see, but cannot send messages to, another user in Microsoft Teams.

### What to do

1. Determine whether the users are affected by an information barrier policy. To do this, use the **Get-InformationBarrierRecipientStatus** cmdlet with the Identity parameter. 

    The syntax is `Get-InformationBarrierRecipientStatus -Identity`

    You can use any identity value that uniquely identifies each recipient, such as Name, Alias, Distinguished name (DN), Canonical DN, Email address, or GUID.

    Example: `Get-InformationBarrierRecipientStatus -Identity meganb`

    In this example, we are using an alias (*meganb*) for the Identity parameter. This cmdlet will return information that indicates whether the user is affected by an information barrier policy. (Look for *ExoPolicyId: \<GUID>.)

    If the users are not included in information barrier policies, contact support. Otherwise, proceed to the next step.

2. Find out which segments are included in an information barrier policy. To do this, use the `Get-InformationBarrierPolicy` cmdlet with the Identity parameter. Use details, such as the policy GUID (ExoPolicyId) you received during the previous step, as an identity value.

    Example: `Get-InformationBarrierPolicy -Identity b42c3d0f-49e9-4506-a0a5-bf2853b5df6f`

    In this example, we are getting detailed information about the information barrier policy that has ExoPolicyId *b42c3d0f-49e9-4506-a0a5-bf2853b5df6f*.
    
    After you run the cmdlet, in the results, look for **AssignedSegment**, **SegmentsAllowed**, and **SegmentsBlocked** values.

    Example: After running the `Get-InformationBarrierPolicy` cmdlet, we saw the following in our list of results:

    ```powershell
        AssignedSegment      : Sales
        SegmentsAllowed      : {}
        SegmentsBlocked      : {Research}
    ```
    In this case, we can see that an information barrier policy affects people who are in the Sales and Research segments. In this case, people in Sales are prevented from communicating with people in Research. If this seems correct, then information barriers are working as expected. If not, proceed to the next step.

4. Make sure your segments are defined correctly. To do this, use the `Get-OrganizationSegment` cmdlet, and review the list of results. 

    To view details for a specific segment, use the `Get-OrganizationSegment` cmdlet with an Identity parameter. 

    Example: `Get-OrganizationSegment -Identity c96e0837-c232-4a8a-841e-ef45787d8fcd`

    In this example, we are getting information about the segment that has GUID *c96e0837-c232-4a8a-841e-ef45787d8fcd*.

    Review the details for the segment. If necessary, [edit a segment](information-barriers-policies.md#edit-a-segment), and then re-use the `Start-InformationBarrierPoliciesApplication` cmdlet.

    If you are still having issues with your information barrier policy, contact support.
    
## Issue: The information barrier application process is taking too long

After running the **Start-InformationBarrierPoliciesApplication** cmdlet, the process is taking a really long time to finish.

### What to do

1. Keep in mind that when you run the policy application cmdlet, information barrier policies are being applied (or removed), user by user, for all accounts in your organization. If you have a lot of users, it will take a while to process. (As a general guideline, it takes about an hour to process 5,000 user accounts.) 

2. Use the **Get-InformationBarrierPoliciesApplicationStatus** cmdlet to verify status.

    Syntax: `Get-InformationBarrierPoliciesApplicationStatus`

    To display status for all information barrier policy applications, use `Get-InformationBarrierPoliciesApplicationStatus -All $true`

    This will display information about whether policy application completed, failed, or is in progress..

3. Depending on the results of step 2, take one of the following steps:

    - If the application has not started, and it has been more than 45 minutes since the **Start-InformationBarrierPoliciesApplication** cmdlet has been run, review your audit log to see if there are any errors in policy definitions, or some other reason why the application has not started.

    - If the application has failed, review your segments and policies. If necessary, [edit segments](information-barriers-policies.md#edit-a-segment) and/or [edit policies](information-barriers-policies.md#edit-a-policy), and then run the **Start-InformationBarrierPoliciesApplication** cmdlet again.

    - If the application is still in progress, allow more time for it to complete. If it has been several days, contact support.

## Related topics

[Define policies for information barriers in Microsoft Teams (Preview)](information-barriers-policies.md)

[Information barriers (Preview)](information-barriers.md)



