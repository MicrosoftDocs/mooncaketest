---
title: Azure CLI Script Sample - Connect a web app to a SQL database | Azure
description: Azure CLI Script Sample - Connect a web app to a SQL database
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: ''
tags: azure-service-management

ms.assetid: 7c2efdd0-f553-4038-a77a-e953021b3f77
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
wacn.date: ''
ms.author: cfowler
---

# Connect a web app to a SQL database

In this scenario you will learn how to create an Azure SQL database and an Azure web app. Then you will link the SQL database to the web app using app settings.

If needed, install the Azure CLI using the instruction found in the [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), and then run `az login` to create a connection with Azure.

This sample works in a Bash shell. For options on running Azure CLI scripts on Windows client, see [Running the Azure CLI in Windows](../../virtual-machines/virtual-machines-windows-cli-options.md).

## Sample script

```azurecli
#/bin/bash

# Variables
appName="webappwithSQL$random"
serverName="webappwithsql$random"
location="ChinaNorth"
startip="0.0.0.0"
endip="0.0.0.0"
username="<replace-with-username>"
sqlServerPassword="<replace-with-password>"

# Create a Resource Group 
az group create --name myResourceGroup --location $location

# Create an App Service Plan
az appservice plan create --name WebAppWithSQLPlan --resource-group myResourceGroup --location $location

# Create a Web App
az appservice web create --name $appName --plan WebAppWithSQLPlan --resource-group myResourceGroup

# Create a SQL Server
az sql server create --name $serverName --resource-group myResourceGroup --location $location --admin-user $username --admin-password $sqlServerPassword

# Configure Firewall for Azure Access
az sql server firewall-rule create --resource-group myResourceGroup --server $serverName --name AllowYourIp --start-ip-address $startip --end-ip-address $endip

# Create Database on Server
az sql db create --resource-group myResourceGroup --server $serverName --name MySampleDatabase --service-objective S0

# Assign the connection string to an App Setting in the Web App
az appservice web config appsettings update --settings "SQLSRV_CONNSTR=Server=tcp:$serverName.database.chinacloudapi.cn;Database=MySampleDatabase;User ID=$username@$serverName;Password=$sqlServerPassword;Trusted_Connection=False;Encrypt=True;" --name $appName --resource-group myResourceGroup
```

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## Script explanation

This script uses the following commands to create a resource group, web app, SQL database and all related resources. Each command in the table links to command specific documentation.

| Command | Notes |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Creates a resource group in which all resources are stored. |
| [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create) | Creates an App Service plan. This is like a server farm for your Azure web app. |
| [az appservice web create](https://docs.microsoft.com/cli/azure/appservice/web#create) | Creates an Azure web app within the App Service plan. |
| [az sql server create](https://docs.microsoft.com/cli/azure/sql/server#create) | Creates a SQL Database Server.  |
| [az sql db create](https://docs.microsoft.com/cli/azure/sql/db#create) | Creates a new database with the SQL Database Server. |
| [az appservice web config appsetings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) | Creates or updates an app setting for an Azure web app. App settings are exposed as environment variables for your app. |

## Next steps

For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).

Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).