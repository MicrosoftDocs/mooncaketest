## <a name="azure-cli"></a> Azure CLI 2.0

Once you have [installed the Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2), use the `az vm image list` command to see a cached list of popular VM images. For example, the following example of the command `az vm image list -o table` displays:

```
You are viewing an offline list of images, use --all to retrieve an up-to-date list
Offer          Publisher               Sku                 Urn                                                             UrnAlias             Version
-------------  ----------------------  ------------------  --------------------------------------------------------------  -------------------  ---------
WindowsServer  MicrosoftWindowsServer  2012-R2-Datacenter  MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest  Win2012R2Datacenter  latest
WindowsServer  MicrosoftWindowsServer  2008-R2-SP1         MicrosoftWindowsServer:WindowsServer:2008-R2-SP1:latest         Win2008R2SP1         latest
WindowsServer  MicrosoftWindowsServer  2012-Datacenter     MicrosoftWindowsServer:WindowsServer:2012-Datacenter:latest     Win2012Datacenter    latest
UbuntuServer   Canonical               14.04.3-LTS         Canonical:UbuntuServer:14.04.3-LTS:latest                       UbuntuLTS            latest
CentOS         OpenLogic               7.2                 OpenLogic:CentOS:7.2:latest                                     CentOS               latest
openSUSE       SUSE                    13.2                SUSE:openSUSE:13.2:latest                                       openSUSE             latest
RHEL           RedHat                  7.2                 RedHat:RHEL:7.2:latest                                          RHEL                 latest
SLES           SUSE                    12-SP1              SUSE:SLES:12-SP1:latest                                         SLES                 latest
Debian         credativ                8                   credativ:Debian:8:latest                                        Debian               latest
CoreOS         CoreOS                  Stable              CoreOS:CoreOS:Stable:latest                                     CoreOS               latest
```

### Finding all current images

To obtain the current list of all images, use the `az vm image list` command with the `--all` option. Unlike the Azure CLI 1.0 commands, the `az vm image list --all` command returns all images in **chinanorth** by default (unless you specify a particular `--location` argument), so the `--all` command takes some time to complete. If you intend to investigate interactively, use `az vm image list --all > allImages.json`, which returns a list of all images currently available on Azure and stores it as a file for local use. 

You can specify one of several options to restrict your search to a specific location, offer, publisher, or sku if you already have one or more in mind. If you do not specify a location, the values for **chinanorth** are returned.

### Find specific images

Use `az vm image list` with a [JMESPATH query filter](https://docs.microsoft.com/cli/azure/query-az-cli2) to find specific information. For example, the following displays the **sku**s that are available for **Debian** (remember that without the `--all` switch, it only searches the local cache of common images):

```azurecli
az vm image list --query '[?contains(offer,`Debian`)]' -o table --all
```

The output is something like: 

```
You are viewing an offline list of images, use --all to retrieve an up-to-date list
  Sku  Publisher    Offer    Urn                       Version    UrnAlias
-----  -----------  -------  ------------------------  ---------  ----------
    8  credativ     Debian   credativ:Debian:8:latest  latest     Debian

<list shortened for the example>
```

If you know where you are deploying, you can use the general image search results along with the `az vm image list-skus`, `az vm image list-offers`, and `az vm image list-publishers` commands to find exactly what you want and where it can be deployed. For example, if from the preceding example you know that `credativ` has a Debian offer, you can then use the `--location` and other options to find exactly what you want. The following example looks for a Debian 8 image in **chinanorth**:

```azurecli
az vm image show -l chinanorth -f debian -p credativ --skus 8 --version 8.0.201701180
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

## Azure CLI 1.0 

> [!NOTE]
> This article describes how to navigate and select virtual machine images, using an installation of either the Azure CLI 1.0 or Azure PowerShell that supports the Azure resource manager deployment model. As a prerequisite, change to the Resource Manager mode. With the Azure CLI, enter that mode by typing `azure config mode arm`. 
> 

The quickest way to locate an image is to call the `azure vm image list` command and pass the location, the publisher name (it's not case-sensitive!), and an offer -- if you know the offer. For example, the following list is only a short example -- many lists are quite long -- if you know that "Canonical" is a publisher for the "UbuntuServer" offer.

```azurecli
azure vm image list chinanorth canonical ubuntuserver
info:    Executing command vm image list
warn:    The parameter --sku if specified will be ignored
+ Getting virtual machine image skus (Publisher:"canonical" Offer:"ubuntuserver" Location:"chinanorth")
data:    Publisher  Offer         Sku              OS     Version          Location    Urn
data:    ---------  ------------  -----------  -----  ---------------  ----------  --------------------------------------------------
data:    canonical  ubuntuserver  12.04.5-LTS     Linux  12.04.201601140  chinanorth    canonical:ubuntuserver:12.04.5-LTS:12.04.201601140
data:    canonical  ubuntuserver  12.04.5-LTS     Linux  12.04.201602010  chinanorth    canonical:ubuntuserver:12.04.5-LTS:12.04.201602010
data:    canonical  ubuntuserver  12.04.5-LTS    Linux  12.04.201606270  chinanorth    canonical:ubuntuserver:12.04.5-LTS:12.04.201606270
data:    canonical  ubuntuserver  12.04.5-LTS    Linux  12.04.201610201  chinanorth    canonical:ubuntuserver:12.04.5-LTS:12.04.201610201
data:    canonical  ubuntuserver  14.04.2-LTS    Linux  14.04.201507060  chinanorth    canonical:ubuntuserver:14.04.2-LTS:14.04.201507060
data:    canonical  ubuntuserver  14.04.3-LTS    Linux  14.04.201510190  chinanorth    canonical:ubuntuserver:14.04.3-LTS:14.04.201510190
data:    canonical  ubuntuserver  14.04.3-LTS    Linux  14.04.201601190  chinanorth    canonical:ubuntuserver:14.04.3-LTS:14.04.201601190
data:    canonical  ubuntuserver  14.04.3-LTS    Linux  14.04.201602010  chinanorth    canonical:ubuntuserver:14.04.3-LTS:14.04.201602010
data:    canonical  ubuntuserver  14.04.3-LTS    Linux  14.04.201602171  chinanorth    canonical:ubuntuserver:14.04.3-LTS:14.04.201602171
data:    canonical  ubuntuserver  14.04.3-LTS    Linux  14.04.201602220  chinanorth    canonical:ubuntuserver:14.04.3-LTS:14.04.201602220
data:    canonical  ubuntuserver  14.04.3-LTS    Linux  14.04.201603140  chinanorth    canonical:ubuntuserver:14.04.3-LTS:14.04.201603140
data:    canonical  ubuntuserver  14.04.3-LTS    Linux  14.04.201604060  chinanorth    canonical:ubuntuserver:14.04.3-LTS:14.04.201604060
data:    canonical  ubuntuserver  14.04.3-LTS    Linux  14.04.201606270  chinanorth    canonical:ubuntuserver:14.04.3-LTS:14.04.201606270
data:    canonical  ubuntuserver  14.04.4-LTS    Linux  14.04.201610200  chinanorth    canonical:ubuntuserver:14.04.4-LTS:14.04.201610200
data:    canonical  ubuntuserver  14.04.5-LTS    Linux  14.04.201610200  chinanorth    canonical:ubuntuserver:14.04.5-LTS:14.04.201610200
data:    canonical  ubuntuserver  16.04.0-LTS      Linux  16.04.201606270  chinanorth    canonical:ubuntuserver:16.04.0-LTS:16.04.201606270
data:    canonical  ubuntuserver  16.04.0-LTS      Linux  16.04.201610200  chinanorth    canonical:ubuntuserver:16.04.0-LTS:16.04.201610200
data:    canonical  ubuntuserver  16.10          Linux  16.10.201610201  chinanorth    canonical:ubuntuserver:16.10:16.10.201610201
```

The **Urn** column will be the form you pass to `azure vm quick-create`.

Often, however, you don't yet know what is available. In this case, you can navigate images by using the `azure vm image list-publishers` command and specifying a data center location at the prompt. For example, the following lists all image publishers in the China North location (pass the location argument by lowercasing and removing spaces from the standard locations)

```azurecli
azure vm image list-publishers
info:    Executing command vm image list-publishers
Location: chinanorth
+ Getting virtual machine and/or extension image publishers (Location: "chinanorth")
data:    Publisher                                        Location
data:    -----------------------------------------------  ----------
data:    AsiaInfo.DeepSecurity                            chinanorth
data:    Canonical                                        chinanorth
data:    CoreOS                                           chinanorth
data:    credativ                                         chinanorth
data:    Microsoft.Azure.Diagnostics                      chinanorth
data:    Microsoft.Azure.Extensions                       chinanorth
data:    Microsoft.Azure.RecoveryServices                 chinanorth
data:    Microsoft.Azure.Security                         chinanorth
data:    Microsoft.AzureCAT.AzureEnhancedMonitoring       chinanorth
data:    Microsoft.AzureCAT.Test.AzureEnhancedMonitoring  chinanorth
data:    Microsoft.Compute                                chinanorth
data:    Microsoft.HpcPack                                chinanorth
data:    Microsoft.OSTCExtensions                         chinanorth
data:    Microsoft.OSTCExtensions1                        chinanorth
data:    Microsoft.Powershell                             chinanorth
data:    Microsoft.Powershell.Test                        chinanorth
data:    Microsoft.SqlServer.Management                   chinanorth
data:    Microsoft.VisualStudio.Azure.RemoteDebug         chinanorth
data:    MicrosoftOSTC                                    chinanorth
data:    MicrosoftSQLServer                               chinanorth
data:    MicrosoftWindowsServer                           chinanorth
data:    MicrosoftWindowsServerHPCPack                    chinanorth
data:    MSOpenTech.Extensions                            chinanorth
data:    OpenLogic                                        chinanorth
data:    SUSE                                             chinanorth
data:    TrendMicro.DeepSecurity                          chinanorth
```

These lists can be quite long, so the example list preceding is just a snippet. Let's say that I noticed that Canonical is, indeed, an image publisher in the China North location. You can now find their offers by calling `azure vm image list-offers` and pass the location and the publisher at the prompts, like the following example:

```azurecli
azure vm image list-offers
info:    Executing command vm image list-offers
Location: chinanorth
Publisher: canonical
+ Getting virtual machine image offers (Publisher: "canonical" Location:"chinanorth")
data:    Publisher  Offer                      Location
data:    ---------  -------------------------  --------
data:    canonical  UbuntuServer               chinanorth
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
data:    canonical  ubuntuserver  12.04.5-LTS        chinanorth
data:    canonical  ubuntuserver  14.04.2-LTS        chinanorth
data:    canonical  ubuntuserver  14.04.3-LTS        chinanorth
data:    canonical  ubuntuserver  14.04.4-LTS        chinanorth
data:    canonical  ubuntuserver  14.04.5-LTS        chinanorth
data:    canonical  ubuntuserver  14.10              chinanorth
data:    canonical  ubuntuserver  15.04              chinanorth
data:    canonical  ubuntuserver  15.10              chinanorth
data:    canonical  ubuntuserver  16.04.0-LTS        chinanorth
data:    canonical  ubuntuserver  16.10              chinanorth
info:    vm image list-skus command OK
```

With this information, you can now find exactly the image you want by calling the original call at the top.

```azurecli
azure vm image list chinanorth canonical ubuntuserver 16.04.0-LTS
info:    Executing command vm image list
+ Getting virtual machine images (Publisher:"canonical" Offer:"ubuntuserver" Sku: "16.04.0-LTS" Location:"chinanorth")
data:    Publisher  Offer         Sku          OS     Version          Location  Urn
data:    ---------  ------------  -----------  -----  ---------------  --------  --------------------------------------------------
data:    canonical  ubuntuserver  16.04.0-LTS  Linux  16.04.201606270  chinanorth    canonical:ubuntuserver:16.04.0-LTS:16.04.201606270
info:    vm image list command OK
```

Now you can choose precisely the image you want to use. To create a virtual machine quickly by using the URN information, which you just found, or to use a template with that URN information, see [Using the Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](../articles/xplat-cli-azure-resource-manager.md).

## <a name="powershell"></a> PowerShell
> [!NOTE]
> Install and configure the [latest Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs). If you are using Azure PowerShell modules below 1.0, you still use the following commands but you must first `Switch-AzureMode AzureResourceManager`. 
> 
> 

When creating a new virtual machine with Azure Resource Manager, in some cases you need to specify an image with the combination of the following image properties:

* Publisher
* Offer
* SKU

For example, these values are needed for the `Set-AzureRMVMSourceImage` PowerShell cmdlet or with a resource group template file in which you must specify the type of virtual machine to be created.

If you need to determine these values, you can navigate the images to determine these values:

1. List the image publishers.
2. For a given publisher, list their offers.
3. For a given offer, list their SKUs.

First, list the publishers with the following commands:

```powershell
$locName="<Azure location, such as China North>"
Get-AzureRMVMImagePublisher -Location $locName | Select PublisherName
```

Fill in your chosen publisher name and run the following commands:

```powershell
$pubName="<publisher>"
Get-AzureRMVMImageOffer -Location $locName -Publisher $pubName | Select Offer
```

Fill in your chosen offer name and run the following commands:

```powershell
$offerName="<offer>"
Get-AzureRMVMImageSku -Location $locName -Publisher $pubName -Offer $offerName | Select Skus
```

From the display of the `Get-AzureRMVMImageSku` command, you have all the information you need to specify the image for a new virtual machine.

The following shows a full example:

```powershell
PS C:\> $locName="China North"
PS C:\> Get-AzureRMVMImagePublisher -Location $locName | Select PublisherName

PublisherName
-------------
Canonical
CoreOS
credativ
...
```

For the "MicrosoftWindowsServer" publisher:

```powershell
PS C:\> $pubName="MicrosoftWindowsServer"
PS C:\> Get-AzureRMVMImageOffer -Location $locName -Publisher $pubName | Select Offer

Offer
-----
WindowsServer
```

For the "WindowsServer" offer:

```powershell
PS C:\> $offerName="WindowsServer"
PS C:\> Get-AzureRMVMImageSku -Location $locName -Publisher $pubName -Offer $offerName | Select Skus

Skus
----
2008-R2-SP1
2008-R2-SP1-zhcn
2012-Datacenter
2012-Datacenter-zhcn
2012-R2-Datacenter
2012-R2-Datacenter-zhcn
2016-Nano-Server-Technical-Preview
2016-Technical-Preview-with-Containers
Windows-Server-Technical-Preview
```

From this list, copy the chosen SKU name, and you have all the information for the `Set-AzureRMVMSourceImage` PowerShell cmdlet or for a resource group template.

<!--Image references-->
[5]: ./media/markdown-template-for-new-articles/octocats.png
[6]: ./media/markdown-template-for-new-articles/pretty49.png
[7]: ./media/markdown-template-for-new-articles/channel-9.png
[8]: ./media/markdown-template-for-new-articles/copytemplate.png

<!--Reference style links - using these makes the source content way more readable than using inline links-->
[gog]: http://google.com/
[yah]: http://search.yahoo.com/  
[msn]: http://search.msn.com/