---
title: Create a work or school identity in AAD for Linux | Azure
description: Learn how to create a work or school identity in Azure Active Directory to use with your Linux virtual machines.
services: virtual-machines-linux
documentationcenter: ''
author: squillace
manager: timlt
editor: ''
tags: azure-service-management,azure-resource-manager

ms.assetid: b0f86d77-c669-4aa1-a095-c2aa4d9105fe
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/23/2016
wacn.date: ''
ms.author: rasquill

---
# Creating a Work or School identity in Azure Active Directory to use with Linux VMs
If you created a personal Azure account -- you used an *Azure.cn account* identity to create it. Many great features of Azure -- [resource group templates](../azure-resource-manager/resource-group-overview.md) is one example -- require a work or school account (an identity managed by Azure Active Directory) to work. You can follow the instructions below to create a new work or school account because fortunately, one of the best things about your personal Azure account is that it comes with a default Azure Active Directory domain that you can use to create a new work or school account that you can use with Azure features that require it.

However, recent changes make it possible to manage your subscription with any type of Azure account using the `azure login -e AzureChinaCloud` interactive login method described [here](../xplat-cli-connect.md). You can either use that mechanism, or you can follow the instructions that follow. You can also [create a work or school identity in Azure Active Directory to use with Windows VMs](virtual-machines-windows-create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-both-include.md)]

[!INCLUDE [virtual-machines-common-create-aad-work-id](../../includes/virtual-machines-common-create-aad-work-id.md)]