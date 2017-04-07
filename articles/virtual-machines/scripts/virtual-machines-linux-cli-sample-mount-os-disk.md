---
title: Azure CLI Script Sample - Mount operating system disk | Azure
description: Azure CLI Script Sample - Mount operating system disk
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management

ms.assetid:
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/27/2017
wacn.date: ''
ms.author: nepeters
---

# Troubleshoot a VMs operating system disk

This script mounts the operating system disk of a failed or problematic virtual machine as a data disk to a second virtual machine. This can be useful when troubleshooting disk issues or recovering data. 

If needed, install the Azure CLI using the instruction found in the [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), and then run `az login` to create a connection with Azure. Also, you need an existing virtual machine. Update the name and resource group of the existing virtual machine in the script sample.

This sample works in a Bash shell. For options on running Azure CLI scripts on Windows client, see [Running the Azure CLI in Windows](../virtual-machines-windows-cli-options.md).

## Sample script

```azurecli
#!/bin/bash

# Source virtual machine details.
sourcevm=<Replace with vm name>
resourcegroup=<Replace with resource group name>

# Get the disk id for the source VM operating system disk.
diskid="$(az vm show -g $resourcegroup -n $sourcevm --query [storageProfile.osDisk.managedDisk.id] -o tsv)"

# Delete the source virtual machine, this will not delete the disk.
az vm delete -g $resourcegroup -n $sourcevm --force

# Create a new virtual machine, this creates SSH keys if not present.
az vm create --resource-group $resourcegroup --name myVM --image UbuntuLTS --generate-ssh-keys

# Attach disk as a data disk to the newly created VM.
az vm disk attach --resource-group $resourcegroup --vm-name myVM --disk $diskid

# Configure disk on new VM.
ip=$(az vm list-ip-addresses --resource-group $resourcegroup --name myVM --query '[].virtualMachine.network.publicIpAddresses[0].ipAddress' -o tsv)
ssh $ip 'sudo mkdir /mnt/remountedOsDisk'
ssh $ip 'sudo mount -t ext4 /dev/sdc1 /mnt/remountedOsDisk'
```

## Script explanation

This script uses the following commands to create a resource group, virtual machine, and all related resources. Each command in the table links to command specific documentation.

| Command | Notes |
|---|---|
| [az vm show](https://docs.microsoft.com/cli/azure/vm#show) | Return a list of virtual machines. In this case, the query option is used to return the virtual machine operating system disk. This value is then added to a variable name 'uri'. |
| [az vm delete](https://docs.microsoft.com/cli/azure/vm#delete) | Deletes a virtual machine. |
| [az vm create](https://docs.microsoft.com/cli/azure/vm#create) | Creates a virtual machine.  |
| [az vm disk attach](https://docs.microsoft.com/cli/azure/vm/disk#attach) | Attaches a disk to a virtual machine. |
| [az vm list-ip-addresses](https://docs.microsoft.com/cli/azure/vm#list-ip-addresses) | Returns the IP addresses of a virtual machine. |

## Next steps

For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).

Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../virtual-machines-linux-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).