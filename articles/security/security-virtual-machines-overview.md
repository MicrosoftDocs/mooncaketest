---
title: Azure Virtual Machines Security Overview | Microsoft Azure
description:  Azure Virtual Machines give you the flexibility of virtualization without having to buy and maintain the physical hardware that runs the virtual machine.  This article provides an overview of the core Azure security features that can be used with Azure Virtual Machines. 
services: security
documentationCenter: na
authors: lingche
manager: shlan
editor: lingche

ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/16/2016
ms.author: lingche
---

# Azure Virtual Machines security overview

Azure Virtual Machines lets you deploy a wide range of computing solutions in an agile way. With support for Microsoft Windows, Linux, Microsoft SQL Server, Oracle, IBM, SAP, and Azure BizTalk Services, you can deploy any workload and any language on nearly any operating system.

An Azure virtual machine gives you the flexibility of virtualization without having to buy and maintain the physical hardware that runs the virtual machine.  You can build and deploy your applications with the assurance that your data is protected and safe in our highly secure datacenters.

With Azure, you can build security-enhanced, compliant solutions that:

- Protect your virtual machines from viruses and malware
- Encrypt your sensitive data
- Secure network traffic
- Identify and detect threats
- Meet compliance requirements

The goal of this article is to provide an overview of the core Azure security features that can be used with virtual machines. We also provide links to articles that give details of each feature so you can learn more.  

The core Azure Virtual Machine security capabilities to be covered in this article:

- Antimalware
- Hardware Security Module
- Virtual machine backup
- Azure Site Recovery
- Virtual networking
- Compliance

## Antimalware

With Azure, you can use antimalware software from security vendors such as Microsoft and Asiainfo (ex-TrendMicro China) to protect your virtual machines from malicious files, adware, and other threats. See the Learn More section below to find articles on partner solutions.

Microsoft Antimalware for Azure Cloud Services and Virtual Machines is a real-time protection capability that helps identify and remove viruses, spyware, and other malicious software.  Microsoft Antimalware provides configurable alerts when known malicious or unwanted software attempts to install itself or run on your Azure systems.

Microsoft Antimalware is a single-agent solution for applications and tenant environments, designed to run in the background without human intervention. You can deploy protection based on the needs of your application workloads, with either basic secure-by-default or advanced custom configuration, including antimalware monitoring.

When you deploy and enable Microsoft Antimalware, the following core features are available:

- Real-time protection - monitors activity in Cloud Services and on Virtual Machines to detect and block malware execution.
- Scheduled scanning - periodically performs targeted scanning to detect malware, including actively running programs.
- Malware remediation - automatically takes action on detected malware, such as deleting or quarantining malicious files and cleaning up malicious registry entries.
- Signature updates - automatically installs the latest protection signatures (virus definitions) to ensure protection is up-to-date on a pre-determined frequency.
- Antimalware Engine updates – automatically updates the Microsoft Antimalware engine.
- Antimalware Platform updates – automatically updates the Microsoft Antimalware platform.
- Active protection - reports to Azure telemetry metadata about detected threats and suspicious resources to ensure rapid response and enables real-time synchronous signature delivery through the Microsoft Active Protection System (MAPS).
- Samples reporting - provides and reports samples to the Microsoft Antimalware service to help refine the service and enable troubleshooting.
- Exclusions – allows application and service administrators to configure certain files, processes, and drives to exclude them from protection and scanning for performance and other reasons.
- Antimalware event collection - records the antimalware service health, suspicious activities, and remediation actions taken in the operating system event log and collects them into the customer’s Azure Storage account.

Learn more:
To learn more about antimalware software to protect your virtual machines, see:

- [Microsoft Antimalware for Azure Cloud Services and Virtual Machines](../security/azure-security-antimalware.md)
- [Deploying Antimalware Solutions on Azure Virtual Machines](https://azure.microsoft.com/blog/deploying-antimalware-solutions-on-azure-virtual-machines/)
- [How to install and configure Asiainfo Deep Security as a Service on a Windows VM](../virtual-machines/virtual-machines-windows-classic-install-trend.md)
- [Security solutions in the Azure Image Marketplace](https://market.azure.cn/List/Index?sort=Featured&filters=tag:security)

## Hardware security Module

Encryption and authentication do not improve security unless the keys themselves are protected. You can simplify the management and security of your critical secrets and keys by storing them in Azure Key Vault. Key Vault provides the option to store your keys in hardware security modules (HSMs) certified to FIPS 140-2 Level 2 standards. Your SQL Server encryption keys for backup or [transparent data encryption](https://msdn.microsoft.com/library/bb934049.aspx) can all be stored in Key Vault with any keys or secrets from your applications. Permissions and access to these protected items are managed through [Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/).

Learn more:

- [What is Azure Key Vault?](../key-vault/key-vault-whatis.md)
- [Get started with Azure Key Vault](../key-vault/key-vault-get-started.md)
- [Azure Key Vault blog](https://blogs.technet.microsoft.com/kv/)

## Virtual machine backup

Azure Backup is a scalable solution that protects your application data with zero capital investment and minimal operating costs. Application errors can corrupt your data, and human errors can introduce bugs into your applications. With Azure Backup, your virtual machines running Windows and Linux are protected.

Learn more:

- [What is Azure Backup?](../backup/backup-introduction-to-azure-backup.md)
- [Azure Backup Service - FAQ](../backup/backup-azure-backup-faq.md)

## Azure Site Recovery

An important part of your organization's BCDR strategy is figuring out how to keep corporate workloads and apps up and running when planned and unplanned outages occur. Azure Site Recovery helps orchestrate replication, failover, and recovery of workloads and apps so that they are available from a secondary location if your primary location goes down.

Site Recovery:

- **Simplifies your BCDR strategy** — Site Recovery makes it easy to handle replication, failover, and recovery of multiple business workloads and apps from a single location. Site recovery orchestrates replication and failover but doesn't intercept your application data or have any information about it.
- **Provides flexible replication** — Using Site Recovery you can replicate workloads running on Hyper-V virtual machines, VMware virtual machines, and Windows/Linux physical servers.
- **Supports failover and recovery** — Site Recovery provides test failovers to support disaster recovery drills without affecting production environments. You can also run planned failovers with a zero-data loss for expected outages, or unplanned failovers with minimal data loss (depending on replication frequency) for unexpected disasters. After failover, you can failback to your primary sites. Site Recovery provides recovery plans that can include scripts and Azure automation workbooks so that you can customize failover and recovery of multi-tier applications.
- **Eliminates secondary datacenter** — You can replicate to a secondary on-premises site, or to Azure. Using Azure as a destination for disaster recovery eliminates the cost and complexity of maintaining a secondary site. Replicated data is stored in Azure Storage.
- **Integrates with existing BCDR technologies** — Site Recovery partners with other application BCDR features. For example, you can use Site Recovery to protect the SQL Server back end of corporate workloads. This includes native support for SQL Server AlwaysOn to manage the failover of availability groups.

Learn more:

- [What is Azure Site Recovery?](../site-recovery/site-recovery-overview.md)
- [How Does Azure Site Recovery Work?](../site-recovery/site-recovery-components.md)
- [What Workloads are Protected by Azure Site Recovery?](../site-recovery/site-recovery-workload.md)

## Virtual networking

Virtual machines need network connectivity. To support that requirement, Azure requires virtual machines to be connected to an Azure Virtual Network. An Azure Virtual Network is a logical construct built on top of the physical Azure network fabric. Each logical Azure Virtual Network is isolated from all other Azure Virtual Networks. This isolation helps insure that network traffic in your deployments is not accessible to other Microsoft Azure customers.

Learn more:

- [Azure Network Security Overview](../articles/security/security-network-overview.md)
- [Virtual Network Overview](../virtual-network/virtual-networks-overview.md)

## Compliance

Azure Virtual Machines service operated by 21Vianet is certified for ISO/IEC 20000/27001, DJCP, Trusted Cloud Service Certification, GB18030 and other key compliance programs. These certifications make it easier for your own Azure applications to meet compliance requirements and for your business to address a wide range of domestic and international regulatory requirements.

Learn more:

- [Trust Center: Compliance](https://www.trustcenter.cn/zh-cn/compliance/default.html)