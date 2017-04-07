---
title: Azure CLI Script Sample - Deploy a web app from a local Git repository | Azure
description: Azure CLI Script Sample - Deploy a web app from a local Git repository
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management

ms.assetid:
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: article
ms.date: 02/01/2017
wacn.date: ''
ms.author: cephalin
---

# Deploy a web app from a local Git repository

This sample script does the following using Azure CLI 2.0: 

* Create a web app in Azure App Service in the China North Azure region.
* Deploy web app code from a local Git repository.
* Display the deployed web app in the browser.

## Prerequisites

* Run `az login` to log in to Azure.
* Commit your web app code into a local Git repository.

## Create VM sample

```
#!/bin/bash

gitdirectory=<Replace with path to local Git repo>
username=<Replace with desired deployment username>
password=<Replace with desired deployment password>
webappname=mywebapp$RANDOM

# Create a resource group.
az group create --location chinanorth --name myResourceGroup

# Create an App Service plan in FREE tier.
az appservice plan create --name $webappname --resource-group myResourceGroup --sku FREE

# Create a web app.
az appservice web create --name $webappname --resource-group myResourceGroup --plan $webappname

# Set the account-level deployment credentials
az appservice web deployment user set --user-name $username --password $password

# Configure local Git and get deployment URL
url=$(az appservice web source-control config-local-git --name $webappname \
--resource-group myResourceGroup --query url --output tsv)

# Add the Azure remote to your local Git respository and push your code
cd $gitdirectory
git remote add azure $url
git push azure master

# When prompted for password, use the value of $password that you specified

# Browse to the deployed web app.
az appservice web browse --name $webappname --resource-group myResourceGroup
```

## Clean up deployment 

After the script sample has been run, the follow command can be used to remove the Resource Group, web app, and all related resources.

```azurecli
az group delete --name $webappname
```

## Script explanation

This script uses the following commands. Each command in the table links to command specific documentation.

| Command | Notes |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Creates a resource group in which all resources are stored. |
| [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create) | Creates an App Service plan. |
| [az appservice web create](https://docs.microsoft.com/cli/azure/appservice/web#delete) | Creates a web app |
| [az appservice web source-control config-local-git](https://docs.microsoft.com/cli/azure/appservice/web/source-control#config-local-git) | Creates a source control configuration for a local Git repository. |
| [az appservice web browse](https://docs.microsoft.com/cli/azure/appservice/web#browse) | Open a web app in a browser. |

## Next steps

For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).

Additional CLI script samples for Azure App Service Web Apps can be found in the [Azure CLI samples]().