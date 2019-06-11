---
title: "Create an APNs Certificate for iOS devices"
ms.reviewer: 
ms.author: brendonb
author: brendonb
manager: laurawi
ms.date: 8/5/2016
audience: Admin
ms.topic: article
f1_keywords:
- 'O365M_APNCertMDM'
- 'O365E_APNCertMDM'
ms.service: O365-seccomp
localization_priority: Normal
search.appverid:
- MOE150
- MED150
- MBS150
- MET150
ms.assetid: 522b43f4-a2ff-46f6-962a-dd4f47e546a7
description: "To manage iOS devices like iPad and iPhones in Mobile Device Management for Office 365, follow these steps to first create an APNs certificate."
---

# Create an APNs Certificate for iOS devices

 To manage iOS devices like iPad and iPhones in Mobile Device Management for Office 365 you must create an APNs certificate. 
  
To do this, follow the steps from the **Set up** link on the portal page. (Go to **Security &amp; Compliance Center** \> **Security policies** \> **Device management** \> **Manage settings**.)
  
![Set up mobile device management required and recommended steps](media/d71e3c76-b6b9-4549-ade6-cbfab846d908.png)
  
1. Next to **Configure a APNs Certificate for iOS devices**, select **Set up**.
    
2. Select **Download your CSR file** and save the Certificate signing request to a somewhere on your computer that you'll remember. 
    
    ![Install APN Certificate dialog box](media/03aa8a24-e95c-4077-9b6b-ef76a86bafd7.png)
  
3. Select **Next**.
    
4. Create an APN certificate.
    
  - Select **Apple APNS Portal** to open the Apple Push Certificates Portal. 
    
    ![Install APN Notification cert dialog with Apple APNS Portal selected](media/ce19f53c-f44a-470b-baf3-9278dfda2ba5.png)
  
  - Sign in with an Apple ID.
    
    > [!IMPORTANT]
    > Use a company Apple ID associated with an email account that will remain with your organization even if the user who manages the account leaves. Save this ID because you'll need to use the same ID when it's time to renew the certificate. 
  
  - Select **Create a Certificate** and accept the **Terms of Use**.
    
  - **Browse** to the Certificate signing request you downloaded to your computer from Office 365 and select **Upload**.
    
  - **Download** the APN certificate created by the Apple Push Certificate Portal to your computer. 
    
    > [!TIP]
    > If you're having trouble downloading the certificate, refresh your browser. 
  
5. Go back to Office 365 and select **Next** to get to the **Upload APNS certificate** page. 
    
6. Browse to the APN certificate you downloaded from the Apple Push Certificates Portal.
    
    ![Click the browse button to select APNS cert you downloaded from Apple](media/afe2849d-af23-4c55-9009-d8f25edaf6c0.png)
  
7. Select **Finish**.
    
Go back to **Security &amp; Compliance Center** \> **Security policies** \> **Device management** \> **Manage settings** to complete setup. 
  

