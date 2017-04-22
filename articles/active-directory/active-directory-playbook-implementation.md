---
title: Azure Active Directory PoC Playbook Implementation | Microsoft Docs
description: Explore and quickly implement Identity and Access Management scenarios 
services: active-directory
keywords: azure active directory, playbook, Proof of Concept, PoC
documentationcenter: ''
author: dstefanMSFT
manager: asuthar

ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/12/2017
ms.author: dstefan

---
# Azure Active Directory Proof of Concept Playbook: Implementation

## Foundation - Syncing AD to Azure AD 

A hybrid identity is the foundation for most of the enterprise customers who already have an on-premises directory. The goal here is to intentionally spend as less time here as possible to show the value of the actual identity and access scenarios. 

| Scenario | Building Blocks| 
| --- | --- |  
| [Extending your on-premises identity to the cloud](#extending-your-on-premises-identity-to-the-cloud) | [Directory Synchronization - Password Hash Sync](active-directory-playbook-building-blocks.md#directory-synchronization---password-hash-sync-phs---new-installation) <br/>**Note**: If you already have DirSync/ADSync or earlier versions of Azure AD Connect, this step is optional. Some scenarios in this guide might require newer version of Azure AD Connect.

### Extending your on-premises identity to the cloud 

1. Bob is the Active Directory administrator at Contoso. He gets the requirement to enable identity as a service for a set of users. After execution of Azure AD Connect wizard, the identity of the target users available in the cloud. 
2. Bob asks Susie, one of the target users, to access the Azure Active Directory access panel and confirm that she can authenticate. Susie sees a branded login page and an empty access panel which is ready for enabling future application access.

## Theme - Lots of apps, one identity

| Scenario | Building Blocks| 
| --- | --- |  
| [SSO and Identity Lifecycle Events](#sso-and-identity-lifecycle-events) |  |
| [Synchronize LDAP identities to Azure AD](#synchronize-ldap-identities-to-azure-ad) |  [Generic LDAP Connector configuration](active-directory-playbook-building-blocks.md#generic-ldap-connector-configuration) |

### SSO and Identity Lifecycle Events

1. Susie takes a leave of absence, and by corporate policy the on-premises AD account is temporary disabled. Susie now can't log in to Azure AD and therefore can't access ServiceNow. 
2. Susie makes a lateral move from Marketing to Sales. Kevin removes her access from ServiceNow. Susie logs in the azure ad myapps and she no longer sees the ServiceNow Tile. After 10 minutes, Kevin confirms that Susie account was disabled from ServiceNow Management console.


### Synchronize LDAP identities to Azure AD

1. Bob's company has complex identity infrastructure. Most of the users are maintained inside Windows Server Active Directory Domain Services (ADDS). Some of them, are managed by HR system inside Active Directory Lightweight Directory Services (ADLDS).
2. Bob is tasked with enabling access to SaaS apps for all users (also these not present in ADDS).
3. Bob configures Generic LDAP Connector to pull data from ADLDS in Azure AD Connect.
4. Bob creates synchronization rules so LDAP users are populated into Metaverse and to Azure AD
5. Susie being LDAP user accesses her SaaS app using synchronized identity



> [!IMPORTANT] 
> This is an advanced configuration requiring some familiarity with FIM/MIM. If used in production, we advise questions about this configuration go through [Premier Support](https://support.microsoft.com/zh-cn/premier).



## Theme - Increase your security 

| Scenario | Building Blocks| 
| --- | --- |  
| [Secure administrator account access](#secure-administrator-account-access) | [Azure MFA with Phone Calls](active-directory-playbook-building-blocks.md#azure-multi-factor-authentication-with-phone-calls) |
| [Protect identities based on risk](#protect-identities-based-on-risk) | [Discovering risk events](active-directory-playbook-building-blocks.md#discovering-risk-events) <br/>[Deploying Sign-in risk policies](active-directory-playbook-building-blocks.md#deploying-sign-in-risk-policies) |
| [Authenticate without passwords using certificate based authentication](#authenticate-without-passwords-using-certificate-based-authentication) | [Configuring certificate based authentication](active-directory-playbook-building-blocks.md#configuring-certificate-based-authentication)

### Secure administrator account access

1. Bob is the Azure AD Global Administrator. He has identified Stuart as a co-administrator of the service. 
2. Bob configures Stuart's account to always require MFA to improve the security posture
3. Stuart logs in to the Azure  portal, and notices that he needs to register his phone number to continue the login
4. Subsequent logins from Stuart are now protected with Multi-Factor Authentication, and he now gets a phone call to verify his identity.

### Authenticate without passwords using certificate based authentication

1. Bob is Global Administrator for financial institution, that forbids use of passwords as an authentication factor for their applications.
2. Bob enables and enforces certificate authentication on ADFS and Azure AD
3. Susie while accessing application is prompted to authenticate using certificate

[!INCLUDE [active-directory-playbook-toc](../../includes/active-directory-playbook-steps.md)]

