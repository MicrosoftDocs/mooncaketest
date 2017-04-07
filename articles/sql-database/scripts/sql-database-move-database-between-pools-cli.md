---
title: Azure CLI Script-Move a SQL database and elastic pools | Microsoft Docs
description: Azure CLI Script Sample - Move a SQL database between elastic pools using Azure CLI
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

# Create elastic pools and move databases between pools and out of a pool using the Azure CLI

This sample CLI script creates two elastic pools and moves a database from one elastic pool into another elastic pool, and then moves a database out of an elastic pool to a single database performance level. 

If needed, install the Azure CLI using the instructions found in the [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), and then run `az login` to create a connection with Azure.

This sample works in a Bash shell. For options on running Azure CLI scripts on Windows, see [Running the Azure CLI in Windows](../../virtual-machines/virtual-machines-windows-cli-options.md).

## Sample script

```azurecli
#!/bin/bash

# Set an admin login and password for your database
adminlogin=ServerAdmin
password=ChangeYourAdminPassword1
# The logical server name has to be unique in the system
servername=server-$RANDOM

# Create a resource group
az group create \
	--name myResourceGroup \
	--location "China East" 

# Create a logical server in the resource group
az sql server create \
	--name $servername \
	--resource-group myResourceGroup \
	--location "China East" \
	--admin-user $adminlogin \
	--admin-password $password

# Create two pools in the logical server
az sql elastic-pools create \
	--resource-group myResourceGroup \
	--location "China East"  \
	--server $servername \
	--name myFirstPool \
	--dtu 50 \
	--database-dtu-max 20
az sql elastic-pools create \
	--resource-group myResourceGroup \
	--location "China East"  \
	--server $servername \
	--name MySecondPool \
	--dtu 50 \
	--database-dtu-max 50

# Create a database in the first pool
az sql db create \
	--resource-group myResourceGroup \
	--server $servername \
	--name mySampleDatabase \
	--elastic-pool-name myFirstPool

# Move the database to the second pool - create command updates the db if it exists
az sql db create \
	--resource-group myResourceGroup \
	--server-name $servername \
	--name mySampleDatabase \
	--elastic-pool-name mySecondPool

# Move the database to standalone S1 performance level
az sql db create \
	--resource-group myResourceGroup \
	--server $servername \
	--name mySampleDatabase \
	--service-objective S1
```

## Clean up deployment

After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.

```azurecli
az group delete --name myResourceGroup
```

## Script explanation

This script uses the following commands. Each command in the table links to command specific documentation.

| Command | Notes |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Creates a resource group in which all resources are stored. |
| [az sql server create](https://docs.microsoft.com/cli/azure/sql/server#create) | Creates a logical server that hosts a database or elastic pool. |
| [az sql elastic-pools create](https://docs.microsoft.com/cli/azure/sql/elastic-pools#create) | Creates an elastic pool within the logical server. |
| [az sql db create](https://docs.microsoft.com/cli/azure/sql/db#create) | Creates a database in a logical server as a single or a pooled database. |
| [az sql db update](https://docs.microsoft.com/cli/azure/sql/db#update) | Updates database properties or moves a database into, out of, or between elastic pools. |
| [az group delete](https://docs.microsoft.com/cli/azure/vm/extension#set) | Deletes a resource group including all nested resources. |

## Next steps

For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).

Additional SQL Database CLI script samples can be found in the [Azure SQL Database documentation](../sql-database-cli-samples.md).


