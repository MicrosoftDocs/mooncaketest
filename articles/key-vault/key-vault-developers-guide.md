---
title: Key Vault Developer's Guide | Azure
description: Developers can use Azure Key Vault to manage cryptographic keys within the Azure environment. 
services: key-vault
documentationcenter: ''
author: BrucePerlerMS
manager: mbaldwin
editor: bruceper

ms.assetid: b2b1bd28-e149-4d69-b08b-97f6c50ebe30
ms.service: key-vault
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 01/17/2017
wacn.date: ''
ms.author: bruceper
---

# Azure Key Vault Developer's Guide
Using Key Vault, you are able to securely access sensitive information from within your applications such that:

- Keys and secrets are protected without having to write the code yourself and you are easily able to use them from your applications.
- You are able to have your customers own and manage their own keys so you can concentrate on providing the core software features. In this way, your applications will not own the responsibility or potential liability for your customers’ tenant keys and secrets.
- Your application can use keys for signing and encryption yet keeps the key management external from your application hence, your solution is suitable for an application that is geographically distributed.
- With the September 2016 release of Key Vault, your applications can now make use of Key Vault certificates. For more information, see **About keys, secrets, and certificates** article in the [REST reference](https://msdn.microsoft.com/zh-cn/library/azure/dn903623.aspx).

For more general information on Azure Key Vault, see [What is Key Vault](./key-vault-whatis.md).

## Creating and Managing Key Vaults
Before working with Azure Key Vault in your code, you can create and manage vaults through REST, Resource Manager Templates, PowerShell or CLI, as described in the following articles:

- [Create and Manage Key Vaults with REST](https://msdn.microsoft.com/zh-cn/library/azure/mt620024.aspx)
- [Create and Manage Key Vaults with PowerShell](./key-vault-get-started.md)
- [Create and Manage Key Vaults with CLI](./key-vault-manage-with-cli.md)
- [Create a key vault and add a secret via an Azure Resource Manager template](../azure-resource-manager/resource-manager-template-keyvault.md)

> [!NOTE]
> Operations against key vaults are authenticated through AAD and authorized through Key Vault’s own Access Policy, defined per vault.
>
>

## Coding with Key Vault
The Key Vault management system for programmers consists of several interfaces, with REST as the foundation, [Key Vault REST API Reference](https://msdn.microsoft.com/zh-cn/library/azure/dn903609.aspx).

You can, subject to successful authorization, do the following:

- Manage cryptographic keys using [Create](https://msdn.microsoft.com/zh-cn/library/azure/dn903634.aspx), [Import](https://msdn.microsoft.com/zh-cn/library/azure/dn903626.aspx), [Update](https://msdn.microsoft.com/zh-cn/library/azure/dn903616.aspx), [Delete](https://msdn.microsoft.com/zh-cn/library/azure/dn903611.aspx) and other operations
- Manage secrets using [Get](https://msdn.microsoft.com/zh-cn/library/azure/dn903633.aspx), [Update](https://msdn.microsoft.com/zh-cn/library/azure/dn986818.aspx), [Delete](https://msdn.microsoft.com/zh-cn/library/azure/dn903613.aspx) and other operations
- Use cryptographic keys with [Sign](https://msdn.microsoft.com/zh-cn/library/azure/dn878096.aspx)/[Verify](https://msdn.microsoft.com/zh-cn/library/azure/dn878082.aspx), [WrapKey](https://msdn.microsoft.com/zh-cn/library/azure/dn878066.aspx)/[UnwrapKey](https://msdn.microsoft.com/zh-cn/library/azure/dn878079.aspx) and [Encrypt](https://msdn.microsoft.com/zh-cn/library/azure/dn878060.aspx)/[Decrypt](https://msdn.microsoft.com/zh-cn/library/azure/dn878097.aspx) operations

The following SDKs are available for working with Key Vault:

| [![.NET](./media/key-vault-developers-guide/msft.netlogo_purple.png)](https://msdn.microsoft.com/zh-cn/library/mt765854.aspx) | [![Node.js](./media/key-vault-developers-guide/nodejs.png)](http://azure.github.io/azure-sdk-for-node/azure-arm-keyvault/latest) |
|:---:|:---:|
| [.NET SDK Documentation](https://msdn.microsoft.com/zh-cn/library/mt765854.aspx) |[Node.js SDK Documentation](http://azure.github.io/azure-sdk-for-node/azure-arm-keyvault/latest) |
| [.NET SDK Package on NuGet](http://www.nuget.org/packages/Microsoft.Azure.KeyVault) |[Node.js SDK Package](https://www.npmjs.com/package/azure-keyvault) |

For more information on the 2.x version of the .NET SDK, see the [Release notes](./key-vault-dotnet2api-release-notes.md).

## Example code
For complete examples using Key Vault with your applications, see:

- .NET sample application *HelloKeyVault* and an Azure web service example. [Azure Key Vault code samples](http://www.microsoft.com/en-us/download/details.aspx?id=45343)
- Tutorial to help you learn how to use Azure Key Vault from a web application in Azure. [Use Azure Key Vault from a Web Application](./key-vault-use-from-web-application.md)

## How-tos
The following articles and scenarios provide task-specific guidance for working with Azure Key Vault:

- [Change key vault tenant ID after subscription move](./key-vault-subscription-move-fix.md) - When you move your Azure subscription from tenant A to tenant B, your existing key vaults are inaccessible by the principals (users and applications) in tenant B. Fix this using this guide.
- [Accessing Key Vault behind firewall](./key-vault-access-behind-firewall.md) - To access a key vault your key vault client application needs to be able to access multiple end-points for various functionalities.

- [How to pass secure values (such as passwords) during deployment](../azure-resource-manager/resource-manager-keyvault-parameter.md) - When you need to pass a secure value (like a password) as a parameter during deployment, you can store that value as a secret in an Azure Key Vault and reference the value in other Resource Manager templates.
- [How to use Key Vault for extensible key management with SQL Server](https://msdn.microsoft.com/zh-cn/library/dn198405.aspx) - The SQL Server Connector for Azure Key Vault enables SQL Server and SQL-in-a-VM to leverage the Azure Key Vault service as an Extensible Key Management (EKM) provider to protect its encryption keys for applications link; Transparent Data Encryption, Backup Encryption, and Column Level Encryption.
- [How to deploy Certificates to VMs from Key Vault](https://blogs.technet.microsoft.com/kv/2015/07/14/deploy-certificates-to-vms-from-customer-managed-key-vault/) - A cloud application running in a VM on Azure needs a certificate. How do you get this certificate into this VM today?
- [Deploying Azure Web App Certificate through Key Vault]( https://blogs.msdn.microsoft.com/appserviceteam/2016/05/24/deploying-azure-web-app-certificate-through-key-vault/) provides step-by-step instructions for deploying certificates stored in Key Vault as part of [App Service Certificate](https://azure.microsoft.com/en-us/blog/internals-of-app-service-certificate/) offering.

For more task-specific guidance on integrating and using Key Vaults with Azure, see [Ryan Jones' Azure Resource Manager template examples for Key Vault](https://github.com/rjmax/ArmExamples/tree/master/keyvaultexamples).

## Integrated with Key Vault
These articles are about other scenarios and services that make use of or integrate with Key Vault.

- Azure Disk Encryption leverages the industry standard [BitLocker](https://technet.microsoft.com/zh-cn/library/cc732774.aspx) feature of Windows and the [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) feature of Linux to provide volume encryption for the OS and the data disks. The solution is integrated with Azure Key Vault to help you control and manage the disk encryption keys and secrets in your key vault subscription, while ensuring that all data in the virtual machine disks are encrypted at rest in your Azure storage.

## Supporting Libraries
- [Azure Key Vault Core Library](http://www.nuget.org/packages/Microsoft.Azure.KeyVault.Core) provides `IKey` and `IKeyResolver` interfaces for locating keys from identifiers and performing operations with keys.
- [Azure Key Vault Extensions](http://www.nuget.org/packages/Microsoft.Azure.KeyVault.Extensions) provides extended capabilities for Azure Key Vault.

## Other Key Vault resources
- [Key Vault Blog](http://aka.ms/kvblog)
- [Key Vault Forum](http://aka.ms/kvforum)