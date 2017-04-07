---
title: Azure CLI Script-Scale an elastic pool | Microsoft Docs
description: Azure CLI Script Sample - Scale an elastic database pool
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management

ms.assetid:
ms.service: sql-database
ms.custom: sample
ms.devlang: CLI
ms.topic: article
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 03/16/2017
ms.author: janeng
---

# Scale an elastic pool in Azure SQL Database using the Azure CLI

This sample CLI script creates elastic pools, moves pooled databases, and changes performance levels. 

If needed, install the Azure CLI using the instructions found in the [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), and then run `az login` to create a connection with Azure.

This sample works in a Bash shell. For options on running Azure CLI scripts on Windows, see [Running the Azure CLI in Windows](../../virtual-machines/virtual-machines-windows-cli-options.md).

## Sample script

```azurecli
#!/bin/bash

# Set an admin login and password for your database
adminlogin=ServerAdmin
password=ChangeYourAdminPassword1
# the logical server name has to be unique in the system
servername=server-$RANDOM

# Create a resource group
az group create \
	--name myResourceGroup \
	--location "China East" 

# Create a server
az sql server create \
	--name $servername \
	--resource-group myResourceGroup \
	--location "China East" \
	--admin-user $adminlogin \
	--admin-password $password

# Create a pool
az sql elastic-pools create \
	--resource-group myResourceGroup \
	--location "China East"  \
	--server $servername \
	--name samplepool \
	--dtu 50 \
	--database-dtu-max 20

# Create two database in the pool
az sql db create \
	--resource-group myResourceGroup \
	--server $servername \
	--name myFirstSampleDatabase \
	--elastic-pool-name samplepool
az sql db create \
	--resource-group myResourceGroup \
	--server $servername \
	--name mySecondSampleDatabase \
	--elastic-pool-name samplepool

# Scale up to the pool to 100 eDTU
az sql elastic-pools update \
	--resource-group myResourceGroup \
	--server $servername \
	--name samplepool \
	--set dtu=100
```

## Clean up deployment

After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.

```azurecli
az group delete --name myResourceGroup
```

## Script explanation

This script uses the following commands to create a resource group, logical server, SQL Database, and firewall rules. Each command in the table links to command specific documentation.

| Command | Notes |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Creates a resource group in which all resources are stored. |
| [az sql server create](https://docs.microsoft.com/cli/azure/sql/server#create) | Creates a logical server that hosts the SQL Database. |
| [az sql elastic-pools create](https://docs.microsoft.com/cli/azure/sql/elastic-pools#create) | Creates an elastic database pool within the logical server. |
| [az sql db create](https://docs.microsoft.com/cli/azure/sql/db#create) | Creates the SQL Database in the logical server. |
| [az sql elastic-pools update](https://docs.microsoft.com/cli/azure/sql/elastic-pools#update) | Updates an elastic database pool, in this example changes the assigned eDTU. |
| [az group delete](https://docs.microsoft.com/cli/azure/vm/extension#set) | Deletes a resource group including all nested resources. |

## Next steps

For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).

Additional SQL Database CLI script samples can be found in the [Azure SQL Database documentation](../sql-database-cli-samples.md).
