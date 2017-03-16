---
title: 使用 PowerShell 导入 BACPAC 文件以创建 Azure SQL 数据库 | Azure
description: 使用 PowerShell 导入 BACPAC 文件以创建 Azure SQL 数据库
services: sql-database
documentationCenter: ''
authors: stevestein
manager: jhubbard
editor: ''

ms.service: sql-database
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: data-management
ms.date: 08/31/2016
wacn.date: 12/19/2016
ms.author: sstein
---

# 使用 PowerShell 导入 BACPAC 文件以创建新的 Azure SQL 数据库

**单一数据库**

> [!div class="op_single_selector"]
- [PowerShell](./sql-database-import-powershell.md)
- [SSMS](./sql-database-cloud-migrate-compatible-import-bacpac-ssms.md)
- [SqlPackage](./sql-database-cloud-migrate-compatible-import-bacpac-sqlpackage.md)

本文说明如何使用 PowerShell 通过导入 [BACPAC](https://msdn.microsoft.com/zh-cn/library/ee210546.aspx#Anchor_4) 文件来创建 Azure SQL 数据库。

数据库通过从 Azure 存储 Blob 容器导入的 BACPAC 文件 (.bacpac) 创建。如果 Azure 存储中没有 BACPAC 文件，请参阅[使用 PowerShell 将 Azure SQL 数据库存档到 BACPAC 文件](./sql-database-export-powershell.md)。如果已有一个 BACPAC 文件但该文件不在 Azure 存储中，[使用 AzCopy 轻松将它上传到 Azure 存储帐户](../storage/storage-use-azcopy.md#blob-upload)。

> [!NOTE]
> Azure SQL 数据库会自动为你可以还原的每个用户数据库创建和维护备份。有关详细信息，请参阅 [SQL 数据库自动备份](./sql-database-automated-backups.md)。

若要导入 SQL 数据库，需要以下内容：

- Azure 订阅。如果你需要 Azure 订阅，只需单击本页顶部的“试用”，然后再回来完成本文的相关操作即可。
- 要导入的数据库的 BACPAC 文件。BACPAC 需位于 [Azure 存储帐户](../storage/storage-create-storage-account.md) Blob 容器中。

[!INCLUDE [启动 PowerShell 会话](../../includes/sql-database-powershell.md)]

## 设置适合环境的变量

有几个变量需要你将示例值替换为你的数据库和存储帐户的特定值。

服务器名称应是上一步骤选择的订阅中当前存在的服务器。它应该是要在其中创建数据库的服务器。不支持直接将数据库导入弹性池。但是可以先导入到单一数据库，然后将该数据库移入池中。

数据库名称是要为新数据库赋予的名称。

```
$ResourceGroupName = "resource group name"
$ServerName = "server name"
$DatabaseName = "database name"
```

以下变量来自 BACPAC 所处的存储帐户。在 [Azure 门户预览](https://portal.azure.cn)中，浏览到存储帐户获取这些值。你可以单击存储帐户边栏选项卡中的“所有设置”，然后单击“密钥”，找到主访问密钥。

Blob 名称是要从中创建数据库的现有 BACPAC 文件的名称。需要包括 .bacpac 扩展名。

```
$StorageName = "storageaccountname"
$StorageKeyType = "StorageAccessKey"
$StorageUri = "http://$StorageName.blob.core.chinacloudapi.cn/containerName/filename.bacpac"
$StorageKey = "primaryaccesskey"
```

运行 [Get-Credential](https://msdn.microsoft.com/zh-cn/library/hh849815.aspx) cmdlet 会打开一个窗口，要求输入用户名和密码。请输入 SQL 数据库服务器的管理员登录名和密码（上述 $ServerName），而不是 Azure 帐户的用户名和密码。

```
$credential = Get-Credential
```

## 导入数据库

此命令会将导入数据库请求提交到服务。根据数据库的大小，导入操作可能需要一些时间才能完成。

```
$importRequest = New-AzureRmSqlDatabaseImport –ResourceGroupName $ResourceGroupName –ServerName $ServerName –DatabaseName $DatabaseName –StorageKeytype $StorageKeyType –StorageKey $StorageKey -StorageUri $StorageUri –AdministratorLogin $credential.UserName –AdministratorLoginPassword $credential.Password –Edition Standard –ServiceObjectiveName S0 -DatabaseMaxSizeBytes 50000
```

## 监视导入操作的进度

运行 [New-AzureRmSqlDatabaseImport](https://msdn.microsoft.com/zh-cn/library/mt707793.aspx) 后，可运行 [Get-AzureRmSqlDatabaseImportExportStatus](https://msdn.microsoft.com/zh-cn/library/mt707794.aspx) 查看请求的状态。

```
Get-AzureRmSqlDatabaseImportExportStatus -OperationStatusLink $importRequest.OperationStatusLink
```

## SQL 数据库 PowerShell 导入脚本

```
$ResourceGroupName = "resourceGroupName"
$ServerName = "servername"
$DatabaseName = "databasename"

$StorageName = "storageaccountname"
$StorageKeyType = "StorageAccessKey"
$StorageUri = "http://$StorageName.blob.core.chinacloudapi.cn/containerName/filename.bacpac"
$StorageKey = "primaryaccesskey"

$credential = Get-Credential

$importRequest = New-AzureRmSqlDatabaseImport –ResourceGroupName $ResourceGroupName –ServerName $ServerName –DatabaseName $DatabaseName –StorageKeytype $StorageKeyType –StorageKey $StorageKey -StorageUri $StorageUri –AdministratorLogin $credential.UserName –AdministratorLoginPassword $credential.Password –Edition Standard –ServiceObjectiveName S0 -DatabaseMaxSizeBytes 50000

Get-AzureRmSqlDatabaseImportExportStatus -OperationStatusLink $importRequest.OperationStatusLink
```

## 后续步骤

- 若要了解如何连接到并查询导入的 SQL 数据库，请参阅[使用 SQL Server Management Studio 连接到 SQL 数据库并执行示例 T-SQL 查询](./sql-database-connect-query-ssms.md)

<!---HONumber=Mooncake_Quality_Review_1202_2016-->