---
title: Azure CLI Script Sample - Create a web app and deploy code to a staging environment | Azure
description: Azure CLI Script Sample - Create a web app and deploy code to a staging environment
services: app-service\web
documentationcenter: ''
author: cephalin
manager: erikre
editor: ''
tags: azure-service-management

ms.assetid: 2b995dcd-e471-4355-9fda-00babcdb156e
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
wacn.date: ''
ms.author: cephalin
---

# Create a web app and deploy code to a staging environment

This sample script creates a web app in App Service with an additional deployment slot called "staging", and then deploys a sample app to the "staging" slot.

If needed, install the Azure CLI using the instruction found in the [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), and then run `az login` to create a connection with Azure.

This sample works in a Bash shell. For options on running Azure CLI scripts on Windows client, see [Running the Azure CLI in Windows](../../virtual-machines/virtual-machines-windows-cli-options.md).

## Sample script

```azurecli
#!/bin/bash

gitrepo=<Replace with a public GitHub repo URL. e.g. https://github.com/Azure-Samples/app-service-web-dotnet-get-started.git>
webappname=mywebapp$RANDOM

# Create a resource group.
az group create --location chinanorth --name myResourceGroup

# Create an App Service plan in STANDARD tier (minimum required by deployment slots).
az appservice plan create --name $webappname --resource-group myResourceGroup --sku S1

# Create a web app.
az appservice web create --name $webappname --resource-group myResourceGroup \
--plan $webappname

#Create a deployment slot with the name "staging".
az appservice web deployment slot create --name $webappname --resource-group myResourceGroup \
--slot staging

# Deploy sample code to "staging" slot from GitHub.
az appservice web source-control config --name $webappname --resource-group myResourceGroup \
--slot staging --repo-url $gitrepo --branch master --manual-integration

# Browse to the deployed web app on staging. Deployment may be in progress, so rerun this if necessary.
az appservice web browse --name $webappname --resource-group myResourceGroup --slot staging

# Swap the verified/warmed up staging slot into production.
az appservice web deployment slot swap --name $webappname --resource-group myResourceGroup \
--slot staging

# Browse to the production slot. 
az appservice web browse --name $webappname --resource-group myResourceGroup
```

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## Script explanation

This script uses the following commands. Each command in the table links to command specific documentation.

| Command | Notes |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Creates a resource group in which all resources are stored. |
| [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create) | Creates an App Service plan. |
| [az appservice web create](https://docs.microsoft.com/cli/azure/appservice/web#delete) | Creates an Azure web app. |
| [az appservice web deployment slot create](https://docs.microsoft.com/cli/azure/appservice/web/deployment/slot#create) | Create a deployment slot. |
| [az appservice web source-control config](https://docs.microsoft.com/cli/azure/appservice/web/source-control#config) | Associates an Azure web app with a Git or Mercurial repository. |
| [az appservice web browse](https://docs.microsoft.com/cli/azure/appservice/web#browse) | Open an Azure web app in a browser. |
| [az appservice web deployment slot swap](https://docs.microsoft.com/cli/azure/appservice/web/deployment/slot#swap) | Swap a specified deployment slot into production. |

## Next steps

For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).

Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).