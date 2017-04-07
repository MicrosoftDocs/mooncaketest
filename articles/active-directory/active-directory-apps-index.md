---
title: Article Index for Application Management in Azure Active Directory | Azure
description: Learn how to customize the expiration date for your federation certificates, and how to renew certificates that will soon expire.
services: active-directory
documentationcenter: ''
author: MarkusVi
manager: femila

ms.assetid: 5321b8e4-2afa-4dfe-8d53-4add7abb5ec8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
wacn.date: ''
ms.author: markvi
---

# Article Index for Application Management in Azure Active Directory
This page provides a comprehensive list of every document written about the various application-related features in Azure Active Directory (Azure AD).

There is a brief introduction to each major feature area, as well as guidance on which articles to read depending on what information you're looking for.

## Overview Articles
The articles below are good starting points for those who simply want a brief explanation of Azure AD application management features.

| Article Guide |  |
|:---:| --- |
| An introduction to the application management problems that Azure AD solves |[Managing Applications with Azure Active Directory (AD)](./active-directory-enable-sso-scenario.md) |
| An overview of the various features in Azure AD related to enabling single sign-on, defining who has access to apps, and how users launch apps |[Application Access and Single Sign-on in Azure Active Directory](./active-directory-appssoaccess-whatis.md) |
| A look at the different steps involved when integrating apps into your Azure AD |[Integrating Azure Active Directory with Applications](./active-directory-integrating-applications-getting-started.md)<br /><br />[Enabling Single Sign-On to SaaS Apps](./active-directory-sso-integrate-saas-apps.md)<br /><br />[Managing Access to Apps](./active-directory-managing-access-to-apps.md) |
| A technical explanation of how apps are represented in Azure AD |[How and Why Applications are Added to Azure AD](./active-directory-how-applications-are-added.md) |

## Troubleshooting Articles
This section provides quick access to relevant troubleshooting guides. More information about each feature area can be found on the rest of this page.

| Feature Area |  |
|:---:| --- |
| Federated Single Sign-On |[Troubleshooting SAML-Based Single Sign-On](./active-directory-saml-debugging.md) |
| Password-Based Single Sign-On | Troubleshooting the Access Panel Extension for Internet Explorer |
| Single sign-on between on-prem AD and Azure AD |[Troubleshooting Password Synchronization](./active-directory-aadconnectsync-implement-password-synchronization.md#troubleshooting-password-synchronization)<br /><br />[Troubleshooting Password Writeback](./active-directory-passwords-troubleshoot.md#troubleshoot-password-writeback) |

## Single Sign-On (SSO)
### Federated Single Sign-On: Sign into many apps using one identity
Single sign-on allows users to access a variety of apps and services using only one set of credentials. Federation is one method through which you can enable single sign-on. When users attempt to sign into federated apps, they will get redirected to their organization's official sign-in page rendered by Azure Active Directory, and are then redirected back to the app upon successful authentication.

| Article Guide |  |
|:---:| --- |
| An introduction to federation and other types of sign-on |[Single Sign-On with Azure AD](./active-directory-appssoaccess-whatis.md) |
| Thousands of SaaS apps that are pre-integrated with Azure AD with simplified single sign-on configuration steps |[Getting started with the Azure AD application gallery](./active-directory-appssoaccess-whatis.md#get-started-with-the-azure-ad-application-gallery)<br /><br />[Full List of Pre-Integrated Apps that Support Federation](http://aka.ms/aadfederatedapps)<br /><br />[How to Add Your App to the Azure AD App Gallery](./active-directory-app-gallery-listing.md) |
| More than 150 app tutorials on how to configure single sign-on for apps, and many more |  |
| How to manually set up and customize your single sign-on configuration |How to Configure Federated Single Sign-On to Apps that are not in the Azure Active Directory Application Gallery <br /><br />[How to Customize Claims Issued in the SAML Token for Pre-Integrated Apps](./active-directory-saml-claims-customization.md) |
| Troubleshooting guide for federated apps that use the SAML protocol |[Troubleshooting SAML-Based Single Sign-On](./active-directory-saml-debugging.md) |
| How to configure your app's certificate's expiration date, and how to renew your certificates |[Managing Certificates for Federated Single Sign-On in Azure Active Directory](./active-directory-sso-certs.md) |

Federated single sign-on is available for all editions of Azure AD for up to ten apps per user. [Azure AD Premium](https://www.azure.cn/pricing/details/identity/) supports unlimited applications. If your organization has [Azure AD Basic](https://www.azure.cn/pricing/details/identity/) or [Azure AD Premium](https://www.azure.cn/pricing/details/identity/), then you can [use groups to assign access to federated applications](#managing-access-to-applications).

### Password-Based Single Sign-On: Account sharing and SSO for non-federated apps
To enable single sign-on to applications that don't support federation, Azure AD offers password management features that can securely store passwords to SaaS apps and automatically sign users into those apps. You can easily distribute credentials for newly created accounts and share team accounts with multiple people. Users don't necessarily need to know the credentials to the accounts that they're given access to.

| Article Guide |  |
|:---:| --- |
| An introduction to how password-based SSO works and a brief technical overview |[Password-Based Single Sign-On with Azure AD](./active-directory-appssoaccess-whatis.md#password-based-single-sign-on) |
| A summary of the scenarios related to account sharing and how these problems are solved by Azure AD |[Sharing accounts with Azure AD](./active-directory-sharing-accounts.md) |
| Automatically change the password for certain apps at a regular interval |[Automated Password Rollover (preview)](https://blogs.technet.microsoft.com/enterprisemobility/2015/02/20/azure-ad-automated-password-roll-over-for-facebook-twitter-and-linkedin-now-in-preview/) |
| Deployment and troubleshooting guides for the Internet Explorer version of the Azure AD password management extension |How to Deploy the Access Panel Extension for Internet Explorer using Group Policy <br /><br /> Troubleshooting the Access Panel Extension for Internet Explorer  |

Password-based single sign-on is available for all editions of Azure AD for up to ten apps per user. [Azure AD Premium](https://www.azure.cn/pricing/details/identity/) supports unlimited applications. If your organization has [Azure AD Basic](https://www.azure.cn/pricing/details/identity/) or [Azure AD Premium](https://www.azure.cn/pricing/details/identity/), then you can [use groups to assign access to applications](#managing-access-to-applications). Automated password rollover is an [Azure AD Premium](https://www.azure.cn/pricing/details/identity/) feature.

### Enabling single sign-on between Azure AD and on-premises AD
If your organization maintains a Windows Server Active Directory on premises along with your Azure Active Directory in the cloud, then you will likely want to enable single sign-on between these two systems. Azure AD Connect (the tool that integrates these two systems together) provides multiple options for setting up single sign-on: establish federation with ADFS or another federation provider, or enable password synchronization.

| Article Guide |  |
|:---:| --- |
| An overview on the single sign-on options offered in Azure AD Connect, as well as information on managing hybrid environments |[User Sign On Options in Azure AD Connect](./active-directory-aadconnect-user-signin.md) |
| General guidance for managing environments with both on-premises Active Directory and Azure Active Directory | [Integrating your On-Premises Identities with Azure Active Directory](./active-directory-aadconnect.md) |
| Guidance on using Password Sync to enable SSO |[Implement Password Synchronization with Azure AD Connect](./active-directory-aadconnectsync-implement-password-synchronization.md)<br /><br />[Troubleshoot Password Synchronization](https://support.microsoft.com/zh-cn/kb/2855271) |
| Guidance on using Password Writeback to enable SSO |[Getting Started with Password Management in Azure AD](./active-directory-passwords-getting-started.md)<br /><br />[Troubleshoot Password Writeback](./active-directory-passwords-troubleshoot.md#troubleshoot-password-writeback) |
| Guidance on using third party identity providers to enable SSO |[List of Compatible Third-Party Identity Providers That Can Be Used to Enable Single Sign-On](https://aka.ms/ssoproviders) |

Azure AD Connect is available for [all editions of Azure Active Directory](https://www.azure.cn/pricing/details/identity/). Azure AD Self-Service Password Reset is available for [Azure AD Basic](https://www.azure.cn/pricing/details/identity/) and [Azure AD Premium](https://www.azure.cn/pricing/details/identity/). Password Writeback to on-prem AD is an [Azure AD Premium](https://www.azure.cn/pricing/details/identity/) feature.

## Apps & Azure AD

### Automatically provision and deprovision user accounts in SaaS apps
Automate the creation, maintenance, and removal of user identities in SaaS applications such as Dropbox, Salesforce, ServiceNow, and more. Match and sync existing identities between Azure AD and your SaaS apps, and control access by automatically disabling accounts when users leave the organization.

| Article Guide |  |
|:---:| --- |
| Learn about how it works and find answers to common questions | |
| Configure how information is mapped between Azure AD and your SaaS app | Customizing Attribute Mappings <br><br> Writing Expressions for Attribute Mappings |
| How to enable automated provisioning to any app that supports the SCIM protocol |[Set up Automated User Provisioning to any SCIM-Enabled App](./active-directory-scim-provisioning.md) |
| Get notified of provisioning failures | Provisioning Notifications |
| Limit who gets provisioned to an application based on their attribute values | coping Filters  |

Automated user provisioning is available for all editions of Azure AD for up to ten apps per user. [Azure AD Premium](https://www.azure.cn/pricing/details/identity/) supports unlimited applications. If your organization has [Azure AD Basic](https://www.azure.cn/pricing/details/identity/) or [Azure AD Premium](https://www.azure.cn/pricing/details/identity/), then you can [use groups to manage which users get provisioned](#managing-access-to-applications).

### Building applications that integrate with Azure AD
If your organization is developing or maintaining line-of-business (LoB) applications, or if you're an app developer with customers who use Azure Active Directory, the following tutorials will help you integrate your applications with Azure AD.

| Article Guide |  |
|:---:| --- |
| Guidance for both IT professionals and application developers on integrating apps with Azure AD |[The IT Pro's Guide for Developing Applications for Azure AD](./active-directory-applications-guiding-developers-for-lob-applications.md)<br /><br />[The Developer's Guide for Azure Active Directory](./active-directory-developers-guide.md) |
| How to application vendors can add their apps to the Azure AD App Gallery |[Listing your Application in the Azure Active Directory Application Gallery](./active-directory-app-gallery-listing.md) |
| How to manage access to developed applications using Azure Active Directory |[How to Enable User Assignment for Developed Applications](./active-directory-applications-guiding-developers-requiring-user-assignment.md)<br /><br />[Assigning Users to your App](./active-directory-applications-guiding-developers-assigning-users.md)<br /> |

## Managing Access to Applications

### Access Panel: A portal for accessing apps and self-service features
The Azure AD Access Panel is where end-users can launch their apps and access the self-service features that allow them to manage their apps and group memberships. In addition to the Access Panel, other options for accessing SSO-enabled apps are included in the list below.

| Article Guide |  |
|:---:| --- |
| A comparison of the different options available for deploying single sign-on apps to users |[Deploying Azure AD Integrated Applications to Users](./active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users) |
| An overview of the Access Panel and its mobile equivalent MyApps | Introduction to Access Panel and MyApps <br />— [iOS](https://itunes.apple.com/us/app/my-apps-azure-active-directory/id824048653?mt=8)<br />— [Android](https://play.google.com/store/apps/details?id=com.microsoft.myapps) |
| How to access Azure AD apps from the Office 365 website |[Using the Office 365 App Launcher](https://support.office.com/en-us/article/Meet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a) |
| How to access Azure AD apps from the Intune Managed Browser mobile app |[Intune Managed Browser](https://technet.microsoft.com/en-us/library/dn878029.aspx)<br />— [iOS](https://itunes.apple.com/us/app/microsoft-intune-managed-browser/id943264951?mt=8)<br />— [Android](https://play.google.com/store/apps/details?id=com.microsoft.intune.mam.managedbrowser) |
| How to access Azure AD apps using deep links to initiate single sign-on |[Getting Direct Sign-On Links to Your Apps](./active-directory-appssoaccess-whatis.md#direct-sign-on-links-for-federated-password-based-or-existing-apps) |

Access Panel is available for [all editions of Azure Active Directory](https://www.azure.cn/pricing/details/identity/).

##See also

[What is Azure Active Directory?](./active-directory-whatis.md)

[Azure Multi-Factor Authentication](https://www.azure.cn/home/features/multi-factor-authentication/)