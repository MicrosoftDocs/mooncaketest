---
title: 使用 Resource Manager 和 PowerShell 将 VNet 网关添加到 ExpressRoute 的虚拟网络中 | Azure
description: 本文指导你将 VNet 网关添加到为 ExpressRoute 创建的 Resource Manager VNet 中
documentationCenter: na
services: expressroute
authors: charwen
manager: carmonm
editor: ''
tags: azure-resource-manager

ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/21/2016
wacn.date: 01/09/2017
ms.author: charwen
---

# 使用 Resource Manager 和 PowerShell 为 ExpressRoute 配置虚拟网络网关

> [!div class="op_single_selector"]
- [PowerShell - Resource Manager](./expressroute-howto-add-gateway-resource-manager.md)
- [PowerShell - Classic](./expressroute-howto-add-gateway-classic.md)

本文将指导你完成为预先存在的 VNet 添加、重设大小和删除虚拟网络 (VNet) 网关的步骤。此配置的步骤专用于使用 **Resource Manager 部署模型**创建的、将在 ExpressRoute 配置中使用的 VNet。

**关于 Azure 部署模型**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## 开始之前

确认已安装此配置所需的 Azure PowerShell cmdlet（1.0.2 或更高版本）。如果尚未安装 cmdlet，必须先安装，然后才能开始执行配置步骤。有关安装 Azure PowerShell 的详细信息，请参阅[如何安装和配置 Azure PowerShell](../powershell-install-configure.md)。

[!INCLUDE [expressroute-gateway-rm-ps](../../includes/expressroute-gateway-rm-ps-include.md)]

## 后续步骤

创建 VNet 网关之后，可以将 VNet 链接到 ExpressRoute 线路。请参阅[将虚拟网络链接到 ExpressRoute 线路](./expressroute-howto-linkvnet-arm.md)。

<!---HONumber=Mooncake_Quality_Review_0104_2017-->