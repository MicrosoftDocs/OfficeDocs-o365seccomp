---
title: "Attributes for information barrier policies"
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
description: "Use this article as a reference for various attributes you can use in information barrier policies."
---

# Attributes for information barrier policies (Preview)

Certain attributes in Azure Active Directory can be used to segment users. Segments are then used as filters for information barrier policies. For example, you might use **Department** to define segments of users by department within your organization (assuming no single employee works for two departments at the same time). 

This article provides a list of attributes that can be used. To learn more about information barriers, see the following resources:
- [Information barriers (Preview)](information-barriers.md)
- [Define policies for information barriers in Microsoft Teams (Preview)](information-barriers-policies.md)

## How to use attributes in information barrier policies

The attributes listed in this article can be used to define (or edit) segments of users. Segments are used as parameters (UserGroupFilter) in information barrier policies, as shown in the following examples:

|Example  |Cmdlet  |
|---------|---------|
|Define a segment called Segment1 using the Department attribute     | `New-OrganizationSegment -Name "Segment1" -UserGroupFilter "Department -eq 'Department1'"`        |
|Define a segment called SegmentA using the MemberOf attribute (suppose this attribute contains group names, such as "BlueGroup")     | `New-OrganizationSegment -Name "SegmentA" -UserGroupFilter "MemberOf -eq 'BlueGroup'"`        |
|Define a segment called DayTraders using ExtensionAttribute1 (suppose this attribute contains job titles, such as "DayTrader")|`New-OrganizationSegment -Name "DayTraders" -UserGroupFilter "ExtensionAttribute1 -eq 'DayTrader'"` |

When you define segments, use the same attribute for all your segments. For example, if you define some segments using *Department*, define all of the segments using *Department*. Don't define some segments using *Department* and others using *MemberOf*. Make sure your segments do not overlap; each user should be assigned to exactly one segment. 

To learn more, see [Define segments using PowerShell](information-barriers-policies.md#define-segments-using-powershell).

## Reference

The following table lists the attributes that you can use with information barriers.

|Azure Active Directory property name (LDAP display name)  |Exchange property name  |
|---------|---------|
|Co       | Co        |
|Company     |Company         |
|Department     |Department         |
|ExtensionAttribute1 |CustomAttribute1  |
|ExtensionAttribute2 |CustomAttribute2  |
|ExtensionAttribute3 |CustomAttribute3  |
|ExtensionAttribute4 |CustomAttribute4  |
|ExtensionAttribute5 |CustomAttribute5  |
|ExtensionAttribute6 |CustomAttribute6  |
|ExtensionAttribute7 |CustomAttribute7  |
|ExtensionAttribute8 |CustomAttribute8  |
|ExtensionAttribute9 |CustomAttribute9  |
|ExtensionAttribute10 |CustomAttribute10  |
|ExtensionAttribute11 |CustomAttribute11  |
|ExtensionAttribute12 |CustomAttribute12  |
|ExtensionAttribute13 |CustomAttribute13  |
|ExtensionAttribute14 |CustomAttribute14  |
|ExtensionAttribute15 |CustomAttribute15  |
|MSExchExtensionCustomAttribute1 |ExtensionCustomAttribute1 |
|MSExchExtensionCustomAttribute2 |ExtensionCustomAttribute2 |
|MSExchExtensionCustomAttribute3 |ExtensionCustomAttribute3 |
|MSExchExtensionCustomAttribute4 |ExtensionCustomAttribute4 |
|MSExchExtensionCustomAttribute5 |ExtensionCustomAttribute5 |
|MailNickname |Alias |
|PhysicalDeliveryOfficeName |Office |
|PostalCode |PostalCode |
|ProxyAddresses |EmailAddresses |
|StreetAddress |StreetAddress |
|TargetAddress |ExternalEmailAddress |
|UsageLocation |UsageLocation |
|UserPrincipalName	|UserPrincipalName	|
|Mail	|WindowsEmailAddress	|
|Description	|Description	|
|MemberOf	|MemberOfGroup	|

## Related topics

[Define policies for information barriers in Microsoft Teams (Preview)](information-barriers-policies.md)

[Troubleshooting information barriers (Preview)](information-barriers-troubleshooting.md)

[Information barriers (Preview)](information-barriers.md)



