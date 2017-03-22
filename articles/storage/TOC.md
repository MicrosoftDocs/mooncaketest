# 概述

## [介绍](storage-introduction.md)

# 入门

## [快速入门指南](storage-getting-started-guide.md)
## [创建存储帐户](storage-create-storage-account.md)

## Blob 存储
### [.NET](storage-dotnet-how-to-use-blobs.md)
### [Java](storage-java-how-to-use-blob-storage.md)
### [Node.js](storage-nodejs-how-to-use-blob-storage.md)
### [C++](storage-c-plus-plus-how-to-use-blobs.md)
### [Python](storage-python-how-to-use-blob-storage.md)
### [PHP](storage-php-how-to-use-blobs.md)
### [Ruby](storage-ruby-how-to-use-blob-storage.md)
### [iOS](storage-ios-how-to-use-blob-storage.md)
### [Xamarin](storage-xamarin-blob-storage.md)

## 队列存储
### [.NET](storage-dotnet-how-to-use-queues.md)
### [Java](storage-java-how-to-use-queue-storage.md)
### [Node.js](storage-nodejs-how-to-use-queues.md)
### [C++](storage-c-plus-plus-how-to-use-queues.md)
### [Python](storage-python-how-to-use-queue-storage.md)
### [PHP](storage-php-how-to-use-queues.md)
### [Ruby](storage-ruby-how-to-use-queue-storage.md)

## 表存储
### [.NET](storage-dotnet-how-to-use-tables.md)
### [Java](storage-java-how-to-use-table-storage.md)
### [Node.js](storage-nodejs-how-to-use-table-storage.md)
### [C++](storage-c-plus-plus-how-to-use-tables.md)
### [Python](storage-python-how-to-use-table-storage.md)
### [PHP](storage-php-how-to-use-table-storage.md)
### [Ruby](storage-ruby-how-to-use-table-storage.md)

## 文件存储
### [Windows、.NET、PowerShell](storage-dotnet-how-to-use-files.md)
### [Linux](storage-how-to-use-files-linux.md)
### [Java](storage-java-how-to-use-file-storage.md)
### [C++](storage-c-plus-plus-how-to-use-files.md)
### [Python](storage-python-how-to-use-file-storage.md)

## 磁盘存储 
### [使用 Resource Manager 和 PowerShell 创建 VM](../virtual-machines/virtual-machines-windows-ps-create.md)
### [使用 Azure CLI 2.0（预览版）创建 Linux VM](../virtual-machines/virtual-machines-linux-quick-create-cli.md)
### [使用 PowerShell 将托管磁盘附加到 Windows VM](../virtual-machines/virtual-machines-windows-attach-disk-ps.md)
### [将托管磁盘添加到 Linux VM](../virtual-machines/virtual-machines-linux-add-disk.md)
### [使用 Windows 中的快照创建作为托管磁盘存储的 VHD 的副本](../virtual-machines/virtual-machines-windows-snapshot-copy-managed-disk.md)
### [使用 Linux 中的快照创建作为托管磁盘存储的 VHD 的副本](../virtual-machines/linux/virtual-machines-linux-snapshot-copy-managed-disk.md)

# 如何
## [创建存储帐户](storage-create-storage-account.md)
## 使用 Blob
### [服务概述](https://msdn.microsoft.com/library/dd179376.aspx)
### [“冷”层和“热”层](storage-blob-storage-tiers.md)
### [自定义域](storage-custom-domain-name.md)
### [匿名访问 Blob](storage-manage-access-to-resources.md)
### [示例](https://azure.microsoft.com/documentation/samples/?service=storage&term=blob)
## 使用队列
### [概念](https://msdn.microsoft.com/library/dd179353.aspx)
### [示例](https://azure.microsoft.com/documentation/samples/?service=storage&term=queue)
## 使用表
### [概述](https://msdn.microsoft.com/library/dd179463.aspx)
### [表设计指南](storage-table-design-guide.md)
### [示例](https://azure.microsoft.com/documentation/samples/?service=storage&term=table)
## 使用文件
### [概述](/rest/api/storageservices/fileservices/File-Service-Concepts)
### [排查 Azure 文件问题](storage-troubleshoot-file-connection-problems.md)
### [示例](https://azure.microsoft.com/documentation/samples/?service=storage&term=file)
## 使用磁盘
### [Windows VM 的磁盘和 VHD](storage-about-disks-and-vhds-windows.md)
### [Linux VM 的磁盘和 VHD](storage-about-disks-and-vhds-linux.md)
### [Azure 托管磁盘概述](storage-managed-disks-overview.md)
### [将 Azure VM 迁移到 Azure 托管磁盘](../virtual-machines/virtual-machines-windows-migrate-to-managed-disks.md)
### [从 AWS 和其他平台迁移到托管磁盘](../virtual-machines/virtual-machines-windows-on-prem-to-azure.md)
### [有关 Azure IaaS VM 磁盘的常见问题](storage-faq-for-disks.md)
### 高级存储
#### [适用于 VM 磁盘的高性能高级存储](storage-premium-storage.md)
#### [高性能设计](storage-premium-storage-performance.md)
### 标准存储
#### [高性价比标准存储以及非托管和托管 VM 磁盘](storage-standard-storage.md)
### 使用非托管磁盘
#### [迁移到高级存储](storage-migration-to-premium-storage.md)
#### [通过递增快照备份非托管 VM 磁盘](storage-incremental-snapshots.md)
## 规划和设计
### [复制](storage-redundancy.md)
### [可伸缩性和性能目标](storage-scalability-targets.md)
### [性能和可缩放性清单](storage-performance-checklist.md)
### [并发](storage-concurrency.md)
## 开发
### 示例
#### [.NET](storage-samples-dotnet.md)
#### [Java](storage-samples-java.md)
### [使用 RA-GRS 设计 HA 应用](storage-designing-ha-apps-with-ragrs.md)
### [配置连接字符串](storage-configure-connection-string.md)
### [使用存储模拟器](storage-use-emulator.md)
### [设置和检索属性及元数据](storage-properties-metadata.md)
## 管理
### [PowerShell](storage-powershell-guide-full.md)
### [Azure CLI 2.0（预览版）](storage-azure-cli.md)
### [Azure CLI 1.0](storage-azure-cli-nodejs.md)
### [Azure 自动化](automation-manage-storage.md)
## 安全
### [安全指南](storage-security-guide.md)
### [静态数据加密](storage-service-encryption.md)
### [共享密钥身份验证](https://msdn.microsoft.com/library/dd179428.aspx)
### [共享访问签名 (SAS)](storage-dotnet-shared-access-signature-part-1.md)
### [教程：使用 Azure 密钥保管库加密和解密 Blob](storage-encrypt-decrypt-blobs-key-vault.md)
### 客户端加密
#### [.NET](storage-client-side-encryption.md)
#### [Java](storage-client-side-encryption-java.md)
#### [Python](storage-client-side-encryption-python.md)
## 监视和故障排除
### 指标和日志记录
#### [存储分析](storage-analytics.md)
#### [启用和查看指标](storage-enable-and-view-metrics.md)
#### [监视、诊断和故障排除](storage-monitoring-diagnosing-troubleshooting.md)
#### [故障排除教程](storage-e2e-troubleshooting.md)
### 排查磁盘删除错误
#### [在 Resource Manager 部署中](storage-resource-manager-cannot-delete-storage-account-container-vhd.md)
#### [在经典部署中](storage-cannot-delete-storage-account-container-vhd.md)
### [排查文件存储问题](storage-troubleshoot-file-connection-problems.md)
### [灾难恢复指南](storage-disaster-recovery-guidance.md)
## 传输数据
### [向/从存储器移动数据](storage-moving-data.md)
### [AzCopy 命令行实用工具](storage-use-azcopy.md)
### [使用导入/导出服务](storage-import-export-service.md)
### [使用导入/导出工具](storage-import-export-tool-how-to.md)
#### [设置导入/导出工具](storage-import-export-tool-setup.md)
#### [为导入作业准备硬盘驱动器](storage-import-export-tool-preparing-hard-drives-import.md)
##### [在导入过程中设置属性和元数据](storage-import-export-tool-setting-properties-metadata-import.md)
##### [为导入作业准备硬盘驱动器的示例工作流](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow.md)
##### [导入作业的常用命令快速参考](storage-import-export-tool-quick-reference.md)
#### [预览导出作业的驱动器使用情况](storage-import-export-tool-previewing-drive-usage-export-v1.md)
#### [使用复制日志文件查看作业状态](storage-import-export-tool-reviewing-job-status-v1.md)
#### [修复导入作业](storage-import-export-tool-repairing-an-import-job-v1.md)
#### [修复导出作业](storage-import-export-tool-repairing-an-export-job-v1.md)
#### [排查导入/导出工具问题](storage-import-export-tool-troubleshooting-v1.md)
#### [导入/导出服务清单文件格式](storage-import-export-file-format-manifest.md)
#### [导入/导出服务元数据和属性文件格式](storage-import-export-file-format-metadata-and-properties.md)
#### [导入/导出服务日志文件格式](storage-import-export-file-format-log.md)
### [使用导入/导出工具 (v1)](storage-import-export-tool-how-to-v1.md)
#### [设置导入/导出工具](storage-import-export-tool-setup-v1.md)
#### [为导入作业准备硬盘驱动器](storage-import-export-tool-preparing-hard-drives-import-v1.md)
##### [在导入过程中设置属性和元数据](storage-import-export-tool-setting-properties-metadata-import-v1.md)
##### [为导入作业准备硬盘驱动器的示例工作流](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow-v1.md)
##### [导入作业的常用命令快速参考](storage-import-export-tool-quick-reference-v1.md)
#### [预览导出作业的驱动器使用情况](storage-import-export-tool-previewing-drive-usage-export-v1.md)
#### [使用复制日志文件查看作业状态](storage-import-export-tool-reviewing-job-status-v1.md)
#### [修复导入作业](storage-import-export-tool-repairing-an-import-job-v1.md)
#### [修复导出作业](storage-import-export-tool-repairing-an-export-job-v1.md)
#### [排查导入/导出工具问题](storage-import-export-tool-troubleshooting-v1.md)
#### [导入/导出服务清单文件格式](storage-import-export-file-format-manifest.md)
#### [导入/导出服务元数据和属性文件格式](storage-import-export-file-format-metadata-and-properties.md)
#### [导入/导出服务日志文件格式](storage-import-export-file-format-log.md)
### [使用 Azure 导入/导出服务 REST API](storage-import-export-using-the-rest-api.md)
#### [创建导入作业](storage-import-export-creating-an-import-job.md)
#### [创建导出作业](storage-import-export-creating-an-export-job.md)
#### [检索作业的状态信息](storage-import-export-retrieving-state-info-for-a-job.md)
#### [枚举作业](storage-import-export-enumerating-jobs.md)
#### [取消和删除作业](storage-import-export-cancelling-and-deleting-jobs.md)
#### [备份驱动器清单](storage-import-export-backing-up-drive-manifests.md)
#### [导入/导出作业的诊断和错误恢复](storage-import-export-diagnostics-and-error-recovery.md)
# 参考
## [PowerShell](/powershell/storage)
## [Azure CLI](/cli/azure/storage)
## .NET
### [资源管理器](/dotnet/api/microsoft.azure.management.storage)
### [数据移动](https://msdn.microsoft.com/library/azure/mt684990.aspx)
### [Blob、队列、表和文件](https://msdn.microsoft.com/library/azure/mt347887.aspx)
## [Java](http://azure.github.io/azure-storage-java/)
## [Node.js](http://azure.github.io/azure-storage-node)
## [Ruby](http://azure.github.io/azure-storage-ruby)
## [Python](https://azure-storage.readthedocs.io/en/latest/index.html)
## [C++](http://azure.github.io/azure-storage-cpp)
## [iOS](http://azure.github.io/azure-storage-ios/)
## [Android](http://azure.github.io/azure-storage-android)
## REST
### [Blob、队列、表和文件](/rest/api/storageservices/fileservices/azure-storage-services-rest-api-reference)
### [资源提供程序](/rest/api/storagerp)
### [导入/导出](/rest/api/storageimportexport)

# 相关内容
## 经典门户
### [创建存储帐户](storage-create-storage-account-classic-portal.md)
### [启用和查看指标](storage-enable-and-view-metrics-classic-portal.md)
### [监视、诊断和故障排除](storage-monitoring-diagnosing-troubleshooting-classic-portal.md)
### [故障排除教程](storage-e2e-troubleshooting-classic-portal.md)

# 资源
## [价格](https://azure.microsoft.com/pricing/details/storage/blobs/)
## [Azure 存储客户端工具](storage-explorers.md)
## [堆栈溢出](http://stackoverflow.com/questions/tagged/windows-azure-storage)
## [论坛](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata)
## [服务更新](https://azure.microsoft.com/updates/?product=storage)
## [视频](https://azure.microsoft.com/documentation/videos/index/?services=storage)

## Azure 存储空间资源管理器
### [存储资源管理器（预览版）](../vs-azure-tools-storage-manage-with-storage-explorer.md)
### [使用存储资源管理器（预览版）管理 Blob](../vs-azure-tools-storage-explorer-blobs.md)

## NuGet 包
### [适用于 .NET 的 Azure 存储空间客户端库](https://www.nuget.org/packages/WindowsAzure.Storage/)
### [Azure 存储数据移动库](https://www.nuget.org/packages/Microsoft.Azure.Storage.DataMovement/)
### [Azure 配置管理器](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)

## 源代码
### .NET
#### [Blob、队列、表和文件](https://github.com/Azure/azure-storage-net)
#### [数据移动](https://github.com/Azure/azure-storage-net-data-movement)
#### [资源提供程序](https://github.com/Azure/azure-sdk-for-net)
### [Node.js](http://azure.github.io/azure-storage-node/)
### [Java](https://github.com/Azure/azure-storage-java)
### [C++](https://github.com/Azure/azure-storage-cpp)
### [PHP](https://github.com/Azure/azure-storage-php)
### [Ruby](https://github.com/Azure/azure-storage-ruby)
### [Python](https://github.com/Azure/azure-storage-python)
### [iOS](https://github.com/Azure/azure-storage-ios)

<!---HONumber=Mooncake_0313_2017-->