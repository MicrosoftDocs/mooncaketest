---
title: Azure PowerShell Script-Import-bacpac-SQL database | Microsoft Docs
description: Azure PowerShell Script Sample - Import from a bacpac into a SQL database using PowerShell
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

# Import from a bacpac into a SQL database using PowerShell

This sample PowerShell script imports a database from a bacpac.  

Before running this script, ensure that a connection with Azure has been created using the `Add-AzureRmAccount` cmdlet.

## Sample script

```powershell
# Set an admin login and password for your database
$adminlogin = "ServerAdmin"
$password = "ChangeYourAdminPassword1"
# The logical server name has to be unique in the system
$servername = "server-$($(Get-AzureRMContext).Subscription.SubscriptionId)"
# The storage account name has to be unique in the system
$storageaccountname = $("sql$($(Get-AzureRMContext).Subscription.SubscriptionId)").substring(0,23).replace("-", "")
# The ip address range that you want to allow to access your DB
$startip = "0.0.0.0"
$endip = "255.255.255.255"

# Create a new resource group
New-AzureRmResourceGroup -Name "myResourceGroup" -Location "northcentralus"

# Create a new Storage Account 
New-AzureRmStorageAccount -ResourceGroupName "myResourceGroup" `
    -AccountName $storageaccountname `
    -Location "northcentralus" `
    -Type "Standard_LRS"

# Create a new storage container 
New-AzureStorageContainer -Name "importsample" `
    -Context $(New-AzureStorageContext -StorageAccountName $storageaccountname `
        -StorageAccountKey $(Get-AzureRmStorageAccountKey -ResourceGroupName "myResourceGroup" -StorageAccountName $storageaccountname).Value[0])

# Download sample database from Github
Invoke-WebRequest -Uri "https://github.com/Microsoft/sql-server-samples/releases/download/wide-world-importers-v1.0/WideWorldImporters-Standard.bacpac" -OutFile "sample.bacpac"

# Upload sample database into storage container
Set-AzureStorageBlobContent -Container "importsample" `
    -File "sample.bacpac" `
    -Context $(New-AzureStorageContext -StorageAccountName $storageaccountname `
        -StorageAccountKey $(Get-AzureRmStorageAccountKey -ResourceGroupName "myResourceGroup" -StorageAccountName $storageaccountname).Value[0])

# Create a new server with a system wide unique server name
New-AzureRmSqlServer -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -Location "northcentralus" `
    -SqlAdministratorCredentials $(New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList "ServerAdmin", $(ConvertTo-SecureString -String "ASecureP@assw0rd" -AsPlainText -Force))

# Open up the server firewall so we can connect
New-AzureRmSqlServerFirewallRule -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -FirewallRuleName "AllowAll" -StartIpAddress $startip -EndIpAddress $endip

# Import bacpac
$importRequest = New-AzureRmSqlDatabaseImport -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName "MyImportSample" `
    -DatabaseMaxSizeBytes "262144000" `
    -StorageKeyType "StorageAccessKey" `
    -StorageKey $(Get-AzureRmStorageAccountKey -ResourceGroupName "myResourceGroup" -StorageAccountName $storageaccountname).Value[0] `
    -StorageUri "http://$storageaccountname.blob.core.windows.net/importsample/sample.bacpac" `
    -Edition "Standard" `
    -ServiceObjectiveName "S0" `
    -AdministratorLogin "ServerAdmin" `
    -AdministratorLoginPassword $(ConvertTo-SecureString -String "ASecureP@assw0rd" -AsPlainText -Force)

# Check import status and wait for the import to complete
$importStatus = Get-AzureRmSqlDatabaseImportExportStatus -OperationStatusLink $importRequest.OperationStatusLink
[Console]::Write("Importing")
while ($importStatus.Status -eq "InProgress")
{
    $importStatus = Get-AzureRmSqlDatabaseImportExportStatus -OperationStatusLink $importRequest.OperationStatusLink
    [Console]::Write(".")
    Start-Sleep -s 10
}
[Console]::WriteLine("")
$importStatus
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
| [New-AzureRmResourceGroup]() | Creates a resource group in which all resources are stored. |
| [New-AzureRmSqlServer]() | Creates a logical server that hosts the SQL Database. |
| [New-AzureRmSqlServerFirewallRule]() | Creates a firewall rule to allow access to all SQL Databases on the server from the entered IP address range. |
| [New-AzureRmSqlDatabase]() | Creates the SQL Database in the logical server. |
| [Remove-AzureRmResourceGroup]() | Deletes a resource group including all nested resources. |

## Next steps

For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).

Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).