---
title: Windows HPC Pack cluster options in the cloud | Azure
description: Learn about options with Microsoft HPC Pack to create and manage a Windows high performance computing (HPC) cluster in the Azure cloud
services: virtual-machines-windows,cloud-services,batch
documentationcenter: ''
author: dlepow
manager: timlt
editor: ''
tags: azure-resource-manager,azure-service-management,hpc-pack

ms.assetid: 02c5566d-2129-483c-9ecf-0d61030442d7
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 02/06/2017
wacn.date: ''
ms.author: danlep

---
# Options with HPC Pack to create and manage a Windows HPC cluster in Azure
[!INCLUDE [virtual-machines-common-hpcpack-cluster-options](../../includes/virtual-machines-common-hpcpack-cluster-options.md)]

## Run an HPC Pack cluster in Azure VMs
### Azure templates

>[!NOTE]
> Templates you downloaded from the GitHub Repo "azure-quickstart-templates" must be modified in order to fit in the Azure China Cloud Environment. For example, replace some endpoints -- "blob.core.chinacloudapi.cn" by "blob.core.chinacloudapi.cn", "chinacloudapp.cn" by "chinacloudapp.cn"; change some unsupported VM images; and, changes some unsupported VM sizes.

* (Quickstart) [Create an HPC cluster](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster)
* (Quickstart) [Create an HPC cluster with custom compute node image](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-custom-image)

### PowerShell deployment script
* [Create an HPC cluster with the HPC Pack IaaS deployment script](virtual-machines-windows-classic-hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

### Tutorials
* [Tutorial: Get started with an HPC Pack cluster in Azure to run Excel and SOA workloads](virtual-machines-windows-excel-cluster-hpcpack.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

### Manual deployment with the Azure portal preview
* [Set up the head node of an HPC Pack cluster in an Azure VM](virtual-machines-windows-hpcpack-cluster-headnode.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

### Cluster management
* [Manage compute nodes in an HPC Pack cluster in Azure](virtual-machines-windows-classic-hpcpack-cluster-node-manage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [Grow and shrink Azure compute resources in an HPC Pack cluster](virtual-machines-windows-classic-hpcpack-cluster-node-autogrowshrink.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [Submit jobs to an HPC Pack cluster in Azure](virtual-machines-windows-hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Job management in HPC Pack](https://technet.microsoft.com/zh-cn/library/jj899585.aspx)

## Add worker role nodes to an HPC Pack cluster
* [Burst to Azure worker instances with HPC Pack](https://technet.microsoft.com/zh-cn/library/gg481749.aspx)
* [Tutorial: Set up a hybrid cluster with HPC Pack in Azure](../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md)
* [Add Azure "burst" nodes to an HPC Pack head node in Azure](virtual-machines-windows-classic-hpcpack-cluster-node-burst.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## Integrate with Azure Batch
* [Burst to Azure Batch with HPC Pack](https://technet.microsoft.com/zh-cn/library/mt612877.aspx)