---
title: 在 Azure 中的 Linux VM 上使用 Docker Compose | Microsoft 文档
description: 如何通过 Azure CLI 在 Linux 虚拟机上使用 Docker 和 Compose
services: virtual-machines-linux
documentationcenter: ''
author: iainfoulds
manager: timlt
editor: ''
tags: azure-resource-manager

ms.assetid: 02ab8cf9-318d-4a28-9d0c-4a31dccc2a84
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/13/2017
ms.author: iainfou

---
# 开始使用 Docker 和 Compose，在 Azure 虚拟机上定义和运行多容器应用程序
借助 [Compose](http://github.com/docker/compose)，可以使用简单的文本文件定义由多个 Docker 容器组成的应用程序。然后，使用单个命令启动应用程序，该命令会执行部署定义环境的所有操作。作为示例，本文说明如何在 Ubuntu VM 上使用后端 MariaDB SQL 数据库快速设置 WordPress 博客。也可以使用 Compose 设置更复杂的应用程序。

## 步骤 1：将 Linux VM 设置为 Docker 主机
可以使用各种 Azure 过程和 Azure 应用商店中提供的映像或 Resource Manager 模板创建 Linux VM，并将其设置为 Docker 主机。例如，请参阅[使用 Docker VM 扩展部署环境](virtual-machines-linux-dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)，了解如何使用[快速入门模板](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu)通过 Azure Docker VM 扩展快速创建 Ubuntu VM。

使用 Docker VM 扩展时，VM 将自动设置为 Docker 主机，并且已安装 Compose。可以使用以下 CLI 版本之一创建 VM 和使用 Docker VM 扩展：

- [Azure CLI 1.0](#azure-cli-10) - 适用于经典部署模型和资源管理部署模型的 CLI
- [Azure CLI 2.0（预览版）](#azure-cli-20-preview)：用于资源管理部署模型的下一代 CLI


### Azure CLI 1.0
安装最新的 [Azure CLI 1.0](../xplat-cli-install.md) 并登录到 Azure 帐户。确保在 Resource Manager 模式下创建 VM (`azure config mode arm`)。

以下示例在 `West US` 位置创建名为 `myResourceGroup` 的资源组，并使用 Azure Docker VM 扩展部署 VM。可以使用 [Github 中的 Azure Resource Manager 模板](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu)部署环境：

```azurecli
azure group create --name myResourceGroup --location "West US" \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

Azure CLI 仅在几秒后就会返回提示符，但仍在创建和配置 Docker 主机。需要几分钟才能完成部署。可以使用 `azure vm show` 命令查看有关 Docker 主机状态的详细信息。以下示例检查名为 `myResourceGroup` 的资源组中名为 `myDockerVM`（模板中的默认名称 - 请不要更改此名称）的 VM 的状态。输入在上一步中创建的资源组的名称：

```azurecli
azure vm show --resource-group myResourceGroup --name myDockerVM
```

### Azure CLI 2.0（预览版）
安装最新的 [Azure CLI 2.0（预览版）](/cli/azure/install-az-cli2)并使用 [az login](/cli/azure/#login) 登录到 Azure 帐户。

首先，使用 [az group create](/cli/azure/group#create) 为 Docker 环境创建资源组。以下示例在 `West US` 位置创建名为 `myResourceGroup` 的资源组：

```azurecli
az group create --name myResourceGroup --location westus
```

接下来，使用 [az group deployment create](/cli/azure/group/deployment#create) 部署 VM，其中包含 [Github 中此 Azure Resource Manager 模板](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu)中的 Azure Docker VM 扩展。为 `newStorageAccountName`、`adminUsername`、`adminPassword` 和 `dnsNameForPublicIP` 提供你自己的值：

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

需要几分钟才能完成部署。部署完成后，请[转到下一步骤](#step-2-verify-that-compose-is-installed)，通过 SSH 连接到该 VM。

（可选）若要重新通过提示符进行控制并让部署在后台继续运行，请将 `--no-wait` 标志添加到前一个命令。使用此过程可在 CLI 中执行其他操作，同时让部署持续几分钟。可以使用 [az vm show](/cli/azure/vm#show) 查看有关 Docker 主机状态的详细信息。以下示例检查名为 `myResourceGroup` 的资源组中名为 `myDockerVM`（模板中的默认名称 - 请不要更改此名称）的 VM 的状态：

```azurecli
az vm show --resource-group myResourceGroup --name myDockerVM \
  --query [provisioningState] --output tsv
```

如果此命令返回 `Succeeded`，则表示部署已完成，你可以执行以下步骤通过 SSH 连接到 VM。

## 步骤 2：确认已安装 Compose
部署完成后，使用部署期间提供的 DNS 名称通过 SSH 连接到新 Docker 主机。可以使用 `azure vm show -g myResourceGroup -n myDockerVM` (Azure CLI 1.0) 或 `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv`（Azure CLI 2.0（预览版））查看 VM 的详细信息，包括 DNS 名称。

若要确认 VM 上安装了 Compose，请运行以下命令：

```bash
docker-compose --version
```

会看到类似于 `docker-compose 1.6.2, build 4d72027` 的输出。

> [!TIP] 如果使用其他方法创建 Docker 主机，并需要自行安装 Compose，请参阅 [Compose 文档](https://github.com/docker/compose/blob/882dc673ce84b0b29cd59b6815cb93f74a6c4134/docs/install.md)。


## 步骤 3：创建 docker-compose.yml 配置文件
接下来，创建 `docker-compose.yml` 文件，它只是一个文本配置文件，用于定义要在 VM 上运行的 Docker 容器。该文件指定要在每个容器中运行的映像（也可以是 Dockerfile 的生成）、必要的环境变量和依赖关系、端口以及容器之间的链接。有关 yml 文件语法的详细信息，请参阅 [Compose 文件参考](http://docs.docker.com/compose/yml/)。

创建 `docker-compose.yml` 文件，如下所示：

```bash
touch docker-compose.yml
```

使用最喜欢的文本编辑器向文件添加一些数据。以下示例使用 `vi` 编辑器：

```bash
vi docker-compose.yml
```

将以下示例粘贴到文本文件中。此配置将使用 [DockerHub 注册表](https://registry.hub.docker.com/_/wordpress/)中的映像安装 WordPress（开源博客和内容管理系统）和链接的后端 MariaDB SQL 数据库。输入自己的 `MYSQL_ROOT_PASSWORD`，如下所示：

```sh
wordpress:
  image: wordpress
  links:
    - db:mysql
  ports:
    - 80:80

db:
  image: mariadb
  environment:
    MYSQL_ROOT_PASSWORD: <your password>
```

## 步骤 4：使用 Compose 启动容器
在与 `docker-compose.yml` 文件相同的目录中，运行以下命令（根据环境，可能需要使用 `sudo` 运行 `docker-compose`。）：

```bash
docker-compose up -d
```

此命令会启动 `docker-compose.yml` 中指定的 Docker 容器。此步骤需要一到两分钟才能完成。会看到类似如下示例的输出：

```bash
Creating wordpress_db_1...
Creating wordpress_wordpress_1...
...
```

> [!NOTE] 启动时请务必使用 **-d** 选项，使容器在后台继续运行。


若要验证容器是否已启动，请键入 `docker-compose ps`。你应看到类似如下的内容：

```bash
Name             Command             State              Ports
-------------------------------------------------------------------------
wordpress_db_1     /docker-           Up                 3306/tcp
             entrypoint.sh
             mysqld
wordpress_wordpr   /entrypoint.sh     Up                 0.0.0.0:80->80
ess_1              apache2-for ...                       /tcp
```

现在可以在 VM 的端口 80 上直接连接到 WordPress。打开 Web 浏览器并输入 VM 的 DNS 名称（例如`http://myresourcegroup.westus.cloudapp.azure.com`）。现在，你应看到 WordPress 开始屏幕，你可以在其中完成安装并开始使用应用程序。

![WordPress 开始屏幕][wordpress_start]

## 后续步骤
* 转到 [Docker VM 扩展用户指南](https://github.com/Azure/azure-docker-extension/blob/master/README.md)，了解用于在 Docker VM 中配置 Docker 和 Compose 的更多选项。例如，其中一个选项是将 Compose yml 文件（已转换为 JSON）直接放在 Docker VM 扩展的配置中。
* 有关生成和部署多容器应用的更多示例，请查阅 [Compose 命令行参考](http://docs.docker.com/compose/reference/)和[用户指南](http://docs.docker.com/compose/)。
* 使用 Azure 资源管理器模板（你自己的或[社区](https://azure.microsoft.com/documentation/templates/)提供的），通过 Docker 部署 Azure VM 和使用 Compose 设置的应用程序。例如，[使用 Docker 部署 WordPress 博客](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-wordpress-mysql)模板使用 Docker 和 Compose 通过 Ubuntu VM 上的 MySQL 后端快速部署 WordPress。
* 请尝试将 Docker Compose 与 [Docker Swarm](virtual-machines-linux-docker-swarm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 群集集成。有关方案，请参阅 [Using Compose with Swarm](https://docs.docker.com/compose/swarm/)（将 Compose 与 Swarm 配合使用）。

<!--Image references-->


[wordpress_start]: ./media/virtual-machines-linux-docker-compose-quickstart/WordPress.png

<!---HONumber=Mooncake_0320_2017-->