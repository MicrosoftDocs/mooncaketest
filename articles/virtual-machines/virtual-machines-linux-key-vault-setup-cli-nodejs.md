---
title: Set up Key Vault for Linux VMs with the Azure CLI 1.0 | Azure
description: How to set up Key Vault for use with an Azure Resource Manager virtual machine with the Azure CLI 1.0.
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
# Set up Key Vault for virtual machines in Azure Resource Manager with the Azure CLI 1.0
In the Azure Resource Manager stack, secrets/certificates are modeled as resources that are provided by the resource provider of Key Vault. To learn more about Azure Key Vault, see [What is Azure Key Vault?](../key-vault/key-vault-whatis.md) In order for Key Vault to be used with Azure Resource Manager virtual machines, the *EnabledForDeployment* property on Key Vault must be set to true. You can do this in various clients. This article shows you how to set up Key Vault for use with Azure Virtual Machines.

## CLI versions to complete the task
You can complete the task using one of the following CLI versions

- [Azure CLI 1.0](#quick-commands) - our CLI for the classic and resource management deployment models (this article)
- [Azure CLI 2.0](virtual-machines-linux-key-vault-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model

## Use CLI 1.0 to set up Key Vault
To create a key vault by using the command-line interface (CLI), see [Manage Key Vault using CLI](../key-vault/key-vault-manage-with-cli.md#create-a-key-vault).

For CLI 1.0, you have to create the key vault before you assign the deployment policy. You can then assign the policy by using the following command:

    azure keyvault set-policy ContosoKeyVault -enabled-for-deployment true

## Use templates to set up Key Vault
When you use a template, you need to set the `enabledForDeployment` property to `true` for the Key Vault resource.

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

For other options that you can configure when you create a key vault by using templates, see [Create a key vault](https://github.com/Azure/azure-quickstart-templates/tree/master/101-key-vault-create/).

>[!NOTE]
> Templates you downloaded from the GitHub Repo "azure-quickstart-templates" must be modified in order to fit in the Azure China Cloud Environment. For example, replace some endpoints -- "blob.core.windows.net" by "blob.core.chinacloudapi.cn", "cloudapp.azure.com" by "chinacloudapp.cn"; change some unsupported VM images; and, changes some unsupported VM sizes.