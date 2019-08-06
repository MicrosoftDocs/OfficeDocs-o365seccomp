---
title: "How Office 365 ATP Safe Links works"
ms.author: deniseb
author: denisebmsft
manager: dansimp
audience: Admin
ms.date: 05/19/2019
ms.topic: overview
ms.service: O365-seccomp
localization_priority: Normal
ms.collection: 
- Strat_O365_IP
- M365-security-compliance
description: "The Safe Links feature provides time-of-click verification of hyperlinks in Office documents and in email messages. Read this article to learn how ATP Safe Links works."
---

# How Office 365 ATP Safe Links works
         
## How ATP Safe Links works with URLs in email

At a high level, here's how [ATP Safe Links](atp-safe-links.md) protection works for URLs in email (hosted in Office 365, not on-premises):
  
1. People receive email messages, some of which contain URLs.
    
2. All email goes through Exchange Online Protection, where internet protocol (IP) and envelope filters, signature-based malware protection, anti-spam and anti-malware filters are applied. 
    
3. Email arrives in people's inboxes.
    
4. A user signs in to Office 365, and goes to their email inbox.
    
5. The user opens an email message, and clicks on a URL in the email message.
    
6. The ATP Safe Links feature immediately checks the URL before opening the website. The URL is identified as blocked, malicious, or safe.
    
    - If the URL is to a website that is included in a [custom "Do not rewrite" URLs list](set-up-a-custom-do-not-rewrite-urls-list-with-atp.md) for a policy that applies to the user, the website opens. 
    
    - If the URL is to a website that is included in the organization's [custom blocked URLs list](set-up-a-custom-blocked-urls-list-wtih-atp.md), a [warning page](atp-safe-links-warning-pages.md) opens. 
    
    - If the URL is to a website that has been determined to be malicious, a [warning page](atp-safe-links-warning-pages.md) opens. 
    
    - If the URL goes to a downloadable file and your organization's [ATP Safe Links policies](set-up-atp-safe-links-policies.md) are configured to scan such content, the downloadable file is checked. 
    
    - If the URL is determined to be safe, the website opens.
    
## How ATP Safe Links works with URLs in Office documents

At a high level, here's how [ATP Safe Links](atp-safe-links.md) protection works for URLs in Office 365 ProPlus applications (current versions of Word, Excel, and PowerPoint on Windows or Mac, Office apps on iOS or Android devices, Visio on Windows, OneNote in a browser, and Office in a browser):
  
1. People have installed Office 365 ProPlus on their computer, smartphone, or tablet. (Or, they are using Office in their browser.)
    
2. A user opens a Word, Excel, PowerPoint, or Visio, and signs in to Office 365 Enterprise using their work or school account. The document contains URLs.
    
3. When the user clicks on a URL in the document, the link is checked by the ATP Safe Links service.
    
      - If the URL is to a website that is included in a [custom "Do not rewrite" URLs list](set-up-a-custom-do-not-rewrite-urls-list-with-atp.md) for a policy that applies to the user, that user is taken to the website. 
    
      - If the URL is to a website that is included in the organization's [custom blocked URLs list](set-up-a-custom-blocked-urls-list-wtih-atp.md), the user is taken to a [warning page](atp-safe-links-warning-pages.md).
    
      - If the URL is to a website that has been determined to be malicious, the user is taken to a [warning page](atp-safe-links-warning-pages.md).
    
      - If the URL goes to a downloadable file and the [ATP Safe Links policies](set-up-atp-safe-links-policies.md) are configured to scan such downloads, the downloadable file is checked. 
    
      - If the URL is considered safe, the user is taken to the website.

