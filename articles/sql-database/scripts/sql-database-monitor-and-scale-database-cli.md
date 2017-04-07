---
title: Azure CLI Script-Monitor & scale a single SQL Database | Microsoft Docs
description: Azure CLI Script Sample - Monitor and scale a single SQL database using the Azure CLI
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

# Monitor and scale a single SQL database using the Azure CLI

This sample CLI script scales a single Azure SQL database to a different performance level after querying the size information of the database. 

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
	-location "China East" 

# Create a server
az sql server create \
	--name $servername \
	--resource-group myResourceGroup \
	--location "China East" \
	--admin-user $adminlogin \
	--admin-password $password

# Create a database
az sql db create \
	--resource-group myResourceGroup \
	--server $servername \
	--name mySampleDatabase \
	--service-objective S0

# Monitor database size
az sql db show-usage \
	--name mySampleDatabase \
	--resource-group myResourceGroup \
	--name $servername

# Scale up database to S1 performance level (create command executes update if DB already exists)
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
| [az sql server create](https://docs.microsoft.com/cli/azure/sql/server#create) | Creates a logical server that hosts a database. |
| [az sql db show-usage](https://docs.microsoft.com/cli/azure/sql/db#show-usage) | Shows the size usage information for a database. |
| [az sql db update](https://docs.microsoft.com/cli/azure/sql/db#update) | Updates database properties (such as the service tier or performance level) or moves a database into, out of, or between elastic pools. |
| [az group delete](https://docs.microsoft.com/cli/azure/vm/extension#set) | Deletes a resource group including all nested resources. |
|||

## Next steps

For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).

Additional SQL Database CLI script samples can be found in the [Azure SQL Database documentation](../sql-database-cli-samples.md).
