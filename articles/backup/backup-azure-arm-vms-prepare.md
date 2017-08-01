---
title: 'Azure Backup: Prepare to back up virtual machines | Microsoft Docs'

description: Make sure your environment is prepared for backing up virtual machines in Azure.

services: backup
documentationcenter: ''
author: markgalioto
manager: carmonm
editor: ''
keywords: backups; backing up;

ms.assetid: e87e8db2-b4d9-40e1-a481-1aa560c03395
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 2/7/2017
ms.author: markgal;trinadhk;

---
# Prepare your environment to back up Resource Manager-deployed virtual machines
> [!div class="op_single_selector"]
> * [Resource Manager model](backup-azure-arm-vms-prepare.md)
> * [Classic model](backup-azure-vms-prepare.md)
>
>

This article provides the steps for preparing your environment to back up a Resource Manager-deployed virtual machine (VM). The steps shown in the procedures use the Azure portal.  

The Azure Backup service has two types of vaults (back up vaults and recovery services vaults) for protecting your VMs. A backup vault protects VMs deployed using the Classic deployment model. A recovery services vault protects **both Classic-deployed or Resource Manager-deployed VMs**. You must use a Recovery Services vault to protect a Resource Manager-deployed VM.

> [!NOTE]
> Azure has two deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md). See [Prepare your environment to back up Azure virtual machines](backup-azure-vms-prepare.md) for details on working with Classic deployment model VMs.
>
>

Before you can protect or back up a Resource Manager-deployed virtual machine (VM), make sure these prerequisites exist:

- Create a recovery services vault (or identify an existing recovery services vault) *in the same location as your VM*.
- Select a scenario, define the backup policy, and define items to protect.
- Check the installation of VM Agent on virtual machine.
- Check network connectivity

If you know these conditions already exist in your environment then proceed to the [Back up your VMs article](backup-azure-vms.md). If you need to set up, or check, any of these prerequisites, this article leads you through the steps to prepare that prerequisite.

##Supported operating system for backup
 - **Linux**: Azure Backup supports [a list of distributions that are endorsed by Azure](../virtual-machines/virtual-machines-linux-endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json/) except Core OS Linux. _Other Bring-Your-Own-Linux distributions also might work as long as the VM agent is available on the virtual machine and support for Python exists. However, we do not endorse those distributions for backup._
 - **Windows Server**:  Versions older than Windows Server 2008 R2 are not supported.

## Limitations when backing up and restoring a VM
Before you prepare your environment, please understand the limitations.

- Backing up virtual machines with more than 16 data disks is not supported.
- Backing up virtual machines with a reserved IP address and no defined endpoint is not supported.
- Backup of VMs encrypted using just BEK is not supported. Backup of Linux VMs encrypted using LUKS encryption is not supported.
- Backup of Linux virtual machines with Docker extension is not supported.
- Backup data doesn't include network mounted drives attached to VM.
- Replacing an existing virtual machine during restore is not supported. If you attempt to restore the VM when the VM exists, the restore operation fails.
- Cross-region backup and restore are not supported.
- You can back up virtual machines in all public regions of Azure (see the [checklist](https://azure.microsoft.com/regions/#services) of supported regions). If the region that you are looking for is unsupported today, it will not appear in the dropdown list during vault creation.
- Restoring a domain controller (DC) VM that is part of a multi-DC configuration is supported only through PowerShell. Read more about [restoring a multi-DC domain controller](backup-azure-restore-vms.md#restoring-domain-controller-vms).
- Restoring virtual machines that have the following special network configurations is supported only through PowerShell. VMs created using the restore workflow in the UI will not have these network configurations after the restore operation is complete. To learn more, see [Restoring VMs with special network configurations](backup-azure-restore-vms.md#restoring-vms-with-special-network-configurations).
  - Virtual machines under load balancer configuration (internal and external)
  - Virtual machines with multiple reserved IP addresses
  - Virtual machines with multiple network adapters

## Create a recovery services vault for a VM
A recovery services vault is an entity that stores the backups and recovery points that have been created over time. The recovery services vault also contains the backup policies associated with the protected virtual machines.

Azure Portal Preview does not support Recovery Services in Azure China yet. To create a recovery services vault, follow the PowerShell steps [here](./backup-azure-vms-automation.md#create-a-recovery-services-vault)

## Install the VM Agent on the virtual machine
The Azure VM Agent must be installed on the Azure virtual machine for the Backup extension to work. If your VM was created from the Azure gallery, then the VM Agent is already present on the virtual machine. This information is provided for the situations where you are *not* using a VM created from the Azure gallery - for example you migrated a VM from an on-premises datacenter. In such a case, the VM Agent needs to be installed in order to protect the virtual machine. Learn about the [VM Agent](../virtual-machines/virtual-machines-windows-classic-agents-and-extensions.md#azure-vm-agents-for-windows-and-linux).

If you have problems backing up the Azure VM, check that the Azure VM Agent is correctly installed on the virtual machine (see the table below). The following table provides additional information about the VM Agent for Windows and Linux VMs.

| **Operation** | **Windows** | **Linux** |
| --- | --- | --- |
| Installing the VM Agent |Download and install the [agent MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). You will need Administrator privileges to complete the installation. |<li> Install the latest [Linux agent](../virtual-machines/virtual-machines-linux-agent-user-guide.md). You will need Administrator privileges to complete the installation. We recommend installing agent from your distribution repository. We **do not recommend** installing Linux VM agent directly from github.  |
| Updating the VM Agent |Updating the VM Agent is as simple as reinstalling the [VM Agent binaries](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). <br>Ensure that no backup operation is running while the VM agent is being updated. |Follow the instructions on [updating the Linux VM Agent](../virtual-machines/virtual-machines-linux-update-agent.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json/). We recommend updating agent from your distribution repository. We **do not recommend** updating Linux VM agent directly from github.<br>Ensure that no backup operation is running while the VM Agent is being updated. |
| Validating the VM Agent installation |<li>Navigate to the *C:\WindowsAzure\Packages* folder in the Azure VM. <li>You should find the WaAppAgent.exe file present.<li> Right-click the file, go to **Properties**, and then select the **Details** tab. The Product Version field should be 2.6.1198.718 or higher. |N/A |

### Backup extension
Once the VM Agent is installed on the virtual machine, the Azure Backup service installs the backup extension to the VM Agent. The Azure Backup service seamlessly upgrades and patches the backup extension.

The backup extension is installed by the Backup service whether or not the VM is running. A running VM provides the greatest chance of getting an application-consistent recovery point. However, the Azure Backup service continues to back up the VM even if it is turned off, and the extension could not be installed. This is known as Offline VM. In this case, the recovery point will be *crash consistent*.

## Network connectivity
In order to manage the VM snapshots, the backup extension needs connectivity to the Azure public IP addresses. Without the right Internet connectivity, the virtual machine's HTTP requests time out and the backup operation fails. If your deployment has access restrictions in place (through a network security group (NSG), for example), then choose one of these options for providing a clear path for backup traffic:

- [Whitelist the Azure datacenter IP ranges](http://www.microsoft.com/en-us/download/details.aspx?id=41653) - see the article for instructions on how to whitelist the IP addresses.
- Deploy an HTTP proxy server for routing traffic.

When deciding which option to use, the trade-offs are between manageability, granular control, and cost.

| Option | Advantages | Disadvantages |
| --- | --- | --- |
| Whitelist IP ranges |No additional costs.<br><br>For opening access in an NSG, use the <i>Set-AzureNetworkSecurityRule</i> cmdlet. |Complex to manage as the impacted IP ranges change over time.<br><br>Provides access to the whole of Azure, and not just Storage. |
| HTTP proxy |Granular control in the proxy over the storage URLs allowed.<br>Single point of Internet access to VMs.<br>Not subject to Azure IP address changes. |Additional costs for running a VM with the proxy software. |

### Whitelist the Azure datacenter IP ranges
To whitelist the Azure datacenter IP ranges, please see the [Azure website](http://www.microsoft.com/en-us/download/details.aspx?id=41653) for details on the IP ranges, and instructions.

### Using an HTTP proxy for VM backups
When backing up a VM, the backup extension on the VM sends the snapshot management commands to Azure Storage using an HTTPS API. Route the backup extension traffic through the HTTP proxy since it is the only component configured for access to the public Internet.

> [!NOTE]
> There is no recommendation for the proxy software that should be used. Ensure that you pick a proxy that is compatible with the configuration steps below.
>
>

The example image below shows the three configuration steps necessary to use an HTTP proxy:

- App VM routes all HTTP traffic bound for the public Internet through Proxy VM.
- Proxy VM allows incoming traffic from VMs in the virtual network.
- The Network Security Group (NSG) named NSF-lockdown needs a security rule allowing outbound Internet traffic from Proxy VM.

![NSG with HTTP proxy deployment diagram](./media/backup-azure-vms-prepare/nsg-with-http-proxy.png)

To use an HTTP proxy to communicating to the public Internet, follow these steps:

#### Step 1. Configure outgoing network connections
###### For Windows machines
This will setup proxy server configuration for Local System Account.

1. Download [PsExec](https://technet.microsoft.com/sysinternals/bb897553)
2. Run following command from elevated prompt,

     ```
     psexec -i -s "c:\Program Files\Internet Explorer\iexplore.exe"
     ```
     It will open internet explorer window.
3. Go to Tools -> Internet Options -> Connections -> LAN settings.
4. Verify proxy settings for System account. Set Proxy IP and port.
5. Close Internet Explorer.

This will set up a machine-wide proxy configuration, and will be used for any outgoing HTTP/HTTPS traffic.

If you have setup a proxy server on a current user account(not a Local System Account), use the following script to apply them to SYSTEMACCOUNT:

```
$obj = Get-ItemProperty -Path Registry::"HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections"
Set-ItemProperty -Path Registry::"HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections" -Name DefaultConnectionSettings -Value $obj.DefaultConnectionSettings
Set-ItemProperty -Path Registry::"HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections" -Name SavedLegacySettings -Value $obj.SavedLegacySettings
$obj = Get-ItemProperty -Path Registry::"HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Internet Settings"
Set-ItemProperty -Path Registry::"HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings" -Name ProxyEnable -Value $obj.ProxyEnable
Set-ItemProperty -Path Registry::"HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings" -Name Proxyserver -Value $obj.Proxyserver
```

> [!NOTE]
> If you observe "(407) Proxy Authentication Required" in proxy server log, check your authentication is setup correctly.
>
>

###### For Linux machines
Add the following line to the ```/etc/environment``` file:

```
http_proxy=http://<proxy IP>:<proxy port>
```

Add the following lines to the ```/etc/waagent.conf``` file:

```
HttpProxy.Host=<proxy IP>
HttpProxy.Port=<proxy port>
```

#### Step 2. Allow incoming connections on the proxy server:
1. On the proxy server, open Windows Firewall. The easiest way to access the firewall is to search for Windows Firewall with Advanced Security.

    ![Open the Firewall](./media/backup-azure-vms-prepare/firewall-01.png)
2. In the Windows Firewall dialog, right-click **Inbound Rules** and click **New Rule...**.

    ![Create a new rule](./media/backup-azure-vms-prepare/firewall-02.png)
3. In the **New Inbound Rule Wizard**, choose the **Custom** option for the **Rule Type** and click **Next**.
4. On the page to select the **Program**, choose **All Programs** and click **Next**.
5. On the **Protocol and Ports** page, enter the following information and click **Next**:

    ![Create a new rule](./media/backup-azure-vms-prepare/firewall-03.png)

   - for *Protocol type* choose *TCP*
   - for *Local port* choose *Specific Ports*, in the field below specify the ```<Proxy Port>``` that has been configured.
   - for *Remote port* select *All Ports*

     For the rest of the wizard, click all the way to the end and give this rule a name.

#### Step 3. Add an exception rule to the NSG:
In an Azure PowerShell command prompt, enter the following command:

The following command adds an exception to the NSG. This exception allows TCP traffic from any port on 10.0.0.5 to any Internet address on port 80 (HTTP) or 443 (HTTPS). If you require a specific port in the public Internet, be sure to add that port to the ```-DestinationPortRange``` as well.

```
Get-AzureNetworkSecurityGroup -Name "NSG-lockdown" |
Set-AzureNetworkSecurityRule -Name "allow-proxy " -Action Allow -Protocol TCP -Type Outbound -Priority 200 -SourceAddressPrefix "10.0.0.5/32" -SourcePortRange "*" -DestinationAddressPrefix Internet -DestinationPortRange "80-443"
```


*These steps use specific names and values for this example. Please use the names and values for your deployment when entering, or cutting and pasting details into your code.*

Now that you know you have network connectivity, you are ready to back up your VM. 

## Questions?
If you have questions, or if there is any feature that you would like to see included, [send us feedback](http://aka.ms/azurebackup_feedback).

## Next steps
Now that you have prepared your environment for backing up your VM, your next logical step is to create a backup. The planning article provides more detailed information about backing up VMs.

- [Back up virtual machines](backup-azure-vms.md)
- [Plan your VM backup infrastructure](backup-azure-vms-introduction.md)
- [Manage virtual machine backups](./backup-azure-manage-vms-classic.md)

