---
title: Azure CLI Script Sample - Connect a web app to a redis cache | Azure
description: Azure CLI Script Sample - Connect a web app to a redis cache
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: ''
tags: azure-service-management

ms.assetid: bc8345b2-8487-40c6-a91f-77414e8688e6
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
wacn.date: ''
ms.author: cfowler
---

# Connect a web app to a redis cache

In this scenario you will learn how to create an Azure redis cache and an Azure web app. Then you will link the redis cache to the web app using app settings.

If needed, install the Azure CLI using the instruction found in the [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), and then run `az login` to create a connection with Azure.

This sample works in a Bash shell. For options on running Azure CLI scripts on Windows client, see [Running the Azure CLI in Windows](../../virtual-machines/virtual-machines-windows-cli-options.md).

## Sample script

```azurecli
#/bin/bash

# Variables
resourceGroupName="myResourceGroup$RANDOM"
appName="webappwithredis$RANDOM"
storageName="webappredis$RANDOM"
location="chinanorth"

# Create a Resource Group 
az group create --name $resourceGroupName --location $location

# Create an App Service Plan
az appservice plan create --name WebAppWithRedisPlan --resource-group $resourceGroupName --location $location

# Create a Web App
az appservice web create --name $appName --plan WebAppWithRedisPlan --resource-group $resourceGroupName 

# Create a Redis Cache
redis=($(az redis create --name $appName --resource-group $resourceGroupName --location $location --sku-capacity 0 --sku-family C --sku-name Basic --query [hostName,sslPort,accessKeys.primaryKey] --output tsv))

# Assign the connection string to an App Setting in the Web App
az appservice web config appsettings update --settings "REDIS_URL=${redis[0]}" "REDIS_PORT=${redis[1]}" "REDIS_KEY=${redis[2]}" --name $appName --resource-group $resourceGroupName
```

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## Script explanation

This script uses the following commands to create a resource group, web app, redis cache and all related resources. Each command in the table links to command specific documentation.

| Command | Notes |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Creates a resource group in which all resources are stored. |
| [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create) | Creates an App Service plan. This is like a server farm for your Azure web app. |
| [az appservice web create](https://docs.microsoft.com/cli/azure/appservice/web#create) | Creates an Azure web app within the App Service plan. |
| [az redis create](https://docs.microsoft.com/cli/azure/redis#create) | Create new Redis Cache instance. This is where the data will be stored. |
| [az redis list-keys](https://docs.microsoft.com/cli/azure/redis#list-keys) | Lists the access keys for the redis cache instance. |
| [az appservice web config appsetings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) | Creates or updates an app setting for an Azure web app. App settings are exposed as environment variables for your app. |

## Next steps

For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).

Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).