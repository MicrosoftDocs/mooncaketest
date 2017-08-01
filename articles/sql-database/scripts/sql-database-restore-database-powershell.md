---
title: Azure PowerShell Script-Restore a SQL database | Microsoft Docs
description: Azure PowerShell Script Sample - Restore a SQL database using PowerShell
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

# Restore a SQL database using PowerShell

This sample PowerShell script restores an Azure SQL database from a geo-redundant backup and restores a deleted database to the latest backup.  

Before running this script, ensure that a connection with Azure has been created using the `Add-AzureRmAccount` cmdlet.

## Sample script

```powershell
# Set an admin login and password for your database
$adminlogin = "ServerAdmin"
$password = "ChangeYourAdminPassword1"
# The logical server name has to be unique in the system
$servername = "server-$($(Get-AzureRMContext).Subscription.SubscriptionId)"

# Create a new resource group
New-AzureRmResourceGroup -Name "myResourceGroup" -Location "China East"

# Create a new server with a system wide unique server name
New-AzureRmSqlServer -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -Location "China East" `
    -SqlAdministratorCredentials $(New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $adminlogin, $(ConvertTo-SecureString -String $password -AsPlainText -Force))

# Create a blank database with S0 performance level
New-AzureRmSqlDatabase  -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName "MySampleDatabase" `
    -RequestedServiceObjectiveName "S0"

# Restore database from latest geo-redundant backup into existing server 
$GeoBackup = Get-AzureRmSqlDatabaseGeoBackup -ResourceGroupName "myResourceGroup" -ServerName $servername -DatabaseName "MySampleDatabase"
Restore-AzureRmSqlDatabase -FromGeoBackup `
    -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -TargetDatabaseName "MySampleDatabase_GeoRestore" `
    -ResourceId $GeoBackup.ResourceID `
    -Edition "Standard" `
    -ServiceObjectiveName "S0"

# Restore database to its state 10 minutes ago
# Note: Point-in-time restore requires database to be at least 5 minutes old
# Restore-AzureRmSqlDatabase -FromPointInTimeBackup `
#      -PointInTime (Get-Date).AddMinutes(-10) `
#      -ResourceGroupName "myResourceGroup" `
#      -ServerName $servername `
#      -TargetDatabaseName "MySampleDatabase_10MinutesAgo" `
#      -ResourceId $(Get-AzureRmSqlDatabase -ResourceGroupName "myResourceGroup" -ServerName $servername -DatabaseName "MySampleDatabase_DeletedRestore").ResourceID `
#      -Edition "Standard" `
#      -ServiceObjectiveName "S0"

# Delete original database
Remove-AzureRmSqlDatabase -ResourceGroupName "myResourceGroup" -ServerName $servername -DatabaseName "MySampleDatabase"

# Restore deleted database 
$deletedDatabase = Get-AzureRmSqlDeletedDatabaseBackup -ResourceGroupName "myResourceGroup" -ServerName $servername -DatabaseName "MySampleDatabase"
Restore-AzureRmSqlDatabase -FromDeletedDatabaseBackup `
    -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -TargetDatabaseName "MySampleDatabase_DeletedRestore" `
    -ResourceId $deletedDatabase.ResourceID `
    -DeletionDate $deletedDatabase.DeletionDate `
    -Edition "Standard" `
    -ServiceObjectiveName "S0"
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
| [New-AzureRmResourceGroup](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | Creates a resource group in which all resources are stored. | [New-AzureRmSqlServer](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.5.0/new-azurermsqlserver) | Creates a logical server that hosts a database or elastic pool. | 
| [New-AzureRmSqlDatabase](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.5.0/new-azurermsqldatabase) | Creates a database in a logical server as a single or a pooled database. |
[Get-AzureRmSqlDatabaseGeoBackup](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.5.0/get-azurermsqldatabasegeobackup) | Gets a geo-redundant backup of a database. |
| [Restore-AzureRmSqlDatabase](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.5.0/restore-azurermsqldatabase) | Restores a SQL database. |
|[Remove-AzureRmSqlDatabase](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.5.0/remove-azurermsqldatabase) | Removes an Azure SQL database. |
| [Get-AzureRmSqlDeletedDatabaseBackup](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.5.0/get-azurermsqldeleteddatabasebackup) | Gets a deleted database that you can restore. |
| [Remove-AzureRmResourceGroup]() | Deletes a resource group including all nested resources. |

## Next steps

For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).

Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).
