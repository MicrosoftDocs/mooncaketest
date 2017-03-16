---
title: 使用 Resource Manager 部署模型和 Azure 门户将虚拟网络链接到 ExpressRoute 线路 | Azure
description: 本文档概述了如何将虚拟网络 (VNet) 链接到 ExpressRoute 线路。
services: expressroute
documentationCenter: na
authors: cherylmc
manager: carmonm
editor: ''
tags: azure-resource-manager

ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/13/2016
wacn.date: 01/03/2017
ms.author: cherylmc
---

# 将虚拟网络链接到 ExpressRoute 线路

> [!div class="op_single_selector"]
- [Azure 门户 - Resource Manager](./expressroute-howto-linkvnet-portal-resource-manager.md)
- [PowerShell - Resource Manager](./expressroute-howto-linkvnet-arm.md)
- [PowerShell - 经典](./expressroute-howto-linkvnet-classic.md)

本文将帮助你使用 Resource Manager 部署模型和 Azure 门户将虚拟网络 (VNet) 链接到 Azure ExpressRoute 线路。虚拟网络可以在同一个订阅中，也可以属于另一个订阅。

**关于 Azure 部署模型**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## 配置先决条件

- 在开始配置之前，请务必查看[先决条件](./expressroute-prerequisites.md)、[路由要求](./expressroute-routing.md)和[工作流](./expressroute-workflows.md)。
- 你必须有一个活动的 ExpressRoute 线路。 
    - 请按说明[创建 ExpressRoute 线路](./expressroute-howto-circuit-arm.md)，并通过连接提供商启用该线路。 

    - 请确保为线路配置 Azure 专用对等互连。如需路由说明，请参阅[配置路由](./expressroute-howto-routing-portal-resource-manager.md)一文。

    - 确保配置 Azure 专用对等互连并运行你的网络和 Azure 之间的 BGP 对等互连，以便启用端到端连接。

    - 确保已创建并完全预配一个虚拟网络和一个虚拟网络网关。请按说明创建 [VPN 网关](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)（仅遵循步骤 1-5）。

最多可以将 10 个虚拟网络链接到一条标准 ExpressRoute 线路。使用标准 ExpressRoute 线路时，所有虚拟网络必须都位于同一地缘政治区域。如果已启用 ExpressRoute 高级外接程序，则可以链接 ExpressRoute 线路的地缘政治区域外部的虚拟网络，或者将更多虚拟网络连接到 ExpressRoute 线路。有关高级外接程序的更多详细信息，请参阅[常见问题](./expressroute-faqs.md)。

## 将同一订阅中的虚拟网络连接到线路

### 创建连接

1. 确保已成功配置 ExpressRoute 线路和 Azure 专用对等互连。请遵循[创建 ExpressRoute 线路](./expressroute-howto-circuit-arm.md)和[配置路由](./expressroute-howto-routing-arm.md)中的说明。ExpressRoute 线路应如下图所示。

    ![ExpressRoute 线路屏幕截图](./media/expressroute-howto-linkvnet-portal-resource-manager/routing1.png)

    >[!NOTE]
    > 如果第 3 层提供商配置了你的对等互连，则 BGP 配置信息将不会显示。如果你的线路处于已预配状态，你应该能够创建连接。

2. 现在你可以开始预配连接，以便将虚拟网络网关链接到 ExpressRoute 线路。单击“连接”>“添加”以打开“添加连接”边栏选项卡，然后配置值。请查看以下参考示例。

    ![添加连接屏幕截图](./media/expressroute-howto-linkvnet-portal-resource-manager/samesub1.png)

3. 成功配置你的连接之后，连接对象将显示连接的信息。

    ![连接对象屏幕截图](./media/expressroute-howto-linkvnet-portal-resource-manager/samesub2.png)

### 删除连接

可以通过选择你的连接的边栏选项卡上的“删除”图标来删除连接。

## 将不同订阅中的虚拟网络连接到线路

此时，无法使用 Azure 门户跨订阅连接虚拟网络。但是，你可以使用 PowerShell 来执行此操作。有关详细信息，请参阅 [PowerShell](./expressroute-howto-linkvnet-arm.md) 一文。

## 后续步骤

有关 ExpressRoute 的详细信息，请参阅 [ExpressRoute 常见问题](./expressroute-faqs.md)。

<!---HONumber=Mooncake_0530_2016-->