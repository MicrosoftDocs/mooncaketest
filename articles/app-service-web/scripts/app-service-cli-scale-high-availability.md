---
title: Azure CLI Script Sample - Scale a web app worldwide with a high-availabilty architecture | Azure
description: Azure CLI Script Sample - Scale a web app worldwide with a high-availabilty architecture
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: ''
tags: azure-service-management

ms.assetid: e4033a50-0e05-4505-8ce8-c876204b2acc
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
wacn.date: ''
ms.author: cfowler
---

# Scale a web app worldwide with a high-availability architecture

In this scenario you will create a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints. Once the exercise is complete you will have a high-available architecture which allows provides global availability of your web app based on the lowest network latency.

If needed, install the Azure CLI using the instruction found in the [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), and then run `az login` to create a connection with Azure.

This sample works in a Bash shell. For options on running Azure CLI scripts on Windows client, see [Running the Azure CLI in Windows](../../virtual-machines/virtual-machines-windows-cli-options.md).

## Sample script

```azurecli
#/bin/bash

# Variables
trafficManagerDnsName="myDnsName$random"
app1Name="AppServiceTM1$random"
app2Name="AppServiceTM2$random"
location1="ChinaNorth"
location2="ChinaEast"

# Create a Resource Group
az group create --name myResourceGroup --location $location1

# Create a Traffic Manager Profile
az network traffic-manager profile create --name $trafficManagerDnsName-tmp --resource-group myResourceGroup --routing-method Performance --unique-dns-name $trafficManagerDnsName

# Create App Service Plans in two Regions
az appservice plan create --name $app1Name-Plan --resource-group myResourceGroup --location $location1 --sku S1
az appservice plan create --name $app2Name-Plan --resource-group myResourceGroup --location $location2 --sku S1

# Add a Web App to each App Service Plan
site1=$(az appservice web create --name $app1Name --plan $app1Name-Plan --resource-group myResourceGroup --query id --output tsv)
site2=$(az appservice web create --name $app2Name --plan $app2Name-Plan --resource-group myResourceGroup --query id --output tsv)

# Assign each Web App as an Endpoint for high-availabilty
az network traffic-manager endpoint create -n $app1Name-$location1 --profile-name $trafficManagerDnsName-tmp -g myResourceGroup --type azureEndpoints --target-resource-id $site1
az network traffic-manager endpoint create -n $app2Name-$location2 --profile-name $trafficManagerDnsName-tmp -g myResourceGroup --type azureEndpoints --target-resource-id $site2
```

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## Script explanation

This script uses the following commands to create a resource group, web app, traffic manager profile, and all related resources. Each command in the table links to command specific documentation.

| Command | Notes |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Creates a resource group in which all resources are stored. |
| [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create) | Creates an App Service plan. This is like a server farm for your Azure web app. |
| [az appservice web create](https://docs.microsoft.com/cli/azure/appservice/web#create) | Creates an Azure web app within the App Service plan. |
| [az network traffic-manager profile create](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) | Creates an Azure Traffic Manager profile. |
| [az network traffic-manager endpoint create](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) | Adds a endpoint to an Azure Traffic Manager Profile. |

## Next steps

For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).

Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).