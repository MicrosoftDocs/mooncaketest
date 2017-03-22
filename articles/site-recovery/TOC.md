# 概述
## [什么是 Site Recovery？](site-recovery-overview.md)
## [Site Recovery 的工作原理是什么？](site-recovery-components.md)
## [可以保护哪些工作负荷？](site-recovery-workload.md)
## [Site Recovery 支持矩阵](site-recovery-support-matrix.md)
## [常见问题](site-recovery-faq.md)
## [观看简介](https://www.youtube.com/watch?v=eOOwMQPBKfM)

# 入门
## [将 VMWare VM 复制到 Azure](site-recovery-vmware-to-azure.md)
## [在多租户部署 (CSP) 中将 VMware VM 复制到 Azure](site-recovery-multi-tenant-support-vmware-using-csp.md)
## [将 Hyper-V VM 复制到 Azure（不包含 VMM）](site-recovery-vmm-to-azure.md)
## [将 Hyper-V VM 复制到 Azure](site-recovery-hyper-v-site-to-azure.md)
## [将 VMware VM 和物理服务器复制到辅助站点](site-recovery-vmware-to-vmware.md)
## [将 Hyper-V VM 复制到辅助站点（包含 VMM）](site-recovery-vmm-to-vmm.md)

# 如何
## 计划
### [部署先决条件](site-recovery-prereq.md)
### [网络基础结构注意事项](site-recovery-network-design.md)
### [使用 Site Recovery Capacity Planner](site-recovery-capacity-planner.md)
### [规划容量以及缩放 VMware 在 Azure 中的复制](site-recovery-plan-capacity-vmware.md)
## 配置
### [设置源复制环境](site-recovery-set-up-vmware-to-azure.md)
### [配置复制设置](site-recovery-setup-replication-settings-vmware.md)
### [为 VMware 复制部署移动服务](site-recovery-vmware-to-azure-install-mob-svc.md)
#### [使用 System Center Configuration Manager 部署移动服务](site-recovery-install-mobility-service-using-sccm.md)
#### [使用 Azure Automation DSC 部署移动服务](site-recovery-automate-mobility-service-install.md)
### [删除服务器并禁用保护](site-recovery-manage-registration-and-protection.md)
## 迁移
### [迁移到 Azure](site-recovery-migrate-to-azure.md)
### [在 Azure 区域之间迁移](site-recovery-migrate-azure-to-azure.md)
### [将 AWS Windows 实例迁移到 Azure](site-recovery-migrate-aws-to-azure.md)
## 工作负荷
### [Active Directory 和 DNS](site-recovery-active-directory.md)
### [SQL Server](site-recovery-sql.md)
### [SharePoint](site-recovery-workload.md#protect-sharepoint)
### [Dynamics AX](site-recovery-workload.md#protect-dynamics-ax)
### [RDS](site-recovery-workload.md#protect-rds)
### [Exchange](site-recovery-workload.md#protect-exchange)
### [SAP](site-recovery-workload.md#protect-sap)
### [其他工作负荷](site-recovery-workload.md#workload-summary)
## 自动复制
### [自动将 Hyper-V 复制到 Azure（不包含 VMM）](site-recovery-deploy-with-powershell-resource-manager.md)
### [自动将 Hyper-V 复制到 Azure（包含 VMM）](site-recovery-vmm-to-azure-powershell-resource-manager.md)
### [自动将 Hyper-V 复制到辅助站点（包含 VMM）](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
## 故障转移和故障回复
### [Site Recovery 中的故障转移](site-recovery-failover.md)
### [设置恢复计划](site-recovery-create-recovery-plans.md)
#### [将 Azure Runbook 添加到恢复计划](site-recovery-runbook-automation.md)
### [运行从 VMware 到 Azure 的测试故障转移](site-recovery-test-failover-to-azure.md)
### [在两个 VMM 站点之间运行测试故障转移](site-recovery-test-failover-vmm-to-vmm.md)
### [对 VMware VM 和物理服务器进行故障回复](site-recovery-failback-azure-to-vmware.md)
## [监视和故障排除](site-recovery-monitoring-and-troubleshooting.md)

# 引用
## [PowerShell](/powershell/resourcemanager/azurerm.siterecovery/v3.2.0/azurerm.siterecovery)
## [PowerShell 经典](/powershell/servicemanagement/azure.siterecovery/v3.1.0/azure.siterecovery)
## [REST](https://msdn.microsoft.com/zh-cn/library/mt750497)

# 相关内容
## [Azure 自动化](/azure/automation/)

# 资源
## [学习路径](https://azure.microsoft.com/documentation/learning-paths/site-recovery/)
## [论坛](https://social.msdn.microsoft.com/Forums/azure/zh-cn/home?forum=hypervrecovmgr)
## [博客](http://azure.microsoft.com/blog/tag/azure-site-recovery/)
## [价格](https://azure.microsoft.com/pricing/details/site-recovery/)
## [服务更新](https://azure.microsoft.com/updates/?product=site-recovery)

<!---HONumber=Mooncake_0306_2017-->