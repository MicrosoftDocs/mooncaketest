---
title: 服务复原指南 | Azure
description: Azure 服务的灾难恢复和主动复原与可用性指南的链接。
services: ''
documentationCenter: na
authors: adamglick
manager: saladki
editor: ''

ms.service: resiliency
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2016
ms.author: aglick
---

# Azure 服务复原指南
在你有需要时，Azure 可以提供所需的资源。作为良好设计和操作实践的一部分，你应该知道如何规划使用 Azure 服务来实现高可用性，以及应用程序受到服务中断的影响时该怎么做。为了帮助你完成此过程，本文档包含灾难恢复指南以及各种 Azure 服务的设计指南的链接。

##灾难恢复指南
以下灾难恢复指南链接提供所需的信息，以便在受到 Azure 服务中断影响时，帮助你快速使应用程序重新联机。创建这些链接的目的是要帮助回答此问题：“受到 Azure 服务中断的影响时该怎么办？”

##设计指南
以下设计指南链接提供设计和体系结构指导，其创建目的是要帮助你了解如何以能够充分发挥应用程序运行时间的方式来使用每个 Azure 服务。创建这些链接的目的是要帮助回答此问题：“如何确保 bug、硬件故障、服务中断或其他故障不会影响应用程序的总体可用性？” 如果想要了解的服务没有专门的指南，请参阅[构建在 Azure 基础之上的应用程序高可用性](./resiliency-high-availability-azure-applications.md)一文，其中可能包含其他可为设计提供帮助的信息。

##服务指南
| 服务 | 灾难恢复指南 | 设计指南 |
|:---------|:--------------------------:|:------------------:|
| [云服务](https://www.azure.cn/home/features/cloud-services/ "Azure 云服务") | [链接](../cloud-services/cloud-services-disaster-recovery-guidance.md "Azure 云服务灾难恢复指南") | 不可用 |
| [密钥保管库](https://www.azure.cn/home/features/key-vault/ "Azure 密钥保管库") | [链接](../key-vault/key-vault-disaster-recovery-guidance.md "Azure 密钥保管库灾难恢复指南") | 不可用 |
| [存储](https://www.azure.cn/home/features/storage/ "Azure 存储空间") | [链接](../storage/storage-disaster-recovery-guidance.md "Azure 存储空间灾难恢复指南") | 不可用 |
| [SQL 数据库](https://www.azure.cn/home/features/sql-database/ "Azure SQL 数据库") | [链接](../sql-database/sql-database-disaster-recovery.md "Azure SQL 数据库灾难恢复指南") | 不可用 |
| [虚拟机](https://www.azure.cn/home/features/virtual-machines/ "Azure 虚拟机") | [链接](../virtual-machines/virtual-machines-disaster-recovery-guidance.md "Azure 虚拟机灾难恢复指南") | 不可用 |
| [虚拟网络](https://www.azure.cn/home/features/networking/ "Azure 虚拟网络") | [链接](../virtual-network/virtual-network-disaster-recovery-guidance.md "Azure 虚拟网络灾难恢复指南") | 不可用 |

## 后续步骤
如果你正在查找主要侧重于系统与解决方案的指南，请参阅[构建在 Azure 基础之上的应用程序灾难恢复和高可用性](./resiliency-disaster-recovery-high-availability-azure-applications.md)。

<!---HONumber=Mooncake_1031_2016-->
<!-- Update_Description:update meta properties; wording update; update link reference-->