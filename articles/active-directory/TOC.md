# 概述
## [什么是 Azure Active Directory？](active-directory-whatis.md)
## [选择版本](active-directory-editions.md)
## [关于 Azure 标识管理](fundamentals-identity.md)
## [预览 Azure 门户体验](active-directory-preview-explainer.md)


# 入门
## [获取 Azure AD 租户](active-directory-howto-tenant.md)
## [注册 Azure AD Premium](active-directory-get-started-premium.md)
## [关联 Azure 订阅](active-directory-how-subscriptions-associated-directory.md)
## [管理 AD 许可](active-directory-licensing-what-is.md)
## [为组织获取 Azure](sign-up-organization.md)
## [常见问题](active-directory-faq.md)
## [SaaS 应用教程](active-directory-saas-tutorial-list.md)

# 如何
## 管理用户
### 添加用户
#### [Azure 门户](active-directory-users-create-azure-portal.md)
#### [经典门户](active-directory-create-users.md)

### 从其他目录添加用户
#### [Azure 门户](active-directory-users-create-external-azure-portal.md)
#### [经典门户](active-directory-create-users-external.md)

### [删除用户](active-directory-users-delete-user-azure-portal.md)
### [管理用户个人资料](active-directory-users-profile-azure-portal.md)
### [重置密码](active-directory-users-reset-password-azure-portal.md)
### [管理用户工作信息](active-directory-users-work-info-azure-portal.md)
### [共享帐户](active-directory-sharing-accounts.md)

## [管理组和成员](active-directory-manage-groups.md)
### 管理组
#### [Azure 门户](active-directory-groups-create-azure-portal.md)
#### [经典门户](active-directory-accessmanagement-manage-groups.md)
#### [Powershell](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
### [管理组成员](active-directory-groups-members-azure-portal.md)
### [管理组所有者](active-directory-accessmanagement-managing-group-owners.md)
### [管理组成员身份](active-directory-groups-membership-azure-portal.md)
### [查看所有组](active-directory-groups-view-azure-portal.md)
### [启用专用组](active-directory-accessmanagement-dedicated-groups.md)
### [添加对 SaaS 应用的组访问权限](active-directory-accessmanagement-group-saasapps.md)
### 管理组设置
#### [Azure 门户](active-directory-groups-settings-azure-portal.md)
#### [Cmdlet](active-directory-accessmanagement-groups-settings-cmdlets.md)
### 创建高级规则
#### [Azure 门户](active-directory-groups-dynamic-membership-azure-portal.md)
#### [经典门户](active-directory-accessmanagement-groups-with-advanced-rules.md)
### [设置自助服务组](active-directory-accessmanagement-self-service-group-management.md)
### [故障排除](active-directory-accessmanagement-troubleshooting.md)

## [查看访问和使用情况报告](active-directory-view-access-usage-reports.md)
### [Azure AD 报告](active-directory-reporting-getting-started.md)
### [已知网络](active-directory-known-networks.md)

### [报告指南](active-directory-reporting-guide.md)
#### [预览](active-directory-reporting-azure-portal.md)
#### [API](active-directory-reporting-api-getting-started.md)
##### [审核参考](active-directory-reporting-api-audit-reference.md)
##### [审核示例](active-directory-reporting-api-audit-samples.md)
##### [先决条件](active-directory-reporting-api-prerequisites.md)
##### [登录参考](active-directory-reporting-api-sign-in-activity-reference.md)
##### [登录示例](active-directory-reporting-api-sign-in-activity-samples.md)


#### [审核事件](active-directory-reporting-audit-events.md)
#### [保留期](active-directory-reporting-retention.md)
#### [延迟](active-directory-reporting-latencies.md)
#### [通知](active-directory-reporting-notifications.md)
### 了解报告
#### [异常登录](active-directory-reporting-irregular-sign-in-activity.md)
#### [多次失败](active-directory-reporting-sign-ins-after-multiple-failures.md)
#### [可疑的 IP 地址](active-directory-reporting-sign-ins-from-ip-addresses-with-suspicious-activity.md)
#### [多个地理区域](active-directory-reporting-sign-ins-from-multiple-geographies.md)
#### [可能受感染的设备](active-directory-reporting-sign-ins-from-possibly-infected-devices.md)
#### [未知源](active-directory-reporting-sign-ins-from-unknown-sources.md)
#### [异常登录](active-directory-reporting-users-with-anomalous-sign-in-activity.md)

## [管理密码](active-directory-manage-passwords.md)
### [更新自己的密码](active-directory-passwords-update-your-own-password.md)
### [了解密码管理](active-directory-passwords-how-it-works.md)
### [了解策略和限制](active-directory-passwords-policy.md)
### 重置密码
#### [Azure 门户](active-directory-users-reset-password-azure-portal.md)
#### [经典门户](active-directory-create-users-reset-password.md)
### [设置过期策略](active-directory-passwords-set-expiration-policy.md)
### 启用密码管理
#### [入门](active-directory-passwords-getting-started.md)
#### [部署](active-directory-passwords-best-practices.md)
#### [设置自助密码重置](active-directory-passwords.md)
#### [自定义](active-directory-passwords-customize.md)
#### [查看报告](active-directory-passwords-get-insights.md)
#### [了解详细信息](active-directory-passwords-learn-more.md)
#### [常见问题](active-directory-passwords-faq.md)
#### [故障排除](active-directory-passwords-troubleshoot.md)

## 管理设备
### [注册设备](active-directory-azureadjoin-personal-device.md)
### [注册 Windows 10 设备](active-directory-azureadjoin-user-upgrade.md)

### [条件性访问](active-directory-conditional-access.md)
#### [入门](active-directory-conditional-access-azuread-connected-apps.md)
#### [支持的应用](active-directory-conditional-access-supported-apps.md)
#### [注册设备](active-directory-conditional-access-device-registration-overview.md)
#### [管理自动注册](active-directory-conditional-access-automatic-device-registration.md)
##### [设置](active-directory-conditional-access-automatic-device-registration-setup.md)
##### [Windows 7](active-directory-conditional-access-automatic-device-registration-windows7.md)
##### [Windows 8.1](active-directory-conditional-access-automatic-device-registration-windows-8-1.md)
#### [管理验证器应用](active-directory-conditional-access-azure-authenticator-app.md)
#### [了解设备策略](active-directory-conditional-access-device-policies.md)
#### [设置对连接的应用的访问](active-directory-conditional-access-policy-connected-applications.md)
#### [本地部署](active-directory-conditional-access-on-premises-setup.md)
#### [常见问题](active-directory-conditional-faqs.md)
#### [故障排除](active-directory-conditional-access-device-remediation.md)
#### [引用](active-directory-conditional-access-technical-reference.md)

### [Azure AD 加入](active-directory-azureadjoin-overview.md)
#### [计划](active-directory-azureadjoin-deployment-aadjoindirect.md)
#### [设置设备注册](active-directory-azureadjoin-setup.md)
#### [注册新设备](active-directory-azureadjoin-user-frx.md)
#### [部署](active-directory-azureadjoin-devices-group-policy.md)
#### [不使用密码进行身份验证](active-directory-azureadjoin-passport.md)
#### [启用 Windows Hello for Business](active-directory-azureadjoin-passport-deployment.md)
#### [了解 Windows 10 集成](active-directory-azureadjoin-windows10-devices-overview.md)
#### [使用 Windows 10 设备](active-directory-azureadjoin-windows10-devices.md)

### 基于证书的身份验证
#### [Android](active-directory-certificate-based-authentication-android.md)
#### [iOS](active-directory-certificate-based-authentication-ios.md)

## 管理应用
### [概述](active-directory-enable-sso-scenario.md)
### [入门](active-directory-integrating-applications-getting-started.md)

### [Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md)
#### [更新注册表设置](active-directory-cloudappdiscovery-registry-settings-for-proxy-services.md)
#### [了解安全性和隐私性](active-directory-cloudappdiscovery-security-and-privacy-considerations.md)

### [授予应用的远程访问权限](active-directory-application-proxy-get-started.md)
#### [启用应用代理](active-directory-application-proxy-enable.md)
#### 发布应用
##### [Azure 门户](application-proxy-publish-azure-portal.md)
##### [经典门户](active-directory-application-proxy-publish.md)
#### 在独立网络上发布
##### [Azure 门户](active-directory-application-proxy-connectors-azure-portal.md)
##### [经典门户](active-directory-application-proxy-connectors.md)
#### [自定义域](active-directory-application-proxy-custom-domains.md)
#### [单一登录](active-directory-application-proxy-sso-using-kcd.md)
##### [Azure 门户](application-proxy-sso-azure-portal.md)
#### [声明感知的应用](active-directory-application-proxy-claims-aware-apps.md)
#### [本机客户端应用](active-directory-application-proxy-native-client.md)
#### [条件性访问](active-directory-application-proxy-conditional-access.md)
#### [无提示安装](active-directory-application-proxy-silent-installation.md)
#### [故障排除](active-directory-application-proxy-troubleshoot.md)
### [了解应用 SSO](active-directory-appssoaccess-whatis.md)

### 集成 SaaS 应用
#### [Azure 门户](active-directory-enterprise-apps-manage-sso.md)
#### [经典门户](active-directory-sso-integrate-saas-apps.md)

### 管理企业应用
#### [分配用户](active-directory-coreapps-assign-user-azure-portal.md)
#### [自定义品牌](active-directory-coreapps-change-app-logo-user-azure-portal.md)
#### [禁用用户登录](active-directory-coreapps-disable-app-azure-portal.md)
#### [删除用户](active-directory-coreapps-remove-assignment-azure-portal.md)
#### [查看我的所有应用](active-directory-coreapps-view-azure-portal.md)
#### [管理用户帐户预配](active-directory-enterprise-apps-manage-provisioning.md)

### 开发
#### [分配用户](active-directory-applications-guiding-developers-assigning-users.md)
#### [分配组](active-directory-applications-guiding-developers-assigning-groups.md)
#### [需要分配](active-directory-applications-guiding-developers-requiring-user-assignment.md)
#### [开发 LoB 应用](active-directory-applications-guiding-developers-for-lob-applications.md)

### [管理对应用的访问](active-directory-managing-access-to-apps.md)
#### [自助访问](active-directory-self-service-application-access.md)
#### [SSO 证书](active-directory-sso-certs.md)

### [使用 SCIM 预配用户](active-directory-scim-provisioning.md)
### [文档库](active-directory-apps-index.md)


## 管理目录
### 自定义域名
#### [概述](active-directory-add-domain-concepts.md)
#### 添加域名
##### [Azure 门户](active-directory-domains-add-azure-portal.md)
##### [经典门户](active-directory-add-domain.md)
##### [使用 AD FS](active-directory-add-domain-federated.md)
#### [分配用户](active-directory-add-domain-add-users.md)
#### 管理域名
##### [Azure 门户](active-directory-domains-manage-azure-portal.md)
##### [经典门户](active-directory-add-manage-domain-names.md)
### 自定义登录页
#### [Azure 门户](active-directory-branding-custom-signon-azure-portal.md)
#### [特定于语言](active-directory-branding-localize-azure-portal.md)
#### [经典门户](active-directory-add-company-branding.md)
### [管理目录](active-directory-administer.md)
### [多个目录](active-directory-licensing-directory-independence.md)
### [O365 目录](active-directory-manage-o365-subscription.md)
### [自助注册](active-directory-self-service-signup.md)
### [企业状态漫游](active-directory-windows-enterprise-state-roaming-overview.md)
#### [启用](active-directory-windows-enterprise-state-roaming-enable.md)
#### [组策略设置](active-directory-windows-enterprise-state-roaming-group-policy-settings.md)
#### [Windows 10 设置](active-directory-windows-enterprise-state-roaming-windows-settings-reference.md)
#### [常见问题](active-directory-windows-enterprise-state-roaming-faqs.md)
#### [故障排除](active-directory-windows-enterprise-state-roaming-troubleshooting.md)
### [将合作伙伴与 Azure AD B2B 集成](active-directory-b2b-what-is-azure-ad-b2b.md)
#### [概述](active-directory-b2b-collaboration-overview.md)
#### [工作原理](active-directory-b2b-how-it-works.md)
#### [功能比较](active-directory-b2b-compare-external-identities.md)
#### [演练](active-directory-b2b-detailed-walkthrough.md)
#### [限制](active-directory-b2b-current-preview-limitations.md)
#### [CSV 文件格式](active-directory-b2b-references-csv-file-format.md)
#### [用户对象](active-directory-b2b-references-external-user-object-attribute-changes.md)
#### [用户令牌](active-directory-b2b-references-external-user-token-format.md)
### [使用 Azure AD Connect 集成本地标识](./connect/active-directory-aadconnect.md)


## 委托对资源的访问权限
### [管理员角色](active-directory-assign-admin-roles.md)
#### [分配管理员角色](active-directory-users-assign-role-azure-portal.md)
### [管理单元](active-directory-administrative-units-management.md)
### [Azure 中的资源访问权限](active-directory-understanding-resource-access.md)
### [基于角色的访问控制](role-based-access-control-what-is.md)
#### 管理访问权限
##### [Azure 门户](role-based-access-control-manage-assignments.md)
##### [经典门户](role-based-access-control-configure.md)
#### [内置角色](role-based-access-built-in-roles.md)
#### [自定义角色](role-based-access-control-custom-roles.md)
#### [报告](role-based-access-control-access-change-history-report.md)
#### 管理角色的更多方式
##### [Azure CLI](role-based-access-control-manage-access-azure-cli.md)
##### [PowerShell](role-based-access-control-manage-access-powershell.md)
##### [REST](role-based-access-control-manage-access-rest.md)
#### [故障排除](role-based-access-control-troubleshooting.md)
### [配置令牌生存期](active-directory-configurable-token-lifetimes.md)

## 保护标识
### [Azure AD Identity Protection](active-directory-identityprotection.md)
#### [启用](active-directory-identityprotection-enable.md)
#### [登录体验](active-directory-identityprotection-flows.md)
#### [解除阻止用户](active-directory-identityprotection-unblock-howto.md)
#### [检测漏洞](active-directory-identityprotection-vulnerabilities.md)
#### [风险事件类型](active-directory-identityprotection-risk-events-types.md)
#### [模拟风险事件](active-directory-identityprotection-playbook.md)
#### [通知](active-directory-identityprotection-notifications.md)
#### [术语表](active-directory-identityprotection-glossary.md)
#### [Microsoft Graph](active-directory-identityprotection-graph-getting-started.md)
### [Privileged Identity Management](./privileged-identity-management/active-directory-securing-privileged-access.md)

## [在 Azure VM 上部署](virtual-networks-windows-server-active-directory-virtual-machines.md)
### [Azure VM 上的 Windows Server Active Directory](active-directory-deploying-ws-ad-guidelines.md)
### [Azure 虚拟网络中的副本域控制器](active-directory-install-replica-active-directory-domain-controller.md)
### [在 Azure 虚拟网络中新建林](active-directory-new-forest-virtual-machine.md)

## [部署混合标识解决方案](active-directory-hybrid-identity-design-considerations-overview.md)
### 确定要求
#### [标识](active-directory-hybrid-identity-design-considerations-business-needs.md)
#### [目录同步](active-directory-hybrid-identity-design-considerations-directory-sync-requirements.md)
#### [多重身份验证](active-directory-hybrid-identity-design-considerations-multifactor-auth-requirements.md)
#### [标识生命周期策略](active-directory-hybrid-identity-design-considerations-lifecycle-adoption-strategy.md)
### [数据安全性规划](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md)
#### [数据保护](active-directory-hybrid-identity-design-considerations-dataprotection-requirements.md)
#### [内容管理](active-directory-hybrid-identity-design-considerations-contentmgt-requirements.md)
#### [访问控制](active-directory-hybrid-identity-design-considerations-accesscontrol-requirements.md)
#### [事件响应](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md)
### 规划标识生命周期
#### [任务](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md)
#### [采用策略](active-directory-hybrid-identity-design-considerations-identity-adoption-strategy.md)
### [后续步骤](active-directory-hybrid-identity-design-considerations-nextsteps.md)
### [工具比较](active-directory-hybrid-identity-design-considerations-tools-comparison.md)

## [在 Azure 中部署 AD FS](active-directory-aadconnect-azure-adfs.md)
### [高可用性](active-directory-adfs-in-azure-with-azure-traffic-manager.md)
### [更改签名哈希算法](active-directory-federation-sha256-guidance.md)

## [故障排除](active-directory-troubleshooting.md)


# 引用
## [PowerShell cmdlet](/powershell/)
## [Java API 参考](/java/api)
## [.NET API](/active-directory/adal/microsoft.identitymodel.clients.activedirectory)
## [服务限制和局限性](active-directory-service-limits-restrictions.md)

# 相关内容
## [多重身份验证](/azure/multi-factor-authentication/)
## [Azure AD Connect](./connect/active-directory-aadconnect.md)
## [Azure AD Connect Health](./connect-health/active-directory-aadconnect-health.md)
## [面向开发人员的 Azure AD](./develop/active-directory-how-to-integrate.md)
## [Azure AD Privileged Identity Management](./privileged-identity-management/active-directory-securing-privileged-access.md)

# 资源
## [价格](https://azure.microsoft.com/pricing/details/active-directory/)
## [MSDN 论坛](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=WindowsAzureAD)
## [堆栈溢出](http://stackoverflow.com/questions/tagged/azure-active-directory)
## [视频](https://azure.microsoft.com/documentation/videos/index/?services=active-directory)
## [服务更新](https://azure.microsoft.com/updates/?product=active-directory)
## [Azure 反馈论坛](https://feedback.azure.com/forums/169401-azure-active-directory)

<!---HONumber=Mooncake_0120_2017-->