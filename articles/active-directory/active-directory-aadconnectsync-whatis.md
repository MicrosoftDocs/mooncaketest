---
title: Azure AD Connect 同步：理解和自定义同步 | Azure
description: 介绍 Azure AD Connect 同步的工作原理以及如何自定义。
services: active-directory
documentationcenter: ''
author: andkjell
manager: femila
editor: ''

ms.assetid: ee4bf802-045b-4da0-986e-90aba2de58d6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/01/2016
ms.author: markusvi
wacn.date: 12/09/2016
---

# Azure AD Connect 同步：理解和自定义同步
Azure Active Directory Connect 同步服务（Azure AD Connect 同步）是 Azure AD Connect 的一个主要组件。它负责在本地环境与 Azure AD 之间同步标识数据的所有相关操作。Azure AD Connect 同步是 DirSync、Azure AD Sync 和 Forefront Identity Manager 的后继版本，同时配置了 Azure Active Directory 连接器。

本主题是 **Azure AD Connect 同步**（也称为**同步引擎**）的主页，其中列出了与其相关的所有其他主题的链接。有关 Azure AD Connect 的链接，请参阅 [Integrating your on-premises identities with Azure Active Directory](./active-directory-aadconnect.md)（将本地标识与 Azure Active Directory 集成）。

同步服务包括两个组件，本地“Azure AD Connect 同步”组件和 Azure AD 中称为“Azure AD Connect 同步服务”的服务端组件。该服务是 DirSync、Azure AD Sync 和 Azure AD Connect 的常见服务。

## Azure AD Connect 同步主题
| 主题 | 涵盖的内容和阅读时机 |
| --- | --- |
| **Azure AD Connect 同步基础知识** | |
| [了解体系结构](./active-directory-aadconnectsync-understanding-architecture.md) |适合不熟悉同步引擎并想要深入了解所用体系结构和术语的人员。 |
| [技术概念](./active-directory-aadconnectsync-technical-concepts.md) |精简版的体系结构主题，简要解释所用的术语。 |
| [Azure AD Connect 的拓扑](./active-directory-aadconnect-topologies.md) |介绍同步引擎支持的各种拓扑和方案。 |
| **自定义配置** | |
| [再次运行安装向导](./active-directory-aadconnectsync-installation-wizard.md) |介绍再次运行 Azure AD Connect 安装向导时可以使用的选项。 |
| [了解声明性预配](./active-directory-aadconnectsync-understanding-declarative-provisioning.md) |介绍称为“声明性预配”的配置模型。 |
| [了解声明性设置表达式](./active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md) |介绍声明性预配中使用的表达式语言的语法。 |
| [了解默认配置](./active-directory-aadconnectsync-understanding-default-configuration.md) |描述现成的规则和默认配置。此外还描述规则如何一起工作，以供现成的方案使用。 |
| [了解用户和联系人](./active-directory-aadconnectsync-understanding-users-and-contacts.md) |延续前一个主题，说明用户和联系人的配置如何一起工作（尤其是在多林环境中）。 |
| [如何更改默认配置](./active-directory-aadconnectsync-change-the-configuration.md) |逐步讲解如何对属性流做出常见的配置更改。 |
| [更改默认配置的最佳做法](./active-directory-aadconnectsync-best-practices-changing-default-configuration.md) |支持方面的限制，以及如何对现成配置进行更改。 |
| [配置筛选](./active-directory-aadconnectsync-configure-filtering.md) |介绍用于限制哪些对象要同步到 Azure AD 的各种选项，并逐步说明如何配置这些选项。 |
| **功能和方案** | |
| [防止意外删除](./active-directory-aadconnectsync-feature-prevent-accidental-deletes.md) |介绍 *防止意外删除* 功能以及如何配置该功能。 |
| [计划程序](./active-directory-aadconnectsync-feature-scheduler.md) |介绍导入、同步和导出数据的内置计划程序。 |
| [实现密码同步](./active-directory-aadconnectsync-implement-password-synchronization.md) |介绍密码同步的工作原理、实现方式，及其操作与故障排除方法。 |
| [目录扩展](./active-directory-aadconnectsync-feature-directory-extensions.md) |介绍如何使用你自己的自定义属性扩展 Azure AD 架构。 |
| **同步服务** | |
| [Azure AD Connect 同步服务功能](./active-directory-aadconnectsyncservice-features.md) |介绍同步服务端，以及如何在 Azure AD 中更改同步设置。 |
| [重复属性修复](./active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md) |介绍如何启用并使用 **userPrincipalName** 和 **proxyAddresses** 重复属性值复原。 |
| **操作和 UI** | |
| [Synchronization Service Manager](./active-directory-aadconnectsync-service-manager-ui.md) |介绍 Synchronization Service Manager UI，包括[“操作”](./active-directory-aadconnectsync-service-manager-ui-operations.md)、[“连接器”](./active-directory-aadconnectsync-service-manager-ui-connectors.md)、[“Metaverse 设计器”](./active-directory-aadconnectsync-service-manager-ui-mvdesigner.md)和[“Metaverse 搜索”](./active-directory-aadconnectsync-service-manager-ui-mvsearch.md)选项卡。 |
| [操作任务和注意事项](./active-directory-aadconnectsync-operations.md) |描述操作注意事项，例如灾难恢复。 |
| **如何...** | |
| [重置 Azure AD 帐户](./active-directory-aadconnectsync-howto-azureadaccount.md) |如何重置用于从 Azure AD Connect 同步连接到 Azure AD 的服务帐户凭据。 |
| **详细信息和参考** | |
| [端口](./active-directory-aadconnect-ports.md) |列出需要在同步引擎以及本地目录与 Azure AD 之间打开的端口。 |
| [与 Azure Active Directory 同步的属性](./active-directory-aadconnectsync-attributes-synchronized.md) |列出在本地 AD 与 Azure AD 之间同步的所有属性。 |
| [函数引用](./active-directory-aadconnectsync-functions-reference.md) |列出声明性预配中可用的所有函数。 |

## 其他资源
- [将本地标识与 Azure Active Directory 集成](./active-directory-aadconnect.md)

<!---HONumber=Mooncake_1128_2016-->