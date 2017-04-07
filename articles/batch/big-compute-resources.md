---
title: Resources for batch and HPC workloads in the cloud | Azure
description: Lists technical resources to help you run your large-scale parallel, batch, and high performance computing (HPC) workloads in Azure.
services: batch, cloud-services, virtual-machines
documentationcenter: ''
author: dlepow
manager: timlt
editor: ''

ms.assetid: 6f8be911-c841-41ae-88d3-3bcfc029eb7f
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: big-compute
ms.date: 01/23/2017
wacn.date: ''
ms.author: danlep
---

# Big Compute in Azure: Technical resources for batch and high-performance computing
This is a guide to technical resources to help you run your large-scale parallel, batch, and high-performance computing (HPC) workloads in Azure. Extend your existing batch or HPC workloads to the Azure cloud, or build new Big Compute solutions using a range of Azure services.

## Solutions options
Learn about Big Compute options in Azure, and choose the right approach for your workload and business need.

- [Batch and HPC solutions](./batch-hpc-solutions.md)

## Azure Batch
[Batch](https://www.azure.cn/home/features/batch/) is a platform service that makes it easy to cloud-enable your Linux and Windows applications and run jobs without setting up and managing a cluster and job scheduler. Use the SDK to integrate client applications with Azure Batch through various languages, stage data to Azure, and build job execution pipelines.

- [Documentation](./index.md)
- [.NET](https://msdn.microsoft.com/zh-cn/library/azure/mt348682.aspx), Python, [Node.js](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/), [Java](http://azure.github.io/azure-sdk-for-java/), and [REST](https://msdn.microsoft.com/zh-cn/library/azure/dn820158.aspx) API reference
- [Batch management .NET library](https://msdn.microsoft.com/zh-cn/library/mt463120.aspx) reference
- Tutorials: Get started with [Azure Batch library for .NET](./batch-dotnet-get-started.md) and [Batch Python client](./batch-python-tutorial.md)
- [Batch forum](https://social.msdn.microsoft.com/Forums/zh-cn/home?forum=azurebatch)

## HPC cluster solutions
Deploy or extend your existing Windows HPC cluster to Azure to run your compute intensive workloads.  

### Microsoft HPC Pack
HPC Pack is Microsoft's free HPC solution built on Azure and Windows Server technologies, capable of running Windows and Linux HPC workloads.  

- [Download HPC Pack 2016](https://www.microsoft.com/zh-cn/download/details.aspx?id=54507)
- [Download HPC Pack 2012 R2 Update 3](https://www.microsoft.com/zh-cn/download/details.aspx?id=49922)
- [Documentation](https://technet.microsoft.com/zh-cn/library/jj899572.aspx)
- [Burst to Azure worker instances with HPC Pack](https://technet.microsoft.com/zh-cn/library/gg481749.aspx)
- [Burst to Azure Batch with HPC Pack](https://technet.microsoft.com/zh-cn/library/mt612877.aspx)
- [Windows HPC forums](https://social.microsoft.com/Forums/home?category=windowshpc)

### Linux and OSS cluster solutions
Use these Azure templates to deploy Linux HPC clusters.

  and [blog post](http://blogs.technet.com/b/windowshpc/archive/2015/06/06/deploy-a-slurm-cluster-on-azure.aspx)

## Microsoft MPI
[Microsoft MPI](https://msdn.microsoft.com/zh-cn/library/bb524831.aspx) (MS-MPI) is a Microsoft implementation of the Message Passing Interface standard for developing and running parallel applications on the Windows platform.

- [Download MS-MPI](http://go.microsoft.com/FWLink/p/?LinkID=389556)
- [MS-MPI reference](https://msdn.microsoft.com/zh-cn/library/dn473458.aspx)
- [MPI forum](https://social.microsoft.com/Forums/en-us/home?forum=windowshpcmpi)

## Compute-intensive instances
Azure offers a [range of VM sizes](../virtual-machines/virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json/) to a back-end RDMA network, to run your Linux and Windows HPC workloads.

## Samples and demos
- [Azure Batch C# and Python code samples](https://github.com/Azure/azure-batch-samples)
- [Batch Shipyard](https://azure.github.io/batch-shipyard/) toolkit for easy deployment of batch-style Dockerized workloads to Azure Batch
- [Test drive SUSE Linux Enterprise Server for HPC](https://azure.microsoft.com/marketplace/partners/suse/suselinuxenterpriseserver12optimizedforhighperformancecompute/)

## Related Azure services

- [HDInsight](../hdinsight/index.md)
- [Virtual Machines](../virtual-machines/index.md)
- [Virtual Machine Scale Sets](../virtual-machine-scale-sets/index.md)
- [Cloud Services](../cloud-services/index.md)
- [App Service](../app-service/index.md)
- [Media Services](../media-services/index.md)

## Industry solutions
- [Banking and capital markets](https://finance.azure.com/)
- [Engineering simulations](https://simulation.azure.com/) 

## Customer stories
- [ANEO](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=4168) 
- [d3View](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=22088)
- [Ludwig Institute of Cancer Research](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=5830)
- [Microsoft Research](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=15634)
- [Milliman](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=14967)
- [Mitsubishi UFJ Securities International](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=26266)
- [Schlumberger](http://azure.microsoft.com/blog/big-compute-for-large-engineering-simulations)
- [Towers Watson](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18222)
- [UberCloud](https://simulation.azure.com/casestudies/Team-182-ABB-UC-Final.pdf)

## Next steps
- For the latest announcements, see the [Microsoft HPC and Batch team blog](http://blogs.technet.com/b/windowshpc/) and the [Azure blog](https://azure.microsoft.com/blog/tag/hpc/).
- Also see [what's new in Batch](https://azure.microsoft.com/updates/?service=batch) or subscribe to the [RSS feed](https://azure.microsoft.com/updates/feed/?service=batch).