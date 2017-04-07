---
title: Overview of SQL Server on Azure Virtual Machines | Azure
description: Learn about how to run full SQL Server editions on Azure Virtual machines. Get direct links to all SQL Server VM images and related content.
services: virtual-machines-windows
documentationcenter: ''
author: rothja
manager: jhubbard
editor: ''
tags: azure-service-management

ms.assetid: c505089e-6bbf-4d14-af0e-dd39a1872767
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/09/2017
wacn.date: ''
ms.author: jroth

---
# Overview of SQL Server on Azure Virtual Machines
This topic describes your options for running SQL Server on Azure virtual machines (VMs), along with [links to portal images](#option-1-create-a-sql-vm-with-per-minute-licensing) and an overview of [common tasks](#manage-your-sql-vm).

> [!NOTE]
> If you're already familiar with SQL Server and just want to see how to deploy a SQL Server VM, see [Provision a SQL Server virtual machine in the Azure portal preview](virtual-machines-windows-portal-sql-server-provision.md).
> 
> 

## Overview
If you are a database administrator or a developer, Azure VMs provide a way to move your on-premises SQL Server workloads and applications to the Cloud. The following video provides a technical overview of SQL Server Azure VMs.

## Scenarios
There are many reasons that you might choose to host your data in Azure. If your application is moving to Azure, it improves performance to also move the data. But there are other benefits. You automatically have access to multiple data centers for a global presence and disaster recovery. The data is also highly secured and durable.

SQL Server running on Azure VMs is one option for storing your relational data in Azure. It is good choice for several scenarios. For example, you might want to configure the Azure VM as similarly as possible to an on-premises SQL Server machine. Or you might want to run additional applications and services on the same database server. There are two main resources that can help you think through even more scenarios and considerations:

* [SQL Server on Azure virtual machines](https://www.azure.cn/home/features/virtual-machines/#home_vm_overview_info) provides an overview of the best scenarios for using SQL Server on Azure VMs. 
* [Choose a cloud SQL Server option: Azure SQL (PaaS) Database or SQL Server on Azure VMs (IaaS)](../../../sql-database/sql-database-paas-vs-sql-server-iaas.md) provides a detailed comparison between SQL Database and SQL Server running on a VM.

## Create a new SQL VM
The following sections provide direct links to the Azure portal preview for the SQL Server virtual machine gallery images.

Find step-by-step guidance for this process in the tutorial, [Provision a SQL Server virtual machine in the Azure portal preview](virtual-machines-windows-portal-sql-server-provision.md). Also, review the [Performance best practices for SQL Server VMs](virtual-machines-windows-sql-performance.md), which explains how to select the appropriate machine size and other features available during provisioning.

## <a name="option-1-create-a-sql-vm-with-per-minute-licensing"></a> Option 1: Create a SQL VM with per-minute licensing
The following table provides a matrix of the latest SQL Server images in the virtual machine gallery. Click on any link to begin creating a new SQL VM with your specified version, edition, and operating system. 

| Version | Operating System | Edition |
| --- | --- | --- |
| **SQL Server 2016 SP1** |Windows Server 2016 |[Enterprise](https://portal.azure.cn/#create/Microsoft.SQLServer2016SP1EnterpriseWindowsServer2016), [Standard](https://portal.azure.cn/#create/Microsoft.SQLServer2016SP1StandardWindowsServer2016), [Web](https://portal.azure.cn/#create/Microsoft.SQLServer2016SP1WebWindowsServer2016), [Express](https://portal.azure.cn/#create/Microsoft.SQLServer2016SP1ExpressWindowsServer2016), [Developer](https://portal.azure.cn/#create/Microsoft.SQLServer2016SP1DeveloperWindowsServer2016) |
| **SQL Server 2014 SP2** |Windows Server 2012 R2 |[Enterprise](https://portal.azure.cn/#create/Microsoft.SQLServer2014SP2EnterpriseWindowsServer2012R2), [Standard](https://portal.azure.cn/#create/Microsoft.SQLServer2014SP2StandardWindowsServer2012R2), [Web](https://portal.azure.cn/#create/Microsoft.SQLServer2014SP2WebWindowsServer2012R2), [Express](https://portal.azure.cn/#create/Microsoft.SQLServer2014SP2ExpressWindowsServer2012R2) |
| **SQL Server 2012 SP3** |Windows Server 2012 R2 |[Enterprise](https://portal.azure.cn/#create/Microsoft.SQLServer2012SP3EnterpriseWindowsServer2012R2), [Standard](https://portal.azure.cn/#create/Microsoft.SQLServer2012SP3StandardWindowsServer2012R2), [Web](https://portal.azure.cn/#create/Microsoft.SQLServer2012SP3WebWindowsServer2012R2), [Express](https://portal.azure.cn/#create/Microsoft.SQLServer2012SP3ExpressWindowsServer2012R2) |
| **SQL Server 2008 R2 SP3** |Windows Server 2008 R2 |[Enterprise](https://portal.azure.cn/#create/Microsoft.SQLServer2008R2SP3EnterpriseWindowsServer2008R2), [Standard](https://portal.azure.cn/#create/Microsoft.SQLServer2008R2SP3StandardWindowsServer2008R2), [Web](https://portal.azure.cn/#create/Microsoft.SQLServer2008R2SP3WebWindowsServer2008R2) |

In addition to this list, other combinations of SQL Server versions and operating systems are available. Find other images through a marketplace search in the Azure portal preview. 

## <a name="manage-your-sql-vm"></a> Manage your SQL VM
After provisioning your SQL Server VM, there are several optional management tasks. In many aspects, you configure and manage SQL Server exactly like you would manage an on-premises SQL Server instance. However, some tasks are specific to Azure. The following sections highlight some of these areas with links to more information.

### Connect to the VM
One of the most basic management steps is to connect to your SQL Server VM through tools, such as SQL Server Management Studio (SSMS). For instructions on how to connect to your new SQL Server VM, see [Connect to a SQL Server Virtual Machine on Azure](virtual-machines-windows-sql-connect.md).

### Migrate your data
If you have an existing database, you'll want to move that to the newly provisioned SQL VM. For a list of migration options and guidance, see [Migrating a Database to SQL Server on an Azure VM](virtual-machines-windows-migrate-sql.md).

### Configure high availability
If you require high availability, consider configuring SQL Server Availability Groups. This involves multiple Azure VMs in a virtual network. If you want to manually configure your Availability Group and associated listener, see [Configure AlwaysOn Availability Groups in Azure VM](/documentation/articles/virtual-machines-windows-portal-sql-alwayson-availability-groups-manual/).

For other high availability considerations, see [High Availability and Disaster Recovery for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-high-availability-dr.md).

### Back up your data
Azure VMs can take advantage of [Automated Backup](virtual-machines-windows-sql-automated-backup.md), which regularly creates backups of your database to blob storage. You can also manually use this technique. For more information, see [Use Azure Storage for SQL Server Backup and Restore](virtual-machines-windows-use-storage-sql-server-backup-restore.md). For an overview of all backup and restore options, see [Backup and Restore for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-backup-recovery.md).

### Automate updates
Azure VMs can use [Automated Patching](virtual-machines-windows-sql-automated-patching.md) to schedule a maintenance window for installing important windows and SQL Server updates automatically.

### Customer experience improvement program (CEIP)
The Customer Experience Improvement Program (CEIP) is enabled by default. This periodically sends reports to Microsoft to help improve SQL Server. There is no management task required with CEIP unless you want to disable it after provisioning. You can customize or disable the CEIP by connecting to the VM with remote desktop. Then run the **SQL Server Error and Usage Reporting** utility. Follow the instructions to disable reporting. 

For more information, see the CEIP section of the [Accept License Terms](https://msdn.microsoft.com/zh-cn/library/ms143343.aspx) topic. 

## Next steps
For questions about pricing, see [Pricing](https://www.azure.cn/pricing/details/virtual-machines/). Select your target edition of SQL Server in the **VM type** list. Then view the prices for differently sized virtual machines. 

More question? First, see the [SQL Server on Azure Virtual Machines FAQ](virtual-machines-windows-sql-server-iaas-faq.md). But also add your questions or comments to the bottom of any SQL VM topics to interact with Azure.cn and the community.