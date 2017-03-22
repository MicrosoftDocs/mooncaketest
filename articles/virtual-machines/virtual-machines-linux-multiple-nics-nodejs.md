---
title: 在 Azure 中创建具有多个 NIC 的 Linux VM | Azure
description: 了解如何使用 Azure CLI 或 Resource Manager 模板创建附有多个 NIC 的 Linux VM。
services: virtual-machines-linux
documentationcenter: ''
author: iainfoulds
manager: timlt
editor: ''

ms.assetid: ''
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/09/2017
wacn.date: 03/20/2017
ms.author: iainfou
---

# 使用 Azure CLI 1.0 创建具有多个 NIC 的 VM
可以在 Azure 中创建附有多个虚拟网络接口 (NIC) 的虚拟机 (VM)。一种常见方案是为前端和后端连接使用不同的子网，或者为监视或备份解决方案使用一个专用网络。本文提供用于创建附有多个 NIC 的 VM 的快速命令。有关详细信息，包括如何在自己的 Bash 脚本中创建多个 NIC，请阅读 [Deploying multi-NIC VMs](../virtual-network/virtual-network-deploy-multinic-arm-cli.md)（部署具有多个 NIC 的 VM）。不同的 [VM 大小](./virtual-machines-linux-sizes.md)支持不同数目的 NIC，因此请相应地调整 VM 的大小。

> [!WARNING]
必须在创建 VM 时附加多个 NIC - 不能将 NIC 添加到现有 VM。可以[基于原始虚拟磁盘创建 VM](./virtual-machines-linux-copy-vm.md)，并在部署 VM 时创建多个 NIC。

## 用于完成任务的 CLI 版本
可使用以下 CLI 版本之一完成任务：

- [Azure CLI 1.0](#create-supporting-resources)：用于经典部署模型和资源管理部署模型的 CLI
- Azure CLI 2.0 - 不支持 Azure 中国区的虚拟机，因为 API 版本的缘故。

## <a name="create-supporting-resources"></a> 创建支持资源
确保已登录 [Azure CLI](../xplat-cli-install.md) 并使用 Resource Manager 模式：

```azurecli
azure config mode arm
```

在以下示例中，请将示例参数名称替换为你自己的值。示例参数名称包括 `myResourceGroup`、`mystorageaccount` 和 `myVM`。

首先创建一个资源组。以下示例在 `ChinaNorth` 位置创建名为 `myResourceGroup` 的资源组：

```azurecli
azure group create myResourceGroup -l ChinaNorth
```

创建一个存储帐户用于存放 VM。以下示例创建名为 `mystorageaccount` 的存储帐户：

```azurecli
azure storage account create mystorageaccount -g myResourceGroup \
    -l ChinaNorth --kind Storage --sku-name PLRS
```

创建要将 VM 连接到的虚拟网络。以下示例创建名为 `myVnet`、地址前缀为 `192.168.0.0/16` 的虚拟网络：

```azurecli
azure network vnet create -g myResourceGroup -l ChinaNorth \
    -n myVnet -a 192.168.0.0/16
```

创建两个虚拟网络子网 - 一个用于前端流量，一个用于后端流量。以下示例创建两个子网，分别名为 `mySubnetFrontEnd` 和 `mySubnetBackEnd`：

```azurecli
azure network vnet subnet create -g myResourceGroup -e myVnet \
    -n mySubnetFrontEnd -a 192.168.1.0/24
azure network vnet subnet create -g myResourceGroup -e myVnet \
    -n mySubnetBackEnd -a 192.168.2.0/24
```

## 创建和配置多个 NIC
详细了解如何[使用 Azure CLI 部署多个 NIC](../virtual-network/virtual-network-deploy-multinic-arm-cli.md)，包括如何编写轮流创建所有 NIC 的过程脚本。

以下示例创建两个名为 `myNic1` 和 `myNic2` 的两个 NIC，其中一个 NIC 将连接到每个子网：

```azurecli
azure network nic create --resource-group myResourceGroup --location ChinaNorth \
    -n myNic1 --subnet-vnet-name myVnet --subnet-name mySubnetFrontEnd
azure network nic create --resource-group myResourceGroup --location ChinaNorth \
    -n myNic2 --subnet-vnet-name myVnet --subnet-name mySubnetBackEnd
```

通常，我们还会创建[网络安全组](../virtual-network/virtual-networks-nsg.md)或[负载均衡器](../load-balancer/load-balancer-overview.md)来帮助管理流量以及跨 VM 分布流量。以下示例创建名为 `myNetworkSecurityGroup` 的网络安全组：

```azurecli
azure network nsg create --resource-group myResourceGroup --location ChinaNorth \
    --name myNetworkSecurityGroup
```

使用 `azure network nic set` 将 NIC 绑定到网络安全组：以下示例使用 `myNetworkSecurityGroup` 绑定 `myNic1` 和 `myNic2`：

```azurecli
azure network nic set --resource-group myResourceGroup --name myNic1 \
    --network-security-group-name myNetworkSecurityGroup
azure network nic set --resource-group myResourceGroup --name myNic2 \
    --network-security-group-name myNetworkSecurityGroup
```

## 创建 VM 并附加 NIC
创建 VM 时，可以指定多个 NIC。请不要使用 `--nic-name` 提供单个 NIC，而要使用 `--nic-names` 并提供 NIC 的逗号分隔列表。还需要谨慎选择 VM 的大小。可添加到 VM 的 NIC 数目有限制。详细了解 [Linux VM 大小](./virtual-machines-linux-sizes.md)。以下示例演示如何指定多个 NIC，然后指定可支持使用多个 NIC 的 VM 大小 (`Standard_DS2_v2`)：

```azurecli
azure vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --location ChinaNorth \
    --os-type linux \
    --nic-names myNic1,myNic2 \
    --vm-size Standard_DS2_v2 \
    --storage-account-name mystorageaccount \
    --image-urn UbuntuLTS \
    --admin-username azureuser \
    --ssh-publickey-file ~/.ssh/id_rsa.pub
```

## 使用 Resource Manager 模板创建多个 NIC
Azure Resource Manager 模板使用声明性 JSON 文件来定义环境。阅读 [Azure Resource Manager 概述](../azure-resource-manager/resource-group-overview.md)。Resource Manager 模板可让你在部署期间创建资源的多个实例，例如，创建多个 NIC。使用 *copy* 指定要创建的实例数：

```json
"copy": {
    "name": "multiplenics",
    "count": "[parameters('count')]"
}
```

阅读有关[使用 *copy* 创建多个实例](../azure-resource-manager/resource-group-create-multiple.md)的详细信息。

也可以使用 `copyIndex()` 并在资源名称中追加一个数字，来创建 `myNic1`、`myNic2`，等等。下面显示了追加索引值的示例：

```json
"name": "[concat('myNic', copyIndex())]", 
```

阅读[使用 Resource Manager 模板创建多个 NIC](../virtual-network/virtual-network-deploy-multinic-arm-template.md) 的完整示例。

## 后续步骤
尝试创建具有多个 NIC 的 VM 时，请务必查看 [Linux VM sizes](./virtual-machines-linux-sizes.md)（Linux VM 大小）。注意每个 VM 大小支持的 NIC 数目上限。

请记住，不能将其他 NIC 添加到现有 VM，而必须在部署 VM 时创建所有 NIC。仔细规划部署，确保从一开始就建立了全部所需的网络连接。

<!---HONumber=Mooncake_0313_2017-->