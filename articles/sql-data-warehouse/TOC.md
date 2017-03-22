# 概述

## [什么是 SQL 数据仓库？](sql-data-warehouse-overview-what-is.md)
## [数据仓库工作负荷](sql-data-warehouse-overview-workload.md)
## [分布式数据](sql-data-warehouse-distributed-data.md)

# 入门

## [初级教程](sql-data-warehouse-get-started-tutorial.md)
## [最佳实践](sql-data-warehouse-best-practices.md)
## [管理](sql-data-warehouse-overview-manage.md)
## [获取支持](sql-data-warehouse-get-started-create-support-ticket.md)

# 如何

## 备份和还原

### [备份概述](sql-data-warehouse-backups.md)
### [还原概述](sql-data-warehouse-restore-database-overview.md)
#### [Azure 门户](sql-data-warehouse-restore-database-portal.md)
#### [PowerShell](sql-data-warehouse-restore-database-powershell.md)
#### [REST](sql-data-warehouse-restore-database-rest-api.md)

## 连接

### [概述](sql-data-warehouse-connect-overview.md)
### [连接字符串](sql-data-warehouse-connection-strings.md)
### [sqlcmd](sql-data-warehouse-get-started-connect-sqlcmd.md)
### [SSMS](sql-data-warehouse-query-ssms.md)
### [Visual Studio](sql-data-warehouse-query-visual-studio.md)
### [安装 Visual Studio](sql-data-warehouse-install-visual-studio.md)

## 创建
### [Azure 门户](sql-data-warehouse-get-started-provision.md)
### [PowerShell](sql-data-warehouse-get-started-provision-powershell.md)
### [T-SQL](sql-data-warehouse-get-started-create-database-tsql.md)

## 开发

### [概述](sql-data-warehouse-overview-develop.md)

### 表

#### [概述](sql-data-warehouse-tables-overview.md)
#### [CTAS](sql-data-warehouse-develop-ctas.md)
#### [数据类型](sql-data-warehouse-tables-data-types.md)
#### [分布式表](sql-data-warehouse-tables-distribute.md)
#### [索引](sql-data-warehouse-tables-index.md)
#### [分区](sql-data-warehouse-tables-partition.md)
#### [统计信息](sql-data-warehouse-tables-statistics.md)
#### [临时](sql-data-warehouse-tables-temporary.md)

### 查询

#### [动态 SQL](sql-data-warehouse-develop-dynamic-sql.md)
#### [Group By 选项](sql-data-warehouse-develop-group-by-options.md)
#### [标签](sql-data-warehouse-develop-label.md)

### T-SQL 语言元素

#### [循环](sql-data-warehouse-develop-loops.md)
#### [存储过程](sql-data-warehouse-develop-stored-procedures.md)
#### [事务](sql-data-warehouse-develop-transactions.md)
#### [事务最佳实践](sql-data-warehouse-develop-best-practices-transactions.md)
#### [用户定义的架构](sql-data-warehouse-develop-user-defined-schemas.md)
#### [变量赋值](sql-data-warehouse-develop-variable-assignment.md)
#### [视图](sql-data-warehouse-develop-views.md)

## 集成

### [概述](sql-data-warehouse-overview-integrate.md)
### [数据工厂](sql-data-warehouse-integrate-azure-data-factory.md)
### [机器学习](sql-data-warehouse-integrate-azure-machine-learning.md)
### [机器学习教程](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
### [Power BI](sql-data-warehouse-integrate-power-bi.md)
### [Power BI 可视化](sql-data-warehouse-get-started-visualize-with-power-bi.md)
### [流分析](sql-data-warehouse-integrate-azure-stream-analytics.md)

## 加载

### [概述](sql-data-warehouse-overview-load.md)
### [样本数据](sql-data-warehouse-load-sample-databases.md)
### [Azure Data Lake Store ](sql-data-warehouse-load-from-azure-data-lake-store.md)
### [AZCopy](sql-data-warehouse-load-from-sql-server-with-azcopy.md)
### [BCP](sql-data-warehouse-load-with-bcp.md)
### [从 SQL Server 使用 BCP](sql-data-warehouse-load-from-sql-server-with-bcp.md)
### [数据工厂](sql-data-warehouse-load-with-data-factory.md)
### [PolyBase](sql-data-warehouse-get-started-load-with-polybase.md)
### [PolyBase 指南](sql-data-warehouse-load-polybase-guide.md)
### [从 Blob 存储使用 PolyBase](sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md)
### [从 SQL Server 使用 PolyBase](sql-data-warehouse-load-from-sql-server-with-polybase.md)
### [RedGate](sql-data-warehouse-load-with-redgate.md)
### [SSIS](sql-data-warehouse-load-from-sql-server-with-integration-services.md)

## 迁移

### [概述](sql-data-warehouse-overview-migrate.md)
### [迁移实用工具](sql-data-warehouse-migrate-migration-utility.md)
### [迁移架构](sql-data-warehouse-migrate-schema.md)
### [迁移代码](sql-data-warehouse-migrate-code.md)
### [迁移数据](sql-data-warehouse-migrate-data.md)
### [迁移到高级存储](sql-data-warehouse-migrate-to-premium-storage.md)

## 暂停和缩放

### [概述](sql-data-warehouse-manage-compute-overview.md)
### [Azure 门户](sql-data-warehouse-manage-compute-portal.md)
### [PowerShell](sql-data-warehouse-manage-compute-powershell.md)
### [REST API](sql-data-warehouse-manage-compute-rest-api.md)
### [T-SQL](sql-data-warehouse-manage-compute-tsql.md)

## 性能

### [概述](sql-data-warehouse-overview-manage-user-queries.md)
### [列存储压缩](sql-data-warehouse-memory-optimizations-for-columnstore-compression.md)
### [查询](sql-data-warehouse-manage-monitor.md)
### [工作符合](sql-data-warehouse-develop-concurrency.md)
### [故障排除](sql-data-warehouse-troubleshoot.md)

## “安全”

### [概述](sql-data-warehouse-overview-manage-security.md)
### [审核](sql-data-warehouse-auditing-overview.md)
### [下层客户端审核](sql-data-warehouse-auditing-downlevel-clients.md)
### [身份验证](sql-data-warehouse-authentication.md)
### [加密](sql-data-warehouse-encryption-tde.md)
### [使用 T-SQL 加密](sql-data-warehouse-encryption-tde-tsql.md)
### [威胁检测](sql-data-warehouse-security-threat-detection.md)

# 引用

## [容量限制](sql-data-warehouse-service-capacity-limits.md)
## [T-SQL 语言元素](sql-data-warehouse-reference-tsql-language-elements.md)
## [T-SQL 语句](sql-data-warehouse-reference-tsql-statements.md)
## [T-SQL 系统视图](sql-data-warehouse-reference-tsql-system-views.md)
## [PowerShell cmdlet](sql-data-warehouse-reference-powershell-cmdlets.md)

# 资源
## [价格](https://azure.microsoft.com/pricing/details/sql-data-warehouse/)
## [堆栈溢出](https://stackoverflow.com/questions/tagged/azure-sqldw/)
## [服务更新](https://azure.microsoft.com/updates/?product=sql-data-warehouse)
## [论坛](https://social.msdn.microsoft.com/Forums/home?forum=AzureSQLDataWarehouse)
## [视频](https://azure.microsoft.com/documentation/videos/index/?services=sql-data-warehouse)

## 合作伙伴
### [商业智能](sql-data-warehouse-partner-business-intelligence.md)
### [数据集成](sql-data-warehouse-partner-data-integration.md)
### [数据管理](sql-data-warehouse-partner-data-management.md)

<!---HONumber=Mooncake_0313_2017-->