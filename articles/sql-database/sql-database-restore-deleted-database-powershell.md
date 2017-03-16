---
title: 还原已删除的 Azure SQL 数据库 (PowerShell) | Azure
description: 还原已删除的 Azure SQL 数据库 (PowerShell)。
services: sql-database
documentationCenter: ''
authors: stevestein
manager: jhubbard
editor: ''

ms.service: sql-database
ms.devlang: NA
ms.date: 10/12/2016
wacn.date: 12/26/2016
ms.author: sstein
ms.workload: NA
ms.topic: article
ms.tgt_pltfrm: NA
---

# 使用 PowerShell 还原已删除的 Azure SQL 数据库

> [!div class="op_single_selector"]
- [概述](./sql-database-recovery-using-backups.md)
- [还原已删除的 DB：门户预览](./sql-database-restore-deleted-database-portal.md)
- [**还原已删除的 DB：PowerShell**](./sql-database-restore-deleted-database-powershell.md)

[!INCLUDE [启动 PowerShell 会话](../../includes/sql-database-powershell.md)]

## 获取已删除数据库的列表

```
$resourceGroupName = "resourcegroupname"
$sqlServerName = "servername"

$DeletedDatabases = Get-AzureRmSqlDeletedDatabaseBackup -ResourceGroupName $resourceGroupName -ServerName $sqlServerName
```

## 将已删除的数据库还原为独立数据库

使用 [Get-AzureRmSqlDeletedDatabaseBackup](https://msdn.microsoft.com/zh-cn/library/azure/mt693387.aspx) cmdlet 获取要还原的已删除数据库备份。然后，使用 [Restore-AzureRmSqlDatabase](https://msdn.microsoft.com/zh-cn/library/azure/mt693390.aspx) cmdlet 从已删除的数据库备份开始还原。

```
$resourceGroupName = "resourcegroupname"
$sqlServerName = "servername"
$databaseName = "deletedDbToRestore"

$DeletedDatabase = Get-AzureRmSqlDeletedDatabaseBackup -ResourceGroupName $resourceGroupName -ServerName $sqlServerName -DatabaseName $databaseName

Restore-AzureRmSqlDatabase –FromDeletedDatabaseBackup –DeletionDate $DeletedDatabase.DeletionDate -ResourceGroupName $DeletedDatabase.ResourceGroupName -ServerName $DeletedDatabase.ServerName -TargetDatabaseName "RestoredDatabase" –ResourceId $DeletedDatabase.ResourceID -Edition "Standard" -ServiceObjectiveName "S2"
```

## 将已删除的数据库还原为弹性数据库池

使用 [Get-AzureRmSqlDeletedDatabaseBackup](https://msdn.microsoft.com/zh-cn/library/azure/mt693387.aspx) cmdlet 获取要还原的已删除数据库备份。然后，使用 [Restore-AzureRmSqlDatabase](https://msdn.microsoft.com/zh-cn/library/azure/mt693390.aspx) cmdlet 从已删除的数据库备份开始还原。

```
$resourceGroupName = "resourcegroupname"
$sqlServerName = "servername"
$databaseName = "deletedDbToRestore"

$DeletedDatabase = Get-AzureRmSqlDeletedDatabaseBackup -ResourceGroupName $resourceGroupName -ServerName $sqlServerName -DatabaseName $databaseName

Restore-AzureRmSqlDatabase –FromDeletedDatabaseBackup –DeletionDate $DeletedDatabase.DeletionDate -ResourceGroupName $DeletedDatabase.ResourceGroupName -ServerName $DeletedDatabase.ServerName -TargetDatabaseName "RestoredDatabase" –ResourceId $DeletedDatabase.ResourceID –ElasticPoolName "elasticpool01"
```

## 后续步骤

- 有关业务连续性的概述和应用场景，请参阅[业务连续性概述](./sql-database-business-continuity.md)
- 若要了解 Azure SQL 数据库自动备份，请参阅 [SQL 数据库自动备份](./sql-database-automated-backups.md)
- 若要了解如何使用自动备份进行恢复，请参阅[从服务启动的备份中还原数据库](./sql-database-recovery-using-backups.md)
- 若要了解更快的恢复选项，请参阅[活动异地复制](./sql-database-geo-replication-overview.md)
- 若要了解如何使用自动备份进行存档，请参阅[数据库复制](./sql-database-copy.md)

<!---HONumber=Mooncake_Quality_Review_1215_2016-->