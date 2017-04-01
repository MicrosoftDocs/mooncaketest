---
title: Set up Azure Key Vault for Linux VMs | Azure
description: How to set up Key Vault for use with an Azure Resource Manager virtual machine with the CLI 2.0.
services: virtual-machines-linux
documentationcenter: ''
author: singhkays
manager: timlt
editor: ''
tags: azure-resource-manager

ms.assetid: bccdd5ab-5ccf-4760-9039-92c6eafb15bd
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/24/2017
wacn.date: ''
ms.author: singhkay

---
# How to set up Key Vault for virtual machines with the Azure CLI 2.0

In the Azure Resource Manager stack, secrets/certificates are modeled as resources that are provided by Key Vault. To learn more about Azure Key Vault, see [What is Azure Key Vault?](../key-vault/key-vault-whatis.md) In order for Key Vault to be used with Azure Resource Manager VMs, the *EnabledForDeployment* property on Key Vault must be set to true. This article shows you how to set up Key Vault for use with Azure virtual machines (VMs) using the Azure CLI 2.0. You can also perform these steps with the [Azure CLI 1.0](virtual-machines-linux-key-vault-setup-cli-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

To perform these steps, you need the latest [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](https://docs.microsoft.com/cli/azure/#login).

## Create a Key Vault
Create a key vault and assign the deployment policy with [az keyvault create](https://docs.microsoft.com/cli/azure/keyvault#create). The following example creates a key vault named `myKeyVault` in the `myResourceGroup` resource group:

```azurecli
az keyvault create -l chinanorth -n myKeyVault -g myResourceGroup --enabled-for-deployment true
```

## Update a Key Vault for use with VMs
Set the deployment policy on an existing key vault with [az keyvault update](https://docs.microsoft.com/cli/azure/keyvault#update). The following updates the key vault named `myKeyVault` in the `myResourceGroup` resource group:

```azurecli
az keyvault update -n myKeyVault -g myResourceGroup --set properties.enabledForDeployment=true
```

## Use templates to set up Key Vault
When you use a template, you need to set the `enabledForDeployment` property to `true` for the Key Vault resource as follows:

```json
{
    "type": "Microsoft.KeyVault/vaults",
    "name": "ContosoKeyVault",
    "apiVersion": "2015-06-01",
    "location": "<location-of-key-vault>",
    "properties": {
    "enabledForDeployment": "true",
    ....
    ....
    }
}
```

## Next steps
For other options that you can configure when you create a Key Vault by using templates, see [Create a key vault](https://github.com/Azure/azure-quickstart-templates/tree/master/101-key-vault-create/).

>[!NOTE]
> Templates you downloaded from the GitHub Repo "azure-quickstart-templates" must be modified in order to fit in the Azure China Cloud Environment. For example, replace some endpoints -- "blob.core.windows.net" by "blob.core.chinacloudapi.cn", "cloudapp.azure.com" by "chinacloudapp.cn"; change some unsupported VM images; and, changes some unsupported VM sizes.