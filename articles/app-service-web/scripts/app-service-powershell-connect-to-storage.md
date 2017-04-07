---
title: Azure PowerShell Script Sample - Connect a web app to a storage account | Azure
description: Azure PowerShell Script Sample - Connect a web app to a storage account
services: app-service\web
documentationcenter: ''
author: syntaxc4
manager: erikre
editor: ''
tags: azure-service-management

ms.assetid: e4831bdc-2068-4883-9474-0b34c2e3e255
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
wacn.date: ''
ms.author: cfowler
---

# Connect a web app to a storage account

In this scenario you will learn how to create an Azure storage account and an Azure web app. Then you will link the storage account to the web app using app settings.

If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount -EnvironmentName AzureChinaCloud` to create a connection with Azure.

## Sample script

```powershell
# Generates a Random Value
$Random=(New-Guid).ToString().Substring(0,8)

# Variables
$ResourceGroup="MyResourceGroup$Random"
$AppName="webappwithStorage$Random"
$StorageName="webappstorage$Random"
$Location="China North"

# Create a Resource Group
New-AzureRMResourceGroup -Name $ResourceGroup -Location $Location

# Create an App Service Plan
New-AzureRMAppservicePlan -Name WebAppwithStoragePlan -ResourceGroupName $ResourceGroup -Location $Location -Tier Basic

# Create a Web App in the App Service Plan
New-AzureRMWebApp -Name $AppName -ResourceGroupName $ResourceGroup -Location $Location -AppServicePlan WebAppwithStoragePlan

# Create Storage Account
New-AzureRMStorageAccount -Name $StorageName -ResourceGroupName $ResourceGroup -Location $Location -SkuName Standard_LRS

# Get Connection String for Storage Account
$StorageKey=(Get-AzureRMStorageAccountKey -ResourceGroupName $ResourceGroup -Name $StorageName).Value[0]

# Assign Connection String to App Setting 
Set-AzureRMWebApp -ConnectionStrings @{ MyStorageConnStr = @{ Type="Custom"; Value="DefaultEndpointsProtocol=https;AccountName=$StorageName;AccountKey=$StorageKey;" } } -Name $AppName -ResourceGroupName $ResourceGroup
```

## Clean up deployment 

After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## Script explanation

This script uses the following commands. Each command in the table links to command specific documentation.

| Command | Notes |
|---|---|
| [New-AzureRmResourceGroup](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Resources/v3.5.0/new-azurermresourcegroup) | Creates a resource group in which all resources are stored. |
| [New-AzureRmAppServicePlan](https://docs.microsoft.com/powershell/resourcemanager/azurerm.websites/v2.5.0/new-azurermappserviceplan) | Creates an App Service plan. |
| [New-AzureRmWebApp](https://docs.microsoft.com/powershell/resourcemanager/azurerm.websites/v2.5.0/new-azurermwebapp) | Creates a web app. |
| [New-AzureRMStorageAccount](https://docs.microsoft.com/powershell/resourcemanager/azurerm.storage/v2.5.0/New-AzureRmStorageAccount) | Creates a Storage account. |
| [Get-AzureRMStorageAccountKey](https://docs.microsoft.com/powershell/resourcemanager/azurerm.storage/v2.5.0/get-azurermstorageaccountkey) | Gets the access keys for an Azure Storage account. |
| [Set-AzureRmWebApp](https://docs.microsoft.com/powershell/resourcemanager/azurerm.websites/v2.5.0/set-azurermwebapp) | Modifies a web app's configuration. |

## Next steps

For more information on the Azure PowerShell module, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/).

Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).