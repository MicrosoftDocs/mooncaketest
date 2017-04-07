---
title: Configure Azure AD User Account | Azure
description: This article describes how to configure Azure AD User account credential for runbooks in Azure Automation to authenticate with.
services: automation
documentationcenter: ''
author: MGoedtel
manager: jwhit
editor: tysonn
keywords: azure active directory user, azure service management, azure ad user account

ms.assetid: fcfe266d-b22e-4dfb-8272-adcab09fc0cf
ms.service: automation
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/14/2016
wacn.date: ''
ms.author: magoedte

---
# Authenticate Runbooks with Azure Service Management and Resource Manager
This article describes the steps you must perform to configure an Azure AD User account for Azure Automation runbooks running against Azure Service Management or Azure Resource Manager  resources.  While this continues to be a supported authentication identity for your Azure Resource Manager based runbooks, the recommended method is using the new Azure Run As account.       

## Create a new Azure Active Directory user
1. Log in to the Azure Classic Management Portal as a service administrator for the Azure subscription you want to manage.
2. Select **Active Directory**, and then select the name of your organization directory.
3. Select the **Users** tab, and then, in the command area, select **Add User**.
4. On the **Tell us about this user** page, under **Type of user**, select **New user in your organization**.
5. Enter a user name.  
6. Select the directory name that is associated with your Azure subscription on the Active Directory page.
7. On the **user profile** page, provide a first and last name, a user-friendly name, and User from the **Roles** list.  Do not **Enable Multi-Factor Authentication**.
8. Note the user's full name and temporary password.
9. Select **Settings > Administrators > Add**.
10. Type the full user name of the user that you created.
11. Select the subscription that you want the user to manage.
12. Log out of Azure and then log back in with the account you just created. You will be prompted to change the user's password.

## Create an Automation account in Azure Classic Management Portal
In this section, you will perform the following steps to create a new Azure Automation account in the Azure Classic Management Portal that will be used with your runbooks managing resources in Azure Service Manager and Azure Resource Manager mode.  

1. Log in to the Azure Classic Management Portal as a service administrator for the Azure subscription you want to manage.
2. Select **Automation**.
3. On the **Automation** page, select **Create an Automation Account**.
4. In the **Create an Automation Account** box, type in a name for your new Automation account and select a **Region** from the drop-down list.  
5. Click **OK** to accept your settings and create the account.
6. After it is created it will be listed on the **Automation** page.
7. Click on the account and it will bring you to the Dashboard page.  
8. On the Automation Dashboard page, select **Assets**.
9. On the **Assets** page, select **Add Settings** located at the bottom of the page.
10. On the **Add Settings** page, select **Add Credential**.
11. On the **Define Credential** page, select **Windows PowerShell Credential** from the **Credential Type** drop-down list and provide a name for the credential.
12. On the following **Define Credential** page type in the username of the AD user account created earlier in the **User Name** field and the password in the **Password** and **Confirm Password** fields. Click **OK** to save your changes.

## Use the credential in a runbook
You can retrieve the credential in a runbook using the [Get-AutomationPSCredential](automation-credentials.md) activity and then use it with [Add-AzureAccount](http://msdn.microsoft.com/zh-cn/library/azure/dn722528.aspx) to connect to your Azure subscription. If the credential is an administrator of multiple Azure subscriptions, then you should also use [Select-AzureSubscription](http://msdn.microsoft.com/zh-cn/library/dn495203.aspx) to specify the correct one. This is shown in the sample Windows PowerShell below that will typically appear at the top of most Azure Automation runbooks.

    $cred = Get-AutomationPSCredential -Name "myuseraccount.partner.onmschina.cn"
    Add-AzureAccount -Environment AzureChinaCloud -Credential $cred
    Select-AzureSubscription -SubscriptionName "My Subscription"

You should repeat these lines after any [checkpoints](http://technet.microsoft.com/zh-cn/library/dn469257.aspx#bk_Checkpoints) in your runbook. If the runbook is suspended and then resumes on another worker, then it will need to perform the authentication again.