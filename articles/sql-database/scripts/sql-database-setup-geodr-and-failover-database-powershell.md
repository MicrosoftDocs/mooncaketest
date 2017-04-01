---
title: Azure PowerShell Script-Set up geo-replication-single SQL Database | Microsoft Docs
description: Azure PowerShell Script Sample - Set up Active Geo-Replication for a single Azure SQL database using PowerShell
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management

ms.assetid:
ms.service: sql-database
ms.custom: sample
ms.devlang: PowerShell
ms.topic: article
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 03/07/2017
ms.author: janeng
---

# Configure Active Geo-Replication for a single Azure SQL database using PowerShell

This sample PowerShell script configures Active Geo-Replication for a single database and fails it over to the secondary replica.

Before running this script, ensure that a connection with Azure has been created using the `Add-AzureRmAccount` cmdlet.

## Sample Scripts

```powershell
# Set an admin login and password for your database
$adminlogin = "ServerAdmin"
$password = "ChangeYourAdminPassword1"
# The logical server names have to be unique in the system
$primaryservername = "primary-server-$($(Get-AzureRMContext).Subscription.SubscriptionId)"
$sercondaryservername = "secondary-server-$($(Get-AzureRMContext).Subscription.SubscriptionId)"

# Create two new resource groups
New-AzureRmResourceGroup -Name "myPrimaryResourceGroup" -Location "northcentralus"
New-AzureRmResourceGroup -Name "mySecondaryResourceGroup" -Location "southcentralus"

# Create two new logical servers with a system wide unique server name
New-AzureRmSqlServer -ResourceGroupName "myPrimaryResourceGroup" `
    -ServerName $primaryservername `
    -Location "northcentralus" `
    -SqlAdministratorCredentials $(New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $adminlogin, $(ConvertTo-SecureString -String $password -AsPlainText -Force))
New-AzureRmSqlServer -ResourceGroupName "mySecondaryResourceGroup" `
    -ServerName $sercondaryservername `
    -Location "southcentralus" `
    -SqlAdministratorCredentials $(New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $adminlogin, $(ConvertTo-SecureString -String $password -AsPlainText -Force))

# Create a blank database with S0 performance level on the primary server
New-AzureRmSqlDatabase  -ResourceGroupName "myPrimaryResourceGroup" `
    -ServerName $primaryservername `
    -DatabaseName "MySampleDatabase" -RequestedServiceObjectiveName "S0"

# Establish Active Geo-Replication
$myDatabase = Get-AzureRmSqlDatabase -DatabaseName "MySampleDatabase" -ResourceGroupName "myPrimaryResourceGroup" -ServerName $primaryservername
$myDatabase | New-AzureRmSqlDatabaseSecondary -PartnerResourceGroupName "mySecondaryResourceGroup" -PartnerServerName $sercondaryservername -AllowConnections "All"

# Initiate a planned failover
$myDatabase = Get-AzureRmSqlDatabase -DatabaseName "MySampleDatabase" -ResourceGroupName "mySecondaryResourceGroup" -ServerName $sercondaryservername
$myDatabase | Set-AzureRmSqlDatabaseSecondary -PartnerResourceGroupName "myPrimaryResourceGroup" -Failover

# Monitor Geo-Replication config and health after failover
$myDatabase = Get-AzureRmSqlDatabase -DatabaseName "MySampleDatabase" -ResourceGroupName "mySecondaryResourceGroup" -ServerName $sercondaryservername
$myDatabase | Get-AzureRmSqlDatabaseReplicationLink -PartnerResourceGroupName "myPrimaryResourceGroup" -PartnerServerName $primaryservername

# Remove the replication link after the failover
$myDatabase = Get-AzureRmSqlDatabase -DatabaseName "MySampleDatabase" -ResourceGroupName "mySecondaryResourceGroup" -ServerName $sercondaryservername
$secondaryLink = $myDatabase | Get-AzureRmSqlDatabaseReplicationLink -PartnerResourceGroupName "myPrimaryResourceGroup" -PartnerServerName $primaryservername
$secondaryLink | Remove-AzureRmSqlDatabaseSecondary
```

## Clean up deployment

After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## Script explanation

This script uses the following commands. Each command in the table links to command specific documentation.

| Command | Notes |
|---|---|
| [New-AzureRmResourceGroup](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | Creates a resource group in which all resources are stored. |
| [New-AzureRmSqlServer](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.5.0/new-azurermsqlserver) | Creates a logical server that hosts a database or elastic pool. |
| [New-AzureRmSqlElasticPool](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.5.0/new-azurermsqlelasticpool) | Creates an elastic pool within a logical server. |
| [Set-AzureRmSqlDatabase](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.5.0/set-azurermsqldatabase) | Updates database properties or moves a database into, out of, or between elastic pools. |
| [New-AzureRmSqlDatabaseSecondary](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.5.0/new-azurermsqldatabasesecondary)| Creates a secondary database for an existing database and starts data replication. |
| [Get-AzureRmSqlDatabase](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.5.0/get-azurermsqldatabase)| Gets one or more databases. |
| [Set-AzureRmSqlDatabaseSecondary](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.5.0/set-azurermsqldatabasesecondary)| Switches a secondary database to be primary to initiate failover.|
| [Get-AzureRmSqlDatabaseReplicationLink](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.5.0/get-azurermsqldatabasereplicationlink) | Gets the geo-replication links between an Azure SQL Database and a resource group or SQL Server. |
| [Remove-AzureRmSqlDatabaseSecondary](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.5.0/remove-azurermsqldatabasesecondary) | Terminates data replication between a SQL Database and the specified secondary database. |
| [Remove-AzureRmResourceGroup](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/remove-azurermresourcegroup) | Deletes a resource group including all nested resources. |
|||

## Next steps

For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).

Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).
