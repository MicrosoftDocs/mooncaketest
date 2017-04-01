---
title: Azure PowerShell Script Sample - Connect a web app to a SQL database | Azure
description: Azure PowerShell Script Sample - Connect a web app to a SQL database
services: app-service\web
documentationcenter: ''
author: syntaxc4
manager: erikre
editor: ''
tags: azure-service-management

ms.assetid: 055440a9-fff1-49b2-b964-9c95b364e533
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
wacn.date: ''
ms.author: cfowler
---

# Connect a web app to a SQL database

In this scenario you will learn how to create an Azure SQL database and an Azure web app. Then you will link the SQL database to the web app using app settings.

If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount -EnvironmentName AzureChinaCloud` to create a connection with Azure.

## Sample script

```powershell
# Generates a Random Value
$Random=(New-Guid).ToString().Substring(0,8)

# Variables
$ResourceGroup="MyResourceGroup$Random"
$AppName="webappwithSQL$Random"
$Location="China North"
$ServerName="webappwithsql$Random"
$StartIP="0.0.0.0"
$EndIP="0.0.0.0"
$Username="ServerAdmin"
$Password="<provide-a-password>"
$SqlServerPassword=New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $Username,(ConvertTo-SecureString -String $Password -AsPlainText -Force)

# Create a Resource Group
New-AzureRMResourceGroup -Name $ResourceGroup -Location $Location

# Create an App Service Plan
New-AzureRMAppservicePlan -Name WebAppwithSQLPlan -ResourceGroupName $ResourceGroup -Location $Location -Tier Basic

# Create a Web App in the App Service Plan
New-AzureRMWebApp -Name $AppName -ResourceGroupName $ResourceGroup -Location $Location -AppServicePlan WebAppwithSQLPlan

# Create a SQL Database Server
New-AzureRMSQLServer -ServerName $ServerName -Location $Location -SqlAdministratorCredentials $SqlServerPassword -ResourceGroupName $ResourceGroup

# Create Firewall Rule for SQL Database Server
New-AzureRmSqlServerFirewallRule -FirewallRuleName "AllowYourIp" -StartIpAddress $StartIP -EndIPAddress $EndIP -ServerName $ServerName -ResourceGroupName $ResourceGroup

# Create SQL Database in SQL Database Server
New-AzureRMSQLDatabase -ServerName $ServerName -DatabaseName MySampleDatabase -ResourceGroupName $ResourceGroup

# Assign Connection String to Connection String 
Set-AzureRMWebApp -ConnectionStrings @{ MyConnectionString = @{ Type="SQLAzure"; Value ="Server=tcp:$ServerName.database.chinacloudapi.cn;Database=MySampleDatabase;User ID=$Username@$ServerName;Password=$password;Trusted_Connection=False;Encrypt=True;" } } -Name $AppName -ResourceGroupName $ResourceGroup
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
| [New-AzureRMSQLServer](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.5.0/new-azurermsqlserver) | Creates a SQL Database server. |
| [New-AzureRmSqlServerFirewallRule](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.5.0/new-azurermsqlserverfirewallrule) | Creates a firewall rule for a SQL Database server. |
| [New-AzureRMSQLDatabase](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.5.0/new-azurermsqldatabase) | Creates a database or an elastic database. |
| [Set-AzureRmWebApp](https://docs.microsoft.com/powershell/resourcemanager/azurerm.websites/v2.5.0/set-azurermwebapp) | Modifies a web app's configuration. |

## Next steps

For more information on the Azure PowerShell module, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/).

Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).