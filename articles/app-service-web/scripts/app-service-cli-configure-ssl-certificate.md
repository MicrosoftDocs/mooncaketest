---
title: Azure CLI Script Sample - Bind a custom SSL certificate to a web app | Azure
description: Azure CLI Script Sample - Bind a custom SSL certificate to a web app
services: app-service\web
documentationcenter: ''
author: cephalin
manager: erikre
editor: ''
tags: azure-service-management

ms.assetid: eb95d350-81ea-4145-a1e2-6eea3b7469b2
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
wacn.date: ''
ms.author: cephalin
---

# Bind a custom SSL certificate to a web app

This sample script creates a web app in App Service with its related resources, then binds the SSL certificate of a custom domain name to it. 

If needed, install the Azure CLI using the instruction found in the [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli). Also, ensure that:

- A connection with Azure has been created using the `az login` command.
- You have access to your domain registrar's DNS configuration page.
- You have a valid .PFX file and its password for the SSL certificate you want to upload and bind.

This sample works in a Bash shell. For options on running Azure CLI scripts on Windows client, see [Running the Azure CLI in Windows](../../virtual-machines/virtual-machines-windows-cli-options.md).

## Sample script

```azurecli
#!/bin/bash

fqdn=<Replace with www.{yourdomain}>
pfxPath=<Replace with path to your .PFX file>
pfxPassword=<Replace with your .PFX password>
webappname=mywebapp$RANDOM

# Create a resource group.
az group create --location chinanorth --name myResourceGroup

# Create an App Service plan in Basic tier (minimum required by custom domains).
az appservice plan create --name $webappname --resource-group myResourceGroup --sku B1

# Create a web app.
az appservice web create --name $webappname --resource-group myResourceGroup \
--plan $webappname

echo "Configure a CNAME record that maps $fqdn to $webappname.chinacloudsites.cn"
read -p "Press [Enter] key when ready ..."

# Before continuing, go to your DNS configuration UI for your custom domain and follow the 
# instructions at https://aka.ms/appservicecustomdns to configure a CNAME record for the 
# hostname "www" and point it your web app's default domain name.

# Map your prepared custom domain name to the web app.
az appservice web config hostname add --webapp $webappname --resource-group myResourceGroup \
--name $fqdn

# Upload the SSL certificate and get the thumbprint.
thumprint=$(az appservice web config ssl upload --certificate-file $pfxPath \
--certificate-password $pfxPassword --name $webappname --resource-group myResourceGroup \
--query thumbprint --output tsv)

# Binds the uploaded SSL certificate to the web app.
az appservice web config ssl bind --certificate-thumbprint $thumbprint --ssl-type SNI \
--name $webappname --resource-group myResourceGroup

echo "You can now browse to https://$fqdn"
```

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## Script explanation

This script uses the following commands. Each command in the table links to command specific documentation.

| Command | Notes |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Creates a resource group in which all resources are stored. |
| [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create) | Creates an App Service plan. |
| [az appservice web create](https://docs.microsoft.com/cli/azure/appservice/web#delete) | Creates an Azure web app. |
| [az appservice web config hostname add](https://docs.microsoft.com/cli/azure/appservice/web/config/hostname#add) | Update an App Service plan to scale its pricing tier. |
| [az appservice web config ssl upload](https://docs.microsoft.com/cli/azure/appservice/web/config/ssl#upload) | Upload an SSL certificate to a web app. |
| [az appservice web config ssl bind](https://docs.microsoft.com/cli/azure/appservice/web/config/ssl#bind) | Bind an uploaded SSL certificate to a web app. |

## Next steps

For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).

Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).