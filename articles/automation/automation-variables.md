---
title: Variable assets in Azure Automation | Azure
description: Variable assets are values that are available to all runbooks in Azure Automation.  This article explains the details of variables and how to work with them in textual authoring.
services: automation
documentationcenter: ''
author: mgoedtel
manager: carmonm
editor: tysonn

ms.assetid: b880c15f-46f5-4881-8e98-e034cc5a66ec
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/10/2017
wacn.date: ''
ms.author: magoedte;bwren

---
# Variable assets in Azure Automation

Variable assets are values that are available to all runbooks in your automation account. They can be created, modified, and retrieved from the Azure Classic Management Portal, Windows PowerShell, and from within a runbook. Automation variables are useful for the following scenarios:

- Share a value between multiple runbooks.

- Share a value between multiple jobs from the same runbook.

- Manage a value from the portal or from the Windows PowerShell command line that is used by runbooks.

Automation variables are persisted so that they continue to be available even if the runbook fails.  This also allows a value to be set by one runbook that is then used by another, or is used by the same runbook the next time that it is run.

When a variable is created, you can specify that it be stored encrypted.  When a variable is encrypted, it is stored securely in Azure Automation, and its value cannot be retrieved from the [Get-AzureAutomationVariable](http://msdn.microsoft.com/zh-cn/library/dn913772.aspx) cmdlet that ships as part of the Azure PowerShell module.  The only way that an encrypted value can be retrieved is from the **Get-AutomationVariable** activity in a runbook.

> [!NOTE]
> Secure assets in Azure Automation include credentials, certificates, connections, and encrypted variables. These assets are encrypted and stored in the Azure Automation using a unique key that is generated for each automation account. This key is encrypted by a master certificate and stored in Azure Automation. Before storing a secure asset, the key for the automation account is decrypted using the master certificate and then used to encrypt the asset.

## <a id="variable-types"></a> Variable types

When you create a variable with the Azure Classic Management Portal, you must specify a data type from the dropdown list so the portal can display the appropriate control for entering the variable value. The variable is not restricted to this data type, but you must set the variable using Windows PowerShell if you want to specify a value of a different type. If you specify **Not defined**, then the value of the variable is set to **$null**, and you must set the value with the [Set-AzureAutomationVariable](http://msdn.microsoft.com/zh-cn/library/dn913767.aspx) cmdlet or **Set-AutomationVariable** activity.  You cannot create or change the value for a complex variable type in the portal, but you can provide a value of any type using Windows PowerShell. Complex types are returned as a [PSCustomObject](http://msdn.microsoft.com/zh-cn/library/system.management.automation.pscustomobject.aspx).

You can store multiple values to a single variable by creating an array or hashtable and saving it to the variable.

The following are a list of variable types available in Automation:

* String
* Integer
* DateTime
* Boolean
* Null

>[!NOTE]
>Variable assets are limited to 1024 characters. 

## Cmdlets and workflow activities

The cmdlets in the following table are used to create and manage Automation variables with Windows PowerShell. They ship as part of the [Azure PowerShell module](https://docs.microsoft.com/powershell/azureps-cmdlets-docs), which is available for use in Automation runbooks.

|Cmdlets|Description|
|:---|:---|
|[Get-AzureAutomationVariable](http://msdn.microsoft.com/zh-cn/library/dn913772.aspx)|Retrieves the value of an existing variable.|
|[New-AzureAutomationVariable](http://msdn.microsoft.com/zh-cn/library/dn913771.aspx)|Creates a new variable and sets its value.|
|[Remove-AzureAutomationVariable](http://msdn.microsoft.com/zh-cn/library/dn913775.aspx)|Removes an existing variable.|
|[Set-AzureAutomationVariable](http://msdn.microsoft.com/zh-cn/library/dn913767.aspx)|Sets the value for an existing variable.|

The workflow activities in the following table are used to access Automation variables in a runbook. They are only available for use in a runbook, and do not ship as part of the Azure PowerShell module.

|Workflow Activities|Description|
|:---|:---|
|Get-AutomationVariable|Retrieves the value of an existing variable.|
|Set-AutomationVariable|Sets the value for an existing variable.|

> [!NOTE] 
> You should avoid using variables in the -Name parameter of **Get-AutomationVariable**  in a runbook since this can complicate discovering dependencies between runbooks, and Automation variables at design time.

## Creating an Automation variable

### To create a variable with the Azure Classic Management Portal

1. From your automation account, click **Assets** at the top of the window.
1. At the bottom of the window, click **Add Setting**.
1. Click **Add Variable**.
1. Complete the wizard and click the checkbox to save the new variable.

### To create a variable with Windows PowerShell

The [New-AzureAutomationVariable](http://msdn.microsoft.com/zh-cn/library/dn913771.aspx) cmdlet creates a variable and sets its initial value. You can retrieve the value using [Get-AzureAutomationVariable](http://msdn.microsoft.com/zh-cn/library/dn913772.aspx). If the value is a simple type, then that same type is returned. If it's a complex type, then a **PSCustomObject** is returned.

The following sample commands show how to create a variable of type string and then return its value.

    New-AzureAutomationVariable -AutomationAccountName "MyAutomationAccount" -Name 'MyStringVariable' -Encrypted $false -Value 'My String'
    $string = (Get-AzureAutomationVariable -AutomationAccountName "MyAutomationAccount" -Name 'MyStringVariable').Value

The following sample commands show how to create a variable with a complex type and then return its properties. In this case, a virtual machine object from **Get-AzureVM** is used.

    $vm = Get-AzureVM -ServiceName "MyVM" -Name "MyVM"
    New-AzureAutomationVariable -AutomationAccountName "MyAutomationAccount" -Name "MyComplexVariable" -Encrypted $false -Value $vm

    $vmValue = (Get-AzureAutomationVariable -AutomationAccountName "MyAutomationAccount" -Name "MyComplexVariable").Value
    $vmName = $vmValue.Name
    $vmIpAddress = $vmValue.IpAddress

## Using a variable in a runbook

Use the **Set-AutomationVariable** activity to set the value of an Automation variable in a runbook, and the **Get-AutomationVariable** to retrieve it.  You shouldn't use the **Set-AzureAutomationVariable** or  **Get-AzureAutomationVariable** cmdlets in a runbook since they are less efficient than the workflow activities.  You also cannot retrieve the value of secure variables with **Get-AzureAutomationVariable**.  The only way to create a new variable from within a runbook is to use the [New-AzureAutomationVariable](http://msdn.microsoft.com/zh-cn/library/dn913771.aspx)  cmdlet.

### Textual runbook samples

#### Setting and retrieving a simple value from a variable

The following sample commands show how to set and retrieve a variable in a textual runbook. In this sample, it is assumed that variables of type integer named *NumberOfIterations* and *NumberOfRunnings* and a variable of type string named *SampleMessage* have already been created.

    $NumberOfIterations = Get-AutomationVariable -Name 'NumberOfIterations'
    $NumberOfRunnings = Get-AutomationVariable -Name 'NumberOfRunnings'
    $SampleMessage = Get-AutomationVariable -Name 'SampleMessage'

    Write-Output "Runbook has been run $NumberOfRunnings times."

    for ($i = 1; $i -le $NumberOfIterations; $i++) {
       Write-Output "$i`: $SampleMessage"
    }
    Set-AutomationVariable -Name NumberOfRunnings -Value ($NumberOfRunnings += 1)

#### Setting and retrieving a complex object in a variable

The following sample code shows how to update a variable with a complex value in a textual runbook. In this sample, an Azure virtual machine is retrieved with **Get-AzureVM** and saved to an existing Automation variable.  As explained in [Variable types](#variable-types), this is stored as a PSCustomObject.

    $vm = Get-AzureVM -ServiceName "MyVM" -Name "MyVM"
    Set-AutomationVariable -Name "MyComplexVariable" -Value $vm

In the following code, the value is retrieved from the variable and used to start the virtual machine.

    $vmObject = Get-AutomationVariable -Name "MyComplexVariable"
    if ($vmObject.PowerState -eq 'Stopped') {
       Start-AzureVM -ServiceName $vmObject.ServiceName -Name $vmObject.Name
    }

#### Setting and retrieving a collection in a variable

The following sample code shows how to use a variable with a collection of complex values in a textual runbook. In this sample, multiple Azure virtual machines are retrieved with **Get-AzureVM** and saved to an existing Automation variable.  As explained in [Variable types](#variable-types), this is stored as a collection of PSCustomObjects.

    $vms = Get-AzureVM | Where -FilterScript {$_.Name -match "my"}     
    Set-AutomationVariable -Name 'MyComplexVariable' -Value $vms

In the following code, the collection is retrieved from the variable and used to start each virtual machine.

    $vmValues = Get-AutomationVariable -Name "MyComplexVariable"
    ForEach ($vmValue in $vmValues)
    {
       if ($vmValue.PowerState -eq 'Stopped') {
          Start-AzureVM -ServiceName $vmValue.ServiceName -Name $vmValue.Name
       }
    }

