---
title: Azure CLI Script Sample - Connect a web app to documentdb | Azure
description: Azure CLI Script Sample - Connect a web app to documentdb
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: ''
tags: azure-service-management

ms.assetid: bbbdbc42-efb5-4b4f-8ba6-c03c9d16a7ea
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
wacn.date: ''
ms.author: cfowler
---

# Connect a web app to a documentdb

In this scenario you will learn how to create an Azure documentdb and an Azure web app. Then you will link the documentdb to the web app using app settings.

If needed, install the Azure CLI using the instruction found in the [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), and then run `az login` to create a connection with Azure.

This sample works in a Bash shell. For options on running Azure CLI scripts on Windows client, see [Running the Azure CLI in Windows](../../virtual-machines/virtual-machines-windows-cli-options.md).

## Sample script

```azurecli
#/bin/bash

# Variables
appName="webappwithdocumentdb$random"
storageName="webappwithdocumentdb$random"
location="ChinaNorth"

# Create a Resource Group 
az group create --name myResourceGroup --location $location

# Create an App Service Plan
az appservice plan create --name WebAppWithDocumentDBPlan --resource-group myResourceGroup --location $location

# Create a Web App
az appservice web create --name $appName --plan WebAppWithDocumentDBPlan --resource-group myResourceGroup 

# Create a DocumentDB
docdb=$(az documentdb create --name $appName --resource-group myResourceGroup --query documentEndpoint --output tsv)
docCreds=$(az documentdb list-keys --name $appName --resource-group myResourceGroup --query primaryMasterKey --output tsv)

# Assign the connection string to an App Setting in the Web App
az appservice web config appsettings update --settings "DOCDB_URL=$docdb" "DOCDB_KEY=$docCreds" --name $appName --resource-group myResourceGroup
```

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## Script explanation

This script uses the following commands to create a resource group, web app, documentdb and all related resources. Each command in the table links to command specific documentation.

| Command | Notes |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Creates a resource group in which all resources are stored. |
| [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create) | Creates an App Service plan. This is like a server farm for your Azure web app. |
| [az appservice web create](https://docs.microsoft.com/cli/azure/appservice/web#create) | Creates an Azure web app within the App Service plan. |
| [az documentdb create](https://docs.microsoft.com/cli/azure/documentdb#create) | Creates a documentdb. This is where the data will be stored. |
| [az documentdb list-keys](https://docs.microsoft.com/cli/azure/documentdb#list-keys) | Lists the access keys for the specified Azure DocumentDB database account. |
| [az appservice web config appsetings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) | Creates or updates an app setting for an Azure web app. App settings are exposed as environment variables for your app. |

## Next steps

For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).

Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).