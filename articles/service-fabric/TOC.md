# 概述
## [Service Fabric 是什么？](service-fabric-overview.md)
## [了解微服务](service-fabric-overview-microservices.md)
## [应用程序方案](service-fabric-application-scenarios.md)
## [体系结构](service-fabric-architecture.md)
## [术语](service-fabric-technical-overview.md)
## [内容路线图](service-fabric-content-roadmap.md)

# 入门
## 设置开发环境
### [Windows](service-fabric-get-started.md)
### [Linux](service-fabric-get-started-linux.md)
### [Mac OS](service-fabric-get-started-mac.md)
## 创建第一个应用程序
### [Windows 上的 C#](service-fabric-create-your-first-application-in-visual-studio.md)
### [Linux 上的 Java](service-fabric-create-your-first-linux-application-with-java.md)
### [Linux 上的 C#](service-fabric-create-your-first-linux-application-with-csharp.md)
## [在本地群集上部署应用](service-fabric-get-started-with-a-local-cluster.md)

# 如何
## 构建应用程序
### [模式和方案](service-fabric-patterns-and-scenarios.md)
### 基础知识
#### [应用程序模型](service-fabric-application-model.md)
#### [支持的编程模型](service-fabric-choose-framework.md)
#### [服务状态](service-fabric-concepts-state.md)
#### [服务通信](service-fabric-connect-and-communicate-with-services.md)
#### [添加 Web 前端](service-fabric-add-a-web-frontend.md)
#### [服务清单资源](service-fabric-service-manifest-resources.md)
#### [在 Visual Studio 中管理应用](service-fabric-manage-application-in-visual-studio.md)
#### [在 Visual Studio 中配置安全连接](service-fabric-visualstudio-configure-secure-connections.md)
#### 调试
##### [在 VS 中调试 C# 服务](service-fabric-debugging-your-application.md)
##### [在 Eclipse 中调试 Java 服务](service-fabric-debugging-your-application-java.md)
#### 监视和诊断
##### [Windows](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)
##### [Linux](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md)
#### [管理应用程序机密](service-fabric-application-secret-management.md)  
#### [为应用程序配置安全策略](service-fabric-application-runas-security.md)  
#### [为多个环境配置应用程序](service-fabric-manage-multiple-environment-app-configuration.md)  
#### [常见错误和异常](service-fabric-errors-and-exceptions.md) 

### 来宾可执行应用程序
#### [部署来宾可执行文件](service-fabric-deploy-existing-app.md)
#### [部署多个来宾可执行文件](service-fabric-deploy-multiple-apps.md)

### 容器应用程序
#### [概述](service-fabric-containers-overview.md)
#### [部署 Windows 容器](service-fabric-deploy-container.md)
#### [部署 Docker 容器](service-fabric-deploy-container-linux.md)

### Reliable Service 应用程序
#### [概述](service-fabric-reliable-services-introduction.md)
#### 入门
##### [Windows 上的 C#](service-fabric-reliable-services-quick-start.md)
##### [Linux 上的 Java](service-fabric-reliable-services-quick-start-java.md)
#### [体系结构](service-fabric-reliable-services-platform-architecture.md)
#### [Reliable Services 生命周期](service-fabric-reliable-services-lifecycle.md)
#### [可靠集合](service-fabric-reliable-services-reliable-collections.md)
#### [使用 Reliable Collections](service-fabric-work-with-reliable-collections.md)
#### [配置](service-fabric-reliable-services-configuration.md)
#### [通知](service-fabric-reliable-services-notifications.md)
#### [备份和还原](service-fabric-reliable-services-backup-restore.md)
#### [与 Reliable Services 通信](service-fabric-reliable-services-communication.md)
#### [通过 Reliable Services 进行安全通信](service-fabric-reliable-services-secure-communication.md)
##### [ASP.NET](service-fabric-reliable-services-communication-webapi.md)
##### [服务远程处理](service-fabric-reliable-services-communication-remoting.md)
##### [WCF](service-fabric-reliable-services-communication-wcf.md)
##### [反向代理](service-fabric-reverseproxy.md)
#### [高级用法](service-fabric-reliable-services-advanced-usage.md)

### Reliable Actor 应用程序
#### [概述](service-fabric-reliable-actors-introduction.md)
#### 入门
##### [Windows 上的 C#](service-fabric-reliable-actors-get-started.md)
##### [Linux 上的 Java](service-fabric-reliable-actors-get-started-java.md)
#### [体系结构](service-fabric-reliable-actors-platform.md)
#### [生命周期和垃圾回收](service-fabric-reliable-actors-lifecycle.md)
#### [多态性](service-fabric-reliable-actors-polymorphism.md)
#### [重新进入](service-fabric-reliable-actors-reentrancy.md)
#### [计时器和提醒](service-fabric-reliable-actors-timers-reminders.md)
#### [事件](service-fabric-reliable-actors-events.md)
#### [状态管理](service-fabric-reliable-actors-state-management.md)
#### [配置状态提供程序](service-fabric-reliable-actors-kvsactorstateprovider-configuration.md)
#### [类型序列化](service-fabric-reliable-actors-notes-on-actor-type-serialization.md)
#### [配置通信设置](service-fabric-reliable-actors-fabrictransportsettings.md) 

## 从云服务迁移
### [云服务与 Service Fabric 的比较](service-fabric-cloud-services-migration-differences.md)
### [迁移到 Service Fabric](service-fabric-cloud-services-migration-worker-role-stateless-service.md)

## 创建和管理群集

### 基础知识
#### [概述](service-fabric-deploy-anywhere.md)
#### [描述群集](service-fabric-cluster-resource-manager-cluster-description.md)
#### [容量规划](service-fabric-cluster-capacity.md)
#### [可视化群集](service-fabric-visualizing-your-cluster.md)
#### [连接到安全群集](service-fabric-connect-to-secure-cluster.md)
#### [使用 Azure CLI 管理群集](service-fabric-azure-cli.md) 
#### [保护群集](service-fabric-cluster-security.md)
#### [灾难恢复](service-fabric-disaster-recovery.md)

### Azure 上的群集
#### 在 Azure 上创建群集
##### [Azure 门户](service-fabric-cluster-creation-via-portal.md)
##### [Azure 资源管理器](service-fabric-cluster-creation-via-arm.md)
#### [节点类型和 VM 规模集](service-fabric-cluster-nodetypes.md)
#### [缩放群集](service-fabric-cluster-scale-up-down.md)
#### [升级群集](service-fabric-cluster-upgrade.md)
#### [删除群集](service-fabric-cluster-delete.md)
#### [访问控制](service-fabric-cluster-security-roles.md)
#### [配置群集](service-fabric-cluster-fabric-settings.md)
#### [使用证书保护群集](service-fabric-windows-cluster-x509-security.md)
#### [添加或滚动更新群集证书](service-fabric-cluster-security-update-certs-azure.md) 
#### [免费试用 Party 群集](http://aka.ms/tryservicefabric)

### 独立群集
#### [创建独立群集](service-fabric-cluster-creation-for-windows-server.md)
#### [在 Azure 虚拟机上创建独立群集](service-fabric-cluster-creation-with-windows-azure-vms.md)
#### [缩放群集](service-fabric-cluster-windows-server-add-remove-nodes.md)
#### [升级群集](service-fabric-cluster-upgrade-windows-server.md)
#### [访问控制](service-fabric-cluster-security-roles.md)
#### [配置群集](service-fabric-cluster-manifest.md)
#### [使用证书保护群集](service-fabric-windows-cluster-x509-security.md)  
#### [使用 Windows 安全性保护群集](service-fabric-windows-cluster-windows-security.md) 

## 管理应用程序生命周期
### [概述](service-fabric-application-lifecycle.md)
### [设置持续集成](service-fabric-set-up-continuous-integration.md)
### [了解 ImageStoreConnectionString 设置](service-fabric-image-store-connection-string.md)
### 部署或删除应用程序
#### [PowerShell](service-fabric-deploy-remove-applications.md)
#### [Visual Studio](service-fabric-publish-app-remote-cluster.md)
### [应用程序升级概述](service-fabric-application-upgrade.md)
### [配置应用程序升级](service-fabric-visualstudio-configure-upgrade.md)
### [应用程序升级参数](service-fabric-application-upgrade-parameters.md)
### 升级应用程序
#### [PowerShell](service-fabric-application-upgrade-tutorial-powershell.md)
#### [Visual Studio](service-fabric-application-upgrade-tutorial.md)
### [应用程序升级故障排除](service-fabric-application-upgrade-troubleshooting.md)
### [应用程序升级中的数据序列化](service-fabric-application-upgrade-data-serialization.md)
### [有关应用程序升级的高级主题](service-fabric-application-upgrade-advanced.md)

## 检查应用程序和群集运行状况
### [监视 Service Fabric 运行状况](service-fabric-health-introduction.md)
### [报告和检查服务运行状况](service-fabric-diagnostics-how-to-report-and-check-service-health.md)
### [添加自定义运行状况报告](service-fabric-report-health.md)
### [使用系统运行状况报告进行故障排除](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)
### [查看运行状况报告](service-fabric-view-entities-aggregated-health.md)

## 监视和诊断
### [监视和诊断应用程序](service-fabric-diagnostics-overview.md)
### 在本地监视和诊断服务
#### [Windows](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)
#### [Linux](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md)
### Azure 诊断日志
#### [Windows](service-fabric-diagnostics-how-to-setup-wad.md)
#### [Linux](service-fabric-diagnostics-how-to-setup-lad.md)
### [从服务进程收集日志](service-fabric-diagnostic-collect-logs-without-an-agent.md)
### [有状态 Reliable Services 中的诊断](service-fabric-reliable-services-diagnostics.md)
### [Reliable Actors 中的诊断](service-fabric-reliable-actors-diagnostics.md)
### [对本地群集进行故障排除](service-fabric-troubleshoot-local-cluster-setup.md)
### [排查常见问题](service-fabric-diagnostics-troubleshoot-common-scenarios.md)

## 缩放应用程序
### [Reliable Services 分区](service-fabric-concepts-partitioning.md)
### [服务的可用性](service-fabric-availability-services.md)
### [缩放应用程序](service-fabric-concepts-scalability.md)
### [规划应用程序的容量](service-fabric-capacity-planning.md)

## 测试应用程序和服务
### [故障分析概述](service-fabric-testability-overview.md)
### [测试服务间通信](service-fabric-testability-scenarios-service-communication.md)
### 模拟失败
#### [使用受控的混沌测试](service-fabric-controlled-chaos.md)
#### [使用测试操作](service-fabric-testability-actions.md)
#### [运行工作负荷期间](service-fabric-testability-workload-tests.md)
#### [调用数据丢失](service-fabric-use-data-loss-api.md)
#### [使用测试方案](service-fabric-testability-scenarios.md)
#### [使用节点转换 API](service-fabric-node-transition-apis.md)
### [对应用程序进行负载测试](service-fabric-vso-load-test.md)

## 管理和协调群集资源
### [群集资源管理器概述](service-fabric-cluster-resource-manager-introduction.md)
### [群集资源管理器体系结构](service-fabric-cluster-resource-manager-architecture.md)
### [描述群集](service-fabric-cluster-resource-manager-cluster-description.md)
### [应用程序组概述](service-fabric-cluster-resource-manager-application-groups.md)
### [配置群集资源管理器设置](service-fabric-cluster-resource-manager-configure-services.md)
### [资源消耗指标](service-fabric-cluster-resource-manager-metrics.md)
### [使用服务相关性](service-fabric-cluster-resource-manager-advanced-placement-rules-affinity.md)
### [服务放置策略](service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies.md)
### [管理群集](service-fabric-cluster-resource-manager-management-integration.md)
### [群集重整](service-fabric-cluster-resource-manager-defragmentation-metrics.md)
### [均衡群集](service-fabric-cluster-resource-manager-balancing.md)
### [限制](service-fabric-cluster-resource-manager-advanced-throttling.md)
### [服务移动](service-fabric-cluster-resource-manager-movement-cost.md)

# 引用
## [PowerShell](//powershell/servicefabric/vlatest/servicefabric)
## [Java API](/java/api/microsoft.servicefabric.services)
## [.NET](/dotnet/api/microsoft.servicefabric.services)
## [REST](/rest/api/servicefabric)

# 资源
## [有关 Service Fabric 的常见问题](service-fabric-common-questions.md)
## [Service Fabric 支持选项](service-fabric-support.md)
## [代码示例](http://aka.ms/servicefabricsamples)
## [学习路径](https://azure.microsoft.com/documentation/learning-paths/service-fabric/)
## [价格](https://azure.microsoft.com/pricing/details/service-fabric/)
## [服务更新](https://azure.microsoft.com/updates/?product=service-fabric)
## [MSDN 论坛](https://social.msdn.microsoft.com/Forums/home?forum=AzureServiceFabric)
## [视频](https://azure.microsoft.com/documentation/videos/index/?services=service-fabric)

<!---HONumber=Mooncake_0227_2017-->