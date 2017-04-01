---
title: Create a Linux VM using an Azure template | Azure
description: Create a Linux VM on Azure using an Azure Resource Manager template.
services: virtual-machines-linux
documentationcenter: ''
author: vlivech
manager: timlt
editor: ''
tags: azure-service-management,azure-resource-manager

ms.assetid: 721b8378-9e47-411e-842c-ec3276d3256a
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: hero-article
ms.date: 10/24/2016
wacn.date: ''
ms.author: v-livech
ms.custom: H1Hack27Feb2017

---
# How to create a Linux VM using an Azure Resourec Manager template
This article shows you how to quickly deploy a Linux Virtual Machine on Azure using an Azure Template.  The article requires:

* an Azure account ([get a trial](https://www.azure.cn/pricing/1rmb-trial/)).
* the [Azure CLI](../cli-install-nodejs.md) logged in with `azure login -e AzureChinaCloud`.
* the Azure CLI *must be in* Azure Resource Manager mode `azure config mode arm`.

You can also quickly deploy a Linux VM template by using the [Azure portal preview](virtual-machines-linux-quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## Quick Command Summary
```azurecli
azure group create \
    -n myResourceGroup \
    -l chinanorth \
    --template-file /path/to/azuredeploy.json
```

## Detailed Walkthrough
Templates allow you to create VMs on Azure with settings that you want to customize during the launch, settings like usernames and hostnames. For this article, we are launching an Azure template utilizing an Ubuntu VM along with a network security group (NSG) with port 22 open for SSH.

Azure Resource Manager templates are JSON files that can be used for simple one-off tasks like launching an Ubuntu VM as done in this article.  Azure Templates can also be used to construct complex Azure configurations of entire environments like a testing, dev, or production deployment stack.

## Create the Linux VM
The following code example shows how to call `azure group create` to create a resource group and deploy an SSH-secured Linux VM at the same time using [this Azure Resource Manager template](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json). Remember that in your example you need to use names that are unique to your environment. This example uses `myResourceGroup` as the resource group name, and `myVM` as the VM name.

>[!NOTE]
> Templates you downloaded from the GitHub Repo "azure-quickstart-templates" must be modified in order to fit in the Azure China Cloud Environment. For example, replace some endpoints -- "blob.core.windows.net" by "blob.core.chinacloudapi.cn", "cloudapp.azure.com" by "chinacloudapp.cn"; change some unsupported VM images; and, changes some unsupported VM sizes.

```azurecli
azure group create \
    --name myResourceGroup \
    --location chinanorth \
    --template-file /path/to/azuredeploy.json
```

The output should look like the following output block:

```azurecli
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Creating resource group myResourceGroup
info:    Created resource group myResourceGroup
info:    Supply values for the following parameters
sshKeyData: ssh-rsa AAAAB3Nza<..ssh public key text..>VQgwjNjQ== myAdminUser@myVM
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "azuredeploy"
data:    Id:                  /subscriptions/<..subid text..>/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            chinanorth
data:    Provisioning State:  Succeeded
data:    Tags: null
data:
info:    group create command OK
```

That example deployed a VM using the `--template-file` parameter with a path to the template file as an argument. You can also use `--template-uri` to deploy directly from the github raw file, if you are sure the template is suitable for Azure China. The Azure CLI prompts you for the parameters required by the template.

## Next steps
Search the [templates gallery](https://github.com/Azure/azure-quickstart-templates/) to discover what app frameworks to deploy next.