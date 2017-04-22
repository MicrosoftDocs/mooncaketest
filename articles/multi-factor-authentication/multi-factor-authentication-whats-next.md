---
title: Configure Azure MFA | Microsoft Docs
description: This is the Azure Multi-factor authentication page that describes what to do next with MFA.  This includes reports, fraud alert, one-time bypass, custom voice messages, caching, trusted ips and app passwords.
services: multi-factor-authentication
documentationcenter: ''
author: kgremban
manager: femila
editor: yossib

ms.assetid: 75af734e-4b12-40de-aba4-b68d91064ae8
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/21/2017
ms.author: kgremban

---
# Configure Azure Multi-Factor Authentication settings
This article helps you manage Azure Multi-Factor Authentication now that you are up and running.  It covers various topics that help you to get the most out of Azure Multi-Factor Authentication.  Not all these features are available in every version of Azure Multi-Factor Authentication.

| Feature | Description | 
|:--- |:--- |
| [Selectable Verification Methods](#selectable-verification-methods) |Allows you to choose the authentication methods that are available for users to use. |

## Selectable Verification Methods
You can choose which verification methods are available for your users. The table below provides a brief overview of each method.

When your users enroll their accounts for MFA, they choose their preferred verification method out of the options that you enabled. The guidance for their enrollment process is covered in [Set up my account for two-step verification](multi-factor-authentication-end-user-first-time.md)

| Method | Description |
|:--- |:--- |
| Call to phone |Places an automated voice call. The user answers the call and presses # in the phone keypad to authenticate. This phone number is not synchronized to on-premises Active Directory. |
| Text message to phone |Sends a text message containing a verification code. The user is prompted to either reply to the text message with the verification code or to enter the verification code into the sign-in interface. |
| Notification through mobile app |Sends a push notification to your phone or registered device. The user views the notification and selects **Verify** to complete verification. <br>The Microsoft Authenticator app is available for [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072), and [IOS](http://go.microsoft.com/fwlink/?Linkid=825073). |
| Verification code from mobile app |The Microsoft Authenticator app generates a new OATH verification code every thirty seconds. The user enters this verification code into the sign-in interface.<br>The Microsoft Authenticator app is available for [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072), and [IOS](http://go.microsoft.com/fwlink/?Linkid=825073). |

### How to enable/disable authentication methods
1. Sign in to the [Azure Classic Management Portal](https://manage.windowsazure.cn/).
2. On the left, click Active Directory.
3. Under Active Directory, click on the directory you wish to enable or disable authentication methods.
4. On the Directory you have selected, click Configure.
5. In the multi-factor authentication section, click Manage service settings.
6. On the Service Settings page, under verification options, select/unselect the options you wish to use.</br></br>
   ![Verification options](./media/multi-factor-authentication-whats-next/authmethods.png)
7. Click **Save**.
8. Click **Close**.
