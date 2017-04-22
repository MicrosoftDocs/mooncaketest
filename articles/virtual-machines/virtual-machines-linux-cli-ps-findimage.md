---
title: Select Linux VM images with the Azure  CLI | Azure
description: Learn how to determine the publisher, offer, and SKU for images when creating a Linux virtual machine with the Resource Manager deployment model.
services: virtual-machines-linux
documentationcenter: ''
author: squillace
manager: timlt
editor: ''
tags: azure-resource-manager

ms.assetid: 7a858e38-4f17-4e8e-a28a-c7f801101721
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/15/2017
wacn.date: ''
ms.author: rasquill
ms.custom: H1Hack27Feb2017

---
# How to find Linux VM images with the Azure CLI
This topic describes how to find publishers, offers, skus, and versions for each location into which you might deploy. 

[!INCLUDE [azure-cli-2-azurechinacloud-environment-parameter](../../includes/azure-cli-2-azurechinacloud-environment-parameter.md)]

## Use Azure CLI 2.0

Once you have [installed the Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2), use the `az vm image list` command to see a cached list of popular VM images. For example, the following example of the command `az vm image list -o table` displays:

```
You are viewing an offline list of images, use --all to retrieve an up-to-date list
Offer          Publisher               Sku                 Urn                                                             UrnAlias             Version
-------------  ----------------------  ------------------  --------------------------------------------------------------  -------------------  ---------
WindowsServer  MicrosoftWindowsServer  2016-Datacenter     MicrosoftWindowsServer:WindowsServer:2016-Datacenter:latest     Win2016Datacenter    latest
WindowsServer  MicrosoftWindowsServer  2008-R2-SP1         MicrosoftWindowsServer:WindowsServer:2008-R2-SP1:latest         Win2008R2SP1         latest
WindowsServer  MicrosoftWindowsServer  2012-Datacenter     MicrosoftWindowsServer:WindowsServer:2012-Datacenter:latest     Win2012Datacenter    latest
WindowsServer  MicrosoftWindowsServer  2012-R2-Datacenter  MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest  Win2012R2Datacenter  latest
CentOS         OpenLogic               7.3                 OpenLogic:CentOS:7.3:latest                                     CentOS               latest
CoreOS         CoreOS                  Stable              CoreOS:CoreOS:Stable:latest                                     CoreOS               latest
openSUSE-Leap  SUSE                    42.2                SUSE:openSUSE-Leap:42.2:latest                                  openSUSE-Leap        latest
SLES           SUSE                    12-SP2              SUSE:SLES:12-SP2:latest                                         SLES                 latest
UbuntuServer   Canonical               16.04-LTS           Canonical:UbuntuServer:16.04-LTS:latest                         UbuntuLTS            latest
Debian         credativ                8                   credativ:Debian:8:latest                                        Debian               latest
RHEL           RedHat                  7.3                 RedHat:RHEL:7.3:latest                                          RHEL                 latest
```

### Finding all current images

To obtain the current list of all images, use the `az vm image list` command with the `--all` option. Unlike the Azure CLI 1.0 commands, the `az vm image list --all` command returns all images in **chinanorth** by default (unless you specify a particular `--location` argument), so the `--all` command takes some time to complete. If you intend to investigate interactively, use `az vm image list --all > allImages.json`, which returns a list of all images currently available on Azure and stores it as a file for local use. 

You can specify one of several options to restrict your search to a specific location, offer, publisher, or sku if you already have one or more in mind. If you do not specify a location, the values for **chinanorth** are returned.

### Find specific images

Use `az vm image list` with a filter to find specific information. For example, the following displays the **offer**s that are available for **Debian** (remember that without the `--all` switch, it only searches the local cache of common images):

```azurecli
az vm image list --offer Debian -o table --all
```

The output is something like: 

```
Offer   Publisher   Sku   Urn                              Version
------  ---------   ---   -------------------------------  -------------
Debian  credativ    8     credativ:Debian:8:8.0.201701180  8.0.201701180

<list shortened for the example>
```

You can perform similar filters on the **--publisher** and **--sku** option. You can even perform partial matches on a filter, such as searching for **--offer Deb** to find all Debian images or **--publisher Micr** to find all Microsoft-published images.

If you know where you are deploying, you can use the general image search results along with the `az vm image list-skus`, `az vm image list-offers`, and `az vm image list-publishers` commands to find exactly what you want and where it can be deployed. For example, if from the preceding example you know that `credativ` has a Debian offer, you can then use the `--location` and other options to find exactly what you want. The following example looks for a Debian 8 image in **chinanorth**:

```azurecli
az vm image show -l chinanorth -f debian -p credativ --sku 8 --version 8.0.201701180
```

and the output is:

```json
{
  "dataDiskImages": [],
  "id": "/Subscriptions/<guid>/Providers/Microsoft.Compute/Locations/chinanorth/Publishers/credativ/ArtifactTypes/VMImage/Offers/debian/Skus/8/Versions/8.0.201701180",
  "location": "chinanorth",
  "name": "8.0.201701180",
  "osDiskImage": {
    "operatingSystem": "Linux"
  },
  "plan": null,
  "tags": null
}
```

## Use Azure CLI 1.0 

> [!NOTE]
> This article describes how to navigate and select virtual machine images, using an installation of either the Azure CLI 1.0 or Azure PowerShell that supports the Azure Resource Manager deployment model. As a prerequisite, change to the Resource Manager mode. With the Azure CLI, enter that mode by typing `azure config mode arm`. 
> 

The quickest way to locate an image is to call the `azure vm image list` command and pass the location, the publisher name (it's not case-sensitive!), and an offer -- if you know the offer. For example, the following list is only a short example -- many lists are quite long -- if you know that "Canonical" is a publisher for the "UbuntuServer" offer.

```azurecli
azure vm image list chinanorth canonical ubuntuserver
info:    Executing command vm image list
warn:    The parameter --sku if specified will be ignored
+ Getting virtual machine image skus (Publisher:"canonical" Offer:"ubuntuserver" Location:"chinanorth")
data:    Publisher  Offer         Sku                OS     Version          Location  Urn
data:    ---------  ------------  -----------------  -----  ---------------  --------  --------------------------------------------------------
data:    canonical  ubuntuserver  16.04.0-LTS        Linux  16.04.201604203  chinanorth    canonical:ubuntuserver:16.04.0-LTS:16.04.201604203
data:    canonical  ubuntuserver  16.04.0-LTS        Linux  16.04.201605161  chinanorth    canonical:ubuntuserver:16.04.0-LTS:16.04.201605161
data:    canonical  ubuntuserver  16.04.0-LTS        Linux  16.04.201606100  chinanorth    canonical:ubuntuserver:16.04.0-LTS:16.04.201606100
data:    canonical  ubuntuserver  16.04.0-LTS        Linux  16.04.201606270  chinanorth    canonical:ubuntuserver:16.04.0-LTS:16.04.201606270
data:    canonical  ubuntuserver  16.04.0-LTS        Linux  16.04.201607210  chinanorth    canonical:ubuntuserver:16.04.0-LTS:16.04.201607210
data:    canonical  ubuntuserver  16.04.0-LTS        Linux  16.04.201608150  chinanorth    canonical:ubuntuserver:16.04.0-LTS:16.04.201608150
data:    canonical  ubuntuserver  16.10-DAILY        Linux  16.10.201607220  chinanorth    canonical:ubuntuserver:16.10-DAILY:16.10.201607220
data:    canonical  ubuntuserver  16.10-DAILY        Linux  16.10.201607230  chinanorth    canonical:ubuntuserver:16.10-DAILY:16.10.201607230
data:    canonical  ubuntuserver  16.10-DAILY        Linux  16.10.201607240  chinanorth    canonical:ubuntuserver:16.10-DAILY:16.10.201607240
```

The **Urn** column will be the form you pass to `azure vm quick-create`.

Often, however, you don't yet know what is available. In this case, you can navigate images by using the `azure vm image list-publishers` command and specifying a data center location at the prompt. For example, the following lists all image publishers in the China North location (pass the location argument by lowercasing and removing spaces from the standard locations)

```azurecli
azure vm image list-publishers
info:    Executing command vm image list-publishers
Location: chinanorth
+ Getting virtual machine and/or extension image publishers (Location: "chinanorth")
data:    Publisher                                   Location
data:    ------------------------------------------  ----------
data:    AsiaInfo.DeepSecurity                       chinanorth
data:    AzureChinaMarketplace                       chinanorth
data:    Canonical                                   chinanorth
data:    CoreOS                                      chinanorth
data:    credativ                                    chinanorth
```

These lists can be quite long, so the example list preceding is just a snippet. Let's say that I noticed that Canonical is, indeed, an image publisher in the China North location. You can now find their offers by calling `azure vm image list-offers` and pass the location and the publisher at the prompts, like the following example:

```azurecli
azure vm image list-offers
info:    Executing command vm image list-offers
Location: chinanorth
Publisher: canonical
+ Getting virtual machine image offers (Publisher: "canonical" Location:"chinanorth")
data:    Publisher  Offer         Location
data:    ---------  ------------  ----------
data:    canonical  UbuntuServer  chinanorth
info:    vm image list-offers command OK
```

Now we know that in the China North region, Canonical publishes the **UbuntuServer** offer on Azure. But what SKUs? To get those values, you call `azure vm image list-skus` and respond to the prompt with the location, publisher, and offer that you have discovered.

```azurecli
azure vm image list-skus
info:    Executing command vm image list-skus
Location: chinanorth
Publisher: canonical
Offer: ubuntuserver
+ Getting virtual machine image skus (Publisher:"canonical" Offer:"ubuntuserver" Location:"chinanorth")
data:    Publisher  Offer         sku                Location
data:    ---------  ------------  -----------------  --------
data:    canonical  ubuntuserver  12.04.2-LTS        chinanorth
data:    canonical  ubuntuserver  12.04.3-LTS        chinanorth
data:    canonical  ubuntuserver  12.04.4-LTS        chinanorth
data:    canonical  ubuntuserver  12.04.5-DAILY-LTS  chinanorth
data:    canonical  ubuntuserver  12.04.5-LTS        chinanorth
data:    canonical  ubuntuserver  12.10              chinanorth
data:    canonical  ubuntuserver  14.04-beta         chinanorth
data:    canonical  ubuntuserver  14.04.0-LTS        chinanorth
data:    canonical  ubuntuserver  14.04.1-LTS        chinanorth
data:    canonical  ubuntuserver  14.04.2-LTS        chinanorth
data:    canonical  ubuntuserver  14.04.3-LTS        chinanorth
data:    canonical  ubuntuserver  14.04.3-DAILY-LTS  chinanorth
data:    canonical  ubuntuserver  14.04.3-LTS        chinanorth
data:    canonical  ubuntuserver  14.04.5-DAILY-LTS  chinanorth
data:    canonical  ubuntuserver  14.04.5-LTS        chinanorth
data:    canonical  ubuntuserver  14.10              chinanorth
data:    canonical  ubuntuserver  14.10-beta         chinanorth
data:    canonical  ubuntuserver  14.10-DAILY        chinanorth
data:    canonical  ubuntuserver  15.04              chinanorth
data:    canonical  ubuntuserver  15.04-beta         chinanorth
data:    canonical  ubuntuserver  15.04-DAILY        chinanorth
data:    canonical  ubuntuserver  15.10              chinanorth
data:    canonical  ubuntuserver  15.10-alpha        chinanorth
data:    canonical  ubuntuserver  15.10-beta         chinanorth
data:    canonical  ubuntuserver  15.10-DAILY        chinanorth
data:    canonical  ubuntuserver  16.04-alpha        chinanorth
data:    canonical  ubuntuserver  16.04-beta         chinanorth
data:    canonical  ubuntuserver  16.04.0-DAILY-LTS  chinanorth
data:    canonical  ubuntuserver  16.04.0-LTS        chinanorth
data:    canonical  ubuntuserver  16.10-DAILY        chinanorth
info:    vm image list-skus command OK
```

With this information, you can now find exactly the image you want by calling the original call at the top.

```azurecli
azure vm image list chinanorth canonical ubuntuserver 16.04.0-LTS
info:    Executing command vm image list
+ Getting virtual machine images (Publisher:"canonical" Offer:"ubuntuserver" Sku: "16.04.0-LTS" Location:"chinanorth")
data:    Publisher  Offer         Sku          OS     Version          Location  Urn
data:    ---------  ------------  -----------  -----  ---------------  --------  --------------------------------------------------
data:    canonical  ubuntuserver  16.04.0-LTS  Linux  16.04.201604203  chinanorth    canonical:ubuntuserver:16.04.0-LTS:16.04.201604203
data:    canonical  ubuntuserver  16.04.0-LTS  Linux  16.04.201605161  chinanorth    canonical:ubuntuserver:16.04.0-LTS:16.04.201605161
data:    canonical  ubuntuserver  16.04.0-LTS  Linux  16.04.201606100  chinanorth    canonical:ubuntuserver:16.04.0-LTS:16.04.201606100
data:    canonical  ubuntuserver  16.04.0-LTS  Linux  16.04.201606270  chinanorth    canonical:ubuntuserver:16.04.0-LTS:16.04.201606270
data:    canonical  ubuntuserver  16.04.0-LTS  Linux  16.04.201607210  chinanorth    canonical:ubuntuserver:16.04.0-LTS:16.04.201607210
data:    canonical  ubuntuserver  16.04.0-LTS  Linux  16.04.201608150  chinanorth    canonical:ubuntuserver:16.04.0-LTS:16.04.201608150
info:    vm image list command OK
```

## Next steps
Now you can choose precisely the image you want to use. To create a virtual machine quickly by using the URN information, which you just found, or to use a template with that URN information, see [Create a Linux VM using the Azure CLI](virtual-machines-linux-quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).