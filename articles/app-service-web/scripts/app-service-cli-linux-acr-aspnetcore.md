---
title: Azure CLI Script Sample - Create an ASP.NET Core web app in a Docker container from Azure Container Registry | Azure
description: Azure CLI Script Sample - Create an ASP.NET Core web app in a Docker container from Azure Container Registry
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: ''
tags: azure-service-management

ms.assetid: 3a2d1983-ff7b-476a-ac44-49ec2aabb31a
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
wacn.date: ''
ms.author: cfowler
---

# Create an ASP.NET Core web app in a Docker container from Azure Container Registry

In this scenario you will learn how to create a resource group, Linux app service plan, and web app, and deploy an ASP.NET Core application using a Docker Container from the Azure Container Registry.

If needed, install the Azure CLI using the instruction found in the [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), and then run `az login` to create a connection with Azure.

This sample works in a Bash shell. For options on running Azure CLI scripts on Windows client, see [Running the Azure CLI in Windows](../../virtual-machines/virtual-machines-windows-cli-options.md).

## Create app sample

```azurecli
#/bin/bash

# Variables
appName="AppServiceLinuxDocker$RANDOM"
location="chinanorth"
dockerContainerUser="<replace-with-docker-user>"    
dockerHubContainerName="<replace-with-docker-container>"
dockerContainerVersion="latest"

# Create a Resource Group
az group create --name myResourceGroup --location $location

# Create Azure Container Registry
acrUrl=$(az acr create --name $appName --resource-group myResourceGroup --location $location --admin-enabled true --query loginServer --output tsv)
acrCreds=($(az acr credential show --name $appName --resource-group myResourceGroup --query [username,password] --output tsv))

# Pull from Docker
docker login ${acrUrl} -u ${acrCreds[0]} -p ${acrCreds[1]}
docker pull $dockerContainerUser/$dockerHubContainerName:$dockerContainerVersion
docker tag $dockerContainerUser/$dockerHubContainerName:$dockerContainerVersion ${acrUrl}/$dockerHubContainerName:$dockerContainerVersion
docker push ${acrUrl}/$dockerHubContainerName:$dockerContainerVersion

# Create an App Service Plan
az appservice plan create --name AppServiceLinuxDockerPlan --resource-group myResourceGroup --location $location --is-linux --sku S1

# Create a Web App
az appservice web create --name $appName --plan AppServiceLinuxDockerPlan --resource-group myResourceGroup

# Configure Web App with a Custom Docker Container from Docker Hub
az appservice web config container update --docker-registry-server-url http://${acrUrl} --docker-custom-image-name ${acrUrl}/$dockerHubContainerName:$dockerContainerVersion --docker-registry-server-user ${acrCreds[0]} --docker-registry-server-password ${acrCreds[1]} --name $appName --resource-group myResourceGroup
```

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## Script explanation

This script uses the following commands to create a resource group, web app, and all related resources. Each command in the table links to command specific documentation.

| Command | Notes |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Creates a resource group in which all resources are stored. |
| [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create) | Creates an App Service plan. This is like a server farm for your Azure web app. |
| [az appservice web create](https://docs.microsoft.com/cli/azure/appservice/web#create) | Creates an Azure web app within the App Service plan. |
| [az appservice web config container update](https://docs.microsoft.com/cli/azure/appservice/web/config/container#update) | Sets the Docker container for the Azure web app. |

## Next steps

For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).

Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).