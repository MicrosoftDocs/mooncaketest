---
title: Creating or importing a runbook in Azure Automation
description: This article describes how to create a new runbook in Azure Automation or import one from a file.
services: automation
documentationcenter: ''
author: mgoedtel
manager: jwhit
editor: tysonn

ms.assetid: 24414362-b690-4474-8ca7-df18e30fc31d
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/12/2016
wacn.date: ''
ms.author: magoedte;bwren

---
# Creating or importing a runbook in Azure Automation
You can add a runbook to Azure Automation by either [creating a new one](#creating-a-new-runbook) or by importing an existing runbook from a file or from the [Runbook Gallery](automation-runbook-gallery.md). This article provides information on creating and importing runbooks from a file.  You can get all of the details on accessing community runbooks and modules in [Runbook and module galleries for Azure Automation](automation-runbook-gallery.md).

## <a name="creating-a-new-runbook"></a> Creating a new runbook
You can create a new runbook in Azure Automation using one of the Azure Classic Management Portal or Windows PowerShell. Once the runbook has been created, you can edit it using information in [Learning PowerShell Workflow](automation-powershell-workflow.md).

### To create a new Azure Automation runbook with the Azure Classic Management Portal
You can only work with PowerShell Workflow runbooks in the Azure Classic Management Portal.

1. In the Azure Classic Management Portal, click, **New**, **App Services**, **Automation**, **Runbook**, **Quick Create**.
2. Enter the required information, and then click **Create**. The runbook name must start with a letter and can have letters, numbers, underscores, and dashes.
3. If you want to edit the runbook now, then click **Edit Runbook**. Otherwise, click **OK**.
4. Your new runbook will appear on the **Runbooks** tab.

### To create a new Azure Automation runbook with Windows PowerShell
You can use the [New-AzureAutomationRunbook](https://msdn.microsoft.com/zh-cn/library/dn690272.aspx) cmdlet to create an empty PowerShell Workflow runbook. You can either specify the **Name** parameter to create an empty runbook that you can later edit, or you can specify the **Path** parameter to import a script file. 

The following sample commands show how to create a new empty runbook.

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Sample-TestRunbook"
    New-AzureAutomationRunbook -AutomationAccountName $automationAccountName -Name $runbookName

## <a name="ImportRunbook"></a> Importing a runbook from a file into Azure Automation
You can create a new runbook in Azure Automation by importing a PowerShell Workflow (.ps1 extension).

If the file contains multiple PowerShell Workflows, then the import will fail. You must save each workflow to its own file and import each separately.

### To import a runbook from a file with the Azure Classic Management Portal
You can use the following procedure to import a script file into Azure Automation.  Note that you can only import a .ps1 file into a PowerShell Workflow runbook using this portal.

1. In the Azure Classic Management portal, select **Automation** and then select an Automation Account.
2. Click **Import**.
3. Click **Browse for File** and locate the script file to import.
4. If you want to edit the runbook now, then click **Edit Runbook**. Otherwise, click OK.
5. The new runbook will appear on the **Runbooks** tab for the Automation Account.
6. You must [publish the runbook](#publishing-a-runbook) before you can run it.

### <a name="ImportRunbookScriptPS"></a> To import a runbook from a script file with Windows PowerShell
You can use the [Set-AzureAutomationRunbookDefinition](https://msdn.microsoft.com/zh-cn/library/dn690267.aspx) cmdlet to import a script file into the Draft version of an existing runbook. The script file must contain a single Windows PowerShell Workflow. If the runbook already has a Draft version, then the import will fail unless you use the Overwrite parameter. After the runbook has been imported, you can publish it with [Publish-AzureAutomationRunbook](https://msdn.microsoft.com/zh-cn/library/dn690266.aspx).

The following sample commands show how to import a script file into a runbook.

    $automationAccountName =  "AutomationAccount"
    $runbookName = "Sample_TestRunbook"
    $scriptPath = "C:\Runbooks\Sample_TestRunbook.ps1"

    Set-AzureAutomationRunbookDefinition -AutomationAccountName $automationAccountName -Name $runbookName -Path $ scriptPath -Overwrite
    Publish-AzureAutomationRunbook -AutomationAccountName $automationAccountName -Name $runbookName

## <a name="publishing-a-runbook"></a> Publishing a runbook
When you create or import a new runbook, you must publish it before you can run it.  Each runbook in Automation has a Draft and a Published version. Only the Published version is available to be run, and only the Draft version can be edited. The Published version is unaffected by any changes to the Draft version. When the Draft version should be made available, then you publish it which overwrites the Published version with the Draft version.

## To publish a runbook using the Azure Classic Management Portal
1. Open the runbook in the Azure Classic Management Portal.
2. At the top of the screen, click **Author**.
3. At the bottom of the screen, click **Publish** and then **Yes** to the verification message.

## To publish a runbook using Windows PowerShell
You can use the [Publish-AzureAutomationRunbook](https://msdn.microsoft.com/zh-cn/library/dn690266.aspx) cmdlet to publish a runbook with Windows PowerShell. The following sample commands show how to publish a sample runbook.

    $automationAccountName = "AutomationAccount"
    $runbookName = "Sample_TestRunbook"

    Publish-AzureAutomationRunbook -AutomationAccountName $automationAccountName -Name $runbookName

## Next Steps
* To learn about how you can benefit from the Runbook and PowerShell Module Gallery, see  [Runbook and module galleries for Azure Automation](automation-runbook-gallery.md)
* To learn more about editing PowerShell and PowerShell Workflow runbooks with a textual editor, see [Editing textual runbooks in Azure Automation](automation-edit-textual-runbook.md)