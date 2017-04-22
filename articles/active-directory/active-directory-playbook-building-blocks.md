---
title: Azure Active Directory PoC Playbook Building Blocks| Microsoft Docs
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
# Azure Active Directory Proof of Concept Playbook: Building Blocks

## Catalog of Actors

| Actor | Description | PoC Responsibility |
| --- | --- | --- |
| **Identity Architecture / development team** | This team is usually the one that designs the solution, implements prototypes, drives approvals, and finally hands off to operations | They provide the environments and are the ones evaluating the different scenarios from the manageability perspective |
| **On-Premises Identity Operations team** | Manages the different identity sources on-premises: Active Directory Forests, LDAP directories, HR systems, and Federation Identity Providers. | Provide access to on-premises resources needed for the PoC scenarios.<br/>They should be involved as little as possible|
| **Application Technical Owners** | Technical owners of the different cloud apps and services that will integrate with Azure AD | Provide details on SaaS applications (potentially instances for testing) |
| **Azure AD Global Admin** | Manages the Azure AD configuration | Provide credentials to configure the synchronization service. Usually the same team as Identity Architecture during PoC but separate during the operations phase|
| **Database team** | Owners of the Database infrastructure | Provide access to SQL environment (ADFS or Azure AD Connect) for specific scenario preparations.<br/>They should be involved as little as possible |
| **Network team** | Owners of the Network infrastructure | Provide required access at the network level for the synchronization servers to properly access the data sources and cloud services (firewall rules, ports opened, IPSec rules etc.) |
| **Security team** | Defines the security strategy, analyzes security reports from various sources, and follows through on findings. | Provide target security evaluation scenarios |

## Common Prerequisites for all building blocks

| Pre-requisite | Resources |
| --- | --- |
| Azure AD tenant defined with a valid Azure subscription | [How to get an Azure Active Directory tenant](active-directory-howto-tenant.md)<br/>**Note:** If you already have an environment with Azure AD Premium licenses, you can get a zero cap subscription by navigating to https://aka.ms/accessaad <br/>Learn more at: https://blogs.technet.microsoft.com/enterprisemobility/2016/02/26/azure-ad-mailbag-azure-subscriptions-and-azure-ad-2/ and https://technet.microsoft.com/library/dn832618.aspx |
| Azure AD Global Admin credentials | Assigning administrator roles in Azure Active Directory |
| Optional but strongly recommended: Parallel lab environment as a fallback | [Prerequisites for Azure AD Connect](./connect/active-directory-aadconnect-prerequisites.md) |

## Directory Synchronization - Password Hash Sync (PHS) - New Installation

Approximate time to Complete: one hour for less than 1,000 PoC users

### Pre-requisites

| Pre-requisite | Resources |
| --- | --- |
| Server to Run Azure AD Connect | [Prerequisites for Azure AD Connect](./connect/active-directory-aadconnect-prerequisites.md) |
| Target POC users, in the same domain and part of a security group, and OU | [Custom installation of Azure AD Connect](./connect/active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering) |
| Azure AD Connect Features needed for the POC are identified | [Connect Active Directory with Azure Active Directory - Configure sync features](./connect/active-directory-aadconnect.md#configure-sync-features) |
| You have needed credentials for on-premises and cloud environments  | [Azure AD Connect: Accounts and permissions](./connect/active-directory-aadconnect-accounts-permissions.md) |

### Steps

| Step | Resources |
| --- | --- |
| Download the latest version of Azure AD Connect | [Download Azure Active Directory Connect](https://www.microsoft.com/download/details.aspx?id=47594) |
| Install Azure AD Connect with the simplest path: Express <br/>1. Filter to the target OU to minimize the Sync Cycle time<br/>2. Choose target set of users in the on-premises group.<br/>3. Deploy the features needed by the other POC Themes | [Azure AD Connect: Custom installation: Domain and OU filtering](./connect/active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering) <br/>[Azure AD Connect: Custom installation: Group based filtering](./connect/active-directory-aadconnect-get-started-custom.md#sync-filtering-based-on-groups)<br/>[Azure AD Connect: Integrating your on-premises identities with Azure Active Directory: Configure Sync Features](./connect/active-directory-aadconnect.md#configure-sync-features) |
| Open the Azure AD Connect UI and see the running profiles completed (Import, sync, and export) | [Azure AD Connect sync: Scheduler](./connect/active-directory-aadconnectsync-feature-scheduler.md) |
| Open the Azure AD management portal, go to the "All Users" blade, add "Source of authority" column and see that the users appear, marked properly as coming from "Windows Server AD" | [Azure AD management portal](https://portal.azure.cn/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) |

### Considerations

1. Look at  the security considerations of password hash sync [here](./connect/active-directory-aadconnectsync-implement-password-synchronization.md).  If password hash sync for pilot production users is definitively not an option, then consider the following alternatives:
   - Create test users in the production domain. Make sure you don't synchronize any other account
   - Move to an UAT environment
2.	If you want to pursue federation, it is worthwhile to understand the costs associated a federated solution with on-premises Identity Provider beyond the POC and measure that against the benefits you are looking for:
    - It is in the critical path so you have to design for high availability
    - It is an on-premises service you need to capacity plan
    - It is an on-premises service you need to monitor/maintain/patch

Learn more: [Understanding Office 365 identity and Azure Active Directory - Federated Identity](https://support.office.com/article/Understanding-Office-365-identity-and-Azure-Active-Directory-06a189e7-5ec6-4af2-94bf-a22ea225a7a9#bk_federated)

## Generic LDAP Connector configuration

Approximate time to Complete: 60 minutes

> [!IMPORTANT]
> This is an advanced configuration requiring some familiarity with FIM/MIM. If used in production, we advise questions about this configuration go through [Premier Support](https://support.microsoft.com/zh-cn/premier).

### Pre-requisites

| Pre-requisite | Resources |
| --- | --- |
| Azure AD Connect installed and configured | Building block: [Directory Synchronization - Password Hash Sync](#directory-synchronization--password-hash-sync-phs--new-installation) |
| ADLDS instance meeting requirements | [Generic LDAP Connector technical reference: Overview of the Generic LDAP Connector](./connect/active-directory-aadconnectsync-connector-genericldap.md#overview-of-the-generic-ldap-connector) |
| List of workloads, that users are using and attributes associated with these workloads | [Azure AD Connect sync: Attributes synchronized to Azure Active Directory](./connect/active-directory-aadconnectsync-attributes-synchronized.md) |


### Steps

| Step | Resources |
| --- | --- |
| Add Generic LDAP Connector | [Generic LDAP Connector technical reference: Create a new Connector](./connect/active-directory-aadconnectsync-connector-genericldap.md#create-a-new-connector) |
| Create run profiles for created connector (full import, delta import, full synchronization, delta synchronization, export) | [Create a Management Agent Run Profile](https://technet.microsoft.com/library/jj590219(v=ws.10).aspx)<br/> [Using connectors with the Azure AD Connect Sync Service Manager](./connect/active-directory-aadconnectsync-service-manager-ui-connectors.md)|
| Run full import profile and verify, that there are objects in connector space | [Search for a Connector Space Object](https://technet.microsoft.com/library/jj590287(v=ws.10).aspx)<br/>[Using connectors with the Azure AD Connect Sync Service Manager: Search Connector Space](./connect/active-directory-aadconnectsync-service-manager-ui-connectors.md#search-connector-space) |
| Create synchronization rules, so that objects in Metaverse have necessary attributes for workloads | [Azure AD Connect sync: Best practices for changing the default configuration: Changes to Synchronization Rules](/connect/active-directory-aadconnectsync-best-practices-changing-default-configuration.md#changes-to-synchronization-rules/)<br/>[Azure AD Connect sync: Understanding Declarative Provisioning](./connect/active-directory-aadconnectsync-understanding-declarative-provisioning.md)<br/>[Azure AD Connect sync: Understanding Declarative Provisioning Expressions](./connect/active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md) |
| Start full synchronization cycle | [Azure AD Connect sync: Scheduler: Start the scheduler](./connect/active-directory-aadconnectsync-feature-scheduler.md#start-the-scheduler) |
| In case of issues do troubleshooting | [Troubleshoot an object that is not synchronizing to Azure AD](./connect/active-directory-aadconnectsync-troubleshoot-object-not-syncing.md) |
| Verify, that LDAP user can sign-in and access the application | https://login.partner.microsoftonline.cn |

### Considerations

> [!IMPORTANT]
> This is an advanced configuration requiring some familiarity with FIM/MIM. If used in production, we advise questions about this configuration go through [Premier Support](https://support.microsoft.com/zh-cn/premier).

## Azure Multi-Factor Authentication with Phone Calls

Approximate time to Complete: 10 minutes

### Pre-requisites

| Pre-requisite | Resources |
| --- | --- |
| Identify POC users that will use MFA  |  |
| Phone with good reception for MFA challenge  | [What is Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md) |

### Steps

| Step | Resources |
| --- | --- |
| Navigate to "Users and groups" blade in Azure AD Management Portal | [Azure AD Management Portal: Users and groups](https://portal.azure.cn/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/Overview/menuId/) |
| Choose "All users" blade |  |
| In the top bar choose "Multi-Factor Authentication" button | Direct URL for Azure MFA portal: https://aka.ms/mfaportal |
| In the "User" settings select the PoC users and enable them for MFA | [User States in Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication-get-started-user-states.md) |
| Login as the PoC user, and walk through the proof-up process  |  |

### Considerations

1. The PoC steps in this building block explicitly setting MFA for a user on all logins. There are other tools such as Conditional Access, and Identity Protection that engage MFA on more targeted scenarios. This will be something to consider when moving from POC to production.
2. The PoC steps in this building block are explicitly using Phone Calls as the MFA method for expedience. As you transition from POC to production, we recommend using applications such as the [Microsoft Authenticator](../multi-factor-authentication/end-user/microsoft-authenticator-app-how-to.md) as your second factor whenever possible.
Learn more: [DRAFT NIST Special Publication 800-63B](https://pages.nist.gov/800-63-3/sp800-63b.html)

## Configuring certificate based authentication

Approximate time to complete: 20 minutes

### Pre-requisites

| Pre-requisite | Resources |
| --- | --- |
| Device with user certificate provisioned (Windows, iOS or Android) from Enterprise PKI | [Deploy User Certificates](https://msdn.microsoft.com/library/cc770857.aspx) |
| Azure AD domain federated with ADFS | [Azure AD Connect and federation](./connect/active-directory-aadconnectfed-whatis.md)<br/>[Active Directory Certificate Services Overview](https://technet.microsoft.com/library/hh831740.aspx)|
| For iOS devices have Microsoft Authenticator app installed | [Get started with the Microsoft Authenticator app](../multi-factor-authentication/end-user/microsoft-authenticator-app-how-to.md) |

### Steps

| Step | Resources |
| --- | --- |
| Enable "Certificate Authentication" on ADFS | [Configure Authentication Policies: To configure primary authentication globally in Windows Server 2012 R2](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configure-authentication-policies#to-configure-primary-authentication-globally-in-windows-server-2012-r2) |
| Optional: Enable Certificate Authentication in Azure AD for Exchange Active Sync clients | [Get started with certificate-based authentication in Azure Active Directory](active-directory-certificate-based-authentication-get-started.md) |
| Navigate to Access Panel and authenticate using User Certificate | https://login.partner.microsoftonline.cn |

### Considerations

To learn more about caveats of this deployment visit: [ADFS: Certificate Authentication with Azure AD & Office 365](https://blogs.msdn.microsoft.com/samueld/2016/07/19/adfs-certauth-aad-o365/)

> [!NOTE]
> Possession of user certificate should be guarded. Either by managing devices or with PIN in case of smart cards.



[!INCLUDE [active-directory-playbook-toc](../../includes/active-directory-playbook-steps.md)]

