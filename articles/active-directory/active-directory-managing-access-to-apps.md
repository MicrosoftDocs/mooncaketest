---
title: Managing access to apps using Azure AD | Azure
description: Describes how Azure Active Directory enables organizations to specify the apps to which each user has access.
services: active-directory
documentationcenter: ''
author: femila
manager: femila
editor: ''

ms.assetid: b0829f18-9e57-4107-925d-5f0457d81671
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
wacn.date: ''
ms.author: markvi
---

# Managing access to apps
Ongoing access management, usage evaluation, and reporting continue to be a challenge after an app is integrated into your organization's identity system. In many cases, IT Administrators or helpdesk have to take an ongoing active role in managing access to your apps. Sometimes, assignment is performed by a general or divisional IT team. Often, the assignment decision is intended to be delegated to the business decision maker, requiring their approval before IT makes the assignment.  Other organizations invest in integration with an existing automated identity and access management system, like Role-Based Access Control (RBAC) or Attribute-Based Access Control (ABAC). Both the integration and rule development tend to be specialized and expensive. Monitoring or reporting on either management approach is its own separate, costly, and complex investment.

## How does Azure Active Directory help?
 Azure AD supports extensive access management for configured applications, enabling organizations to easily achieve the right access policies ranging from automatic, attribute-based assignment (ABAC or RBAC scenarios) through delegation and including administrator management. With Azure AD you can easily achieve complex policies, combining multiple management models for a single application and can even re-use management rules across applications with the same audiences.

- [Adding new or existing applications](./active-directory-sso-integrate-saas-apps.md)

 Azure AD's application assignment focuses following assignment mode:

- **Individual assignment** An IT admin with directory Global Administrator permissions can select individual user accounts and grant them access to the application.

## How can I get started?

First, if you aren't already using Azure AD and you are an IT admin:

- [Try it out!](https://www.azure.cn/pricing/1rmb-trial/) - you can sign up for a 1rmb trial today and deploy your first cloud solution using this link.

Azure AD features that enable account sharing include:

- Adding applications to Azure AD
- Getting started with assignment
- Application assignment FAQ
- [App usage dashboard/reports](./active-directory-passwords-get-insights.md)

## Where can I learn more?

- [Article Index for Application Management in Azure Active Directory](./active-directory-apps-index.md)