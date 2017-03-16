---
title: 使用 PowerShell 控制路由和使用虚拟设备（Azure）
description: 了解如何使用 PowerShell 控制 VNet 中的路由 | 经典
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: ''
tags: azure-service-management

ms.assetid: d8d07c16-cbe5-4536-acd6-870269346fe3
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
wacn.date: 12/26/2016
ms.author: jdial
---

# 使用 PowerShell 控制路由和使用虚拟设备（经典）
> [!div class="op_single_selector"]
- [PowerShell](./virtual-network-create-udr-arm-ps.md)
- [Azure CLI](./virtual-network-create-udr-arm-cli.md)
- [模板](./virtual-network-create-udr-arm-template.md)
- [PowerShell（经典）](./virtual-network-create-udr-classic-ps.md)
- [CLI（经典）](./virtual-network-create-udr-classic-cli.md)

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

> [!IMPORTANT]
在使用 Azure 资源之前，请务必了解 Azure 当前使用两种部署模型：Azure Resource Manager 部署模型和经典部署模型。在使用任何 Azure 资源前，请确保了解[部署模型和工具](../azure-resource-manager/resource-manager-deployment-model.md)。可选择本文顶部的选项，查看不同工具的文档。本文介绍经典部署模型。
> 

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

下述示例 Azure PowerShell 命令需要一个已经基于上述方案创建的简单环境。如果你想要运行本文档中所显示的命令，首先需要构建[使用 PowerShell 创建 VNet](./virtual-networks-create-vnet-classic-netcfg-ps.md) 中所述的环境。

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## 为前端子网创建 UDR
若要根据上述方案为前端子网创建所需的路由表和路由，请按照下面的步骤操作。

1. 运行以下命令，为前端子网创建路由表：

    ```powershell
    New-AzureRouteTable -Name UDR-FrontEnd -Location chinanorth `
    -Label "Route table for front end subnet"
    ```

    输出：

    ```
    Name         Location   Label                          
    ----         --------   -----                          
    UDR-FrontEnd China North    Route table for front end subnet
    ```
2. 运行以下命令，在路由表中创建路由，将流向后端子网 (192.168.2.0/24) 的所有流量发送到 **FW1** VM (192.168.0.4)：

    ```powershell
    Get-AzureRouteTable UDR-FrontEnd `
    |Set-AzureRoute -RouteName RouteToBackEnd -AddressPrefix 192.168.2.0/24 `
    -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

    输出：

    ```
    Name     : UDR-FrontEnd
    Location : China North
    Label    : Route table for frontend subnet
    Routes   : 
               Name                 Address Prefix    Next hop type        Next hop IP address
               ----                 --------------    -------------        -------------------
               RouteToBackEnd       192.168.2.0/24    VirtualAppliance     192.168.0.4  
    ```
3. 运行以下命令，将路由表与 **FrontEnd** 子网关联：

    ```powershell
    Set-AzureSubnetRouteTable -VirtualNetworkName TestVNet `
    -SubnetName FrontEnd `
    -RouteTableName UDR-FrontEnd
    ```

## 为后端子网创建 UDR
若要根据方案为后端子网创建所需的路由表和路由，请完成以下步骤：

1. 运行以下命令，为后端子网创建路由表：

    ```powershell
    New-AzureRouteTable -Name UDR-BackEnd `
    -Location chinanorth `
    -Label "Route table for back end subnet"
    ```

2. 运行以下命令，在路由表中创建路由，将流向前端子网 (192.168.1.0/24) 的所有流量发送到 **FW1** VM (192.168.0.4)：

    ```powershell
    Get-AzureRouteTable UDR-BackEnd `
    |Set-AzureRoute -RouteName RouteToFrontEnd -AddressPrefix 192.168.1.0/24 `
    -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

3. 运行以下命令，将路由表与 **BackEnd** 子网关联：

    ```powershell
    Set-AzureSubnetRouteTable -VirtualNetworkName TestVNet `
    -SubnetName BackEnd `
    -RouteTableName UDR-BackEnd
    ```

## 在 FW1 VM 上启用 IP 转发

若要在 FW1 VM 中启用 IP 转发，请完成以下步骤：

1. 运行以下命令，检查 IP 转发的状态：

    ```powershell
    Get-AzureVM -Name FW1 -ServiceName TestRGFW `
    | Get-AzureIPForwarding
    ```

    输出：

    ```
    Disabled
    ```
2. 运行以下命令，为 *FW1* VM 启用 IP 转发：

    ```powershell
    Get-AzureVM -Name FW1 -ServiceName TestRGFW `
    | Set-AzureIPForwarding -Enable
    ```

<!---HONumber=Mooncake_1219_2016-->