---
title: Assigning administrator roles in Azure Active Directory | Azure
description: Explains what administrator roles are available with Azure Active Directory and how to assign them.
services: active-directory
documentationcenter: ''
author: curtand
manager: femila
editor: ''

ms.assetid: 7fc27e8e-b55f-4194-9b8f-2e95705fb731
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/07/2017
wacn.date: ''
ms.author: curtand
---

# Assigning administrator roles in Azure Active Directory
Using Azure Active Directory (Azure AD), you can designate separate administrators to serve different functions. These administrators will have access to various features in the Azure portal or Azure Classic Management Portal and, depending on their role, will be able to create or edit users, assign administrative roles to others, reset user passwords, manage user licenses, and manage domains, among other things. A user who is assigned an admin role will have the same permissions across all of the cloud services that your organization has subscribed to, regardless of whether you assign the role in the Office 365 portal, or in the Azure Classic Management Portal, or by using the Azure AD module for Windows PowerShell.

The following administrator roles are available:

- **Global administrator / Company Administrator**: Has access to all administrative features. The person who signs up for the Azure account becomes a global administrator. Only global administrators can assign other administrator roles. There can be more than one global administrator at your company.

  > [!NOTE]
  > In Microsoft Graph API, Azure AD Graph API, and Azure AD PowerShell, this role is identified as "Company Administrator". It is "Global Administrator" in the [Azure portal](https://portal.azure.cn).
  >
  >

## Administrator permissions

### Global administrator
| Can do | Cannot do |
| --- | --- |
| <p>View company and user information</p><p>Manage Office support tickets</p><p>Perform billing and purchasing operations for Office products</p> <p>Reset user passwords</p><p>Create and manage user views</p><p>Create, edit, and delete users and groups, and manage user licenses</p><p>Manage domains</p><p>Manage company information</p><p>Delegate administrative roles to others</p><p>Use directory synchronization</p><p>Enable or disable multi-factor authentication</p><p>View reports</p> |N/A |

## Details about the global administrator role
The global administrator has access to all administrative features. By default, the person who signs up for an Azure subscription is assigned the global administrator role for the directory. Only global administrators can assign other administrator roles.

## Assign or remove administrator roles
1. In the [Azure Classic Management Portal](https://manage.windowsazure.cn), click **Active Directory**, and then click the name of your organization’s directory.
2. On the **Users** page, click the display name of the user you want to edit.
3. In the **Organizational Role** list, select the administrator role that you want to assign to this user, or select **User** if you want to remove an existing administrator role.
4. In the **Alternate Email Address** box, type an email address. This email address is used for important notifications, including password self-reset, so the user must be able to access the email account whether or not the user can access Azure.
5. Select **Allow** or **Block** to specify whether to allow the user to sign in and access services.
6. Specify a location from the **Usage Location** drop-down list.
7. When you have finished, click **Save**.

## Next steps
- To learn more about how resource access is controlled in Azure, see [Understanding resource access in Azure](./active-directory-understanding-resource-access.md)
- For more information on how Azure Active Directory relates to your Azure subscription, see [How Azure subscriptions are associated with Azure Active Directory](./active-directory-how-subscriptions-associated-directory.md)
- [Manage users](./active-directory-create-users.md)
- [Manage passwords](./active-directory-manage-passwords.md)