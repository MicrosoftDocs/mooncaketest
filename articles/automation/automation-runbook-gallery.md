---
title: Runbook and module galleries for Azure Automation | Azure
description: Runbooks and modules from Microsoft and the community are available for you to install and use in your Azure Automation environment.  This article describes how you can access these resources and to contribute your runbooks to the gallery.
services: automation
documentationcenter: ''
author: mgoedtel
manager: jwhit
editor: tysonn

ms.assetid: d3fee7b4-630a-4c10-8425-9bf51d7c9e58
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/14/2016
wacn.date: ''
ms.author: magoedte;bwren

---
# Runbook and module galleries for Azure Automation
Rather than creating your own runbooks and modules in Azure Automation, you can access a variety of scenarios that have already been built by Microsoft and the community.  You can either use these scenarios without modification or you can use them as a starting point and edit them for your specific requirements.

You can get runbooks from the [Runbook Gallery](#runbooks-in-runbook-gallery) and modules from the [PowerShell Gallery](#modules-in-powerShell-gallery).  You can also contribute to the community by sharing scenarios that you develop.

##<a name="runbooks-in-runbook-gallery"></a> Runbooks in Runbook Gallery
The [Runbook Gallery](http://gallery.technet.microsoft.com/scriptcenter/site/search?f[0].Type=RootCategory&f[0].Value=WindowsAzure&f[1].Type=SubCategory&f[1].Value=WindowsAzure_automation&f[1].Text=Automation) provides a variety of runbooks from Microsoft and the community that you can import into Azure Automation. You can download a runbook from the gallery which is hosted in the [TechNet Script Center](https://gallery.technet.microsoft.com/scriptcenter/site/upload), or you can directly import runbooks from the gallery from the Azure Classic Management Portal.

You can only import directly from the Runbook Gallery using the Azure Classic Management Portal. You cannot perform this function using Windows PowerShell.

> [!NOTE]
> You should validate the contents of any runbooks that you get from the Runbook Gallery and use extreme caution in installing and running them in a production environment.|
> 
> 

### To import a runbook from the Runbook Gallery with the Azure Classic Management Portal
1. In the Azure Classic Management Portal, click, **New**, **App Services**, **Automation**, **Runbook**, **From Gallery**.
2. Select a category to view related runbooks, and select a runbook to view its details. When you select the runbook you want, click the right arrow button.

    ![Runbook gallery](./media/automation-runbook-gallery/runbook-gallery.png)
3. Review the contents of the runbook and note any requirements in the description. Click the right arrow button when you're done.
4. Enter the runbook details and then click the checkmark button. The runbook name will already be filled in.
5. The runbook will appear on the **Runbooks** tab for the Automation Account.

###<a name="AddRunbook"></a> Adding a runbook to the runbook gallery
Microsoft encourages you to add runbooks to the Runbook Gallery that you think would be useful to other customers.  You can add a runbook by [uploading it to the Script Center](http://gallery.technet.microsoft.com/site/upload) taking into account the following details.

* You must specify *Windows Azure* for the **Category** and *Automation* for the **Subcategory** for the runbook to be displayed in the wizard.  
* The upload must be a single .ps1 file.  If the runbook requires any modules, child runbooks, or assets, then you should list those in the description of the submission and in the comments section of the runbook.  If you have a scenario requiring multiple runbooks, then upload each separately and list the names of the related runbooks in each of their descriptions. Make sure that you use the same tags so that they will show up in the same category. A user will have to read the description to know that other runbooks are required the scenario to work.
* Insert PowerShell Workflow code snippet into the description using **Insert code section** icon.
* The Summary for the upload will be displayed in the Runbook Gallery results so you should provide detailed information that will help a user identify the functionality of the runbook.
* You should assign one to three of the following Tags to the upload.  The runbook will be listed in the wizard under the categories that match its tags.  Any tags not on this list will be ignored by the wizard. If you don't specify any matching tags, the runbook will be listed under the Other category.

    * Backup
    * Capacity Management
    * Change Control
    * Compliance
    * Dev / Test Environments
    * Disaster Recovery
    * Monitoring
    * Patching
    * Provisioning
    * Remediation
    * VM Lifecycle Management
* Automation updates the Gallery once an hour, so you won't see your contributions immediately.

## Requesting a runbook or module
You can send requests to [User Voice](https://www.azure.cn/product-feedback).  If you need help writing a runbook or have a question about PowerShell, post a question to our [forum](http://social.msdn.microsoft.com/Forums/zh-cn/home?forum=windowsazurezhchsen-US/home?forum=azureautomation&filter=alltypes&sort=lastpostdesc).

## Next Steps
* To get started with runbooks, see [Creating or importing a runbook in Azure Automation](automation-creating-importing-runbook.md)
* [Learning PowerShell workflow](automation-powershell-workflow.md)