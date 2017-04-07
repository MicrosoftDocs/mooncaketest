---
title: Create network security groups - Azure Resource Manager Template| Azure
description: Learn how to create and deploy network security groups using an Azure Resource Manager template.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager

ms.assetid: f3e7385d-717c-44ff-be20-f9aa450aa99b
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
wacn.date: ''
ms.author: jdial
ms.custom: H1Hack27Feb2017

---
# Create network security groups using an Azure Resource Manager template

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

This article covers the Resource Manager deployment model. You can also [create NSGs in the classic deployment model](virtual-networks-create-nsg-classic-ps.md).

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

## NSG resources in a template file
You can view and download the [sample template](https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/NSGs.json).

The following section shows the definition of the front-end NSG, based on the scenario.

```json
"apiVersion": "2015-06-15",
"type": "Microsoft.Network/networkSecurityGroups",
"name": "[parameters('frontEndNSGName')]",
"location": "[resourceGroup().location]",
"tags": {
  "displayName": "NSG - Front End"
},
"properties": {
  "securityRules": [
    {
      "name": "rdp-rule",
      "properties": {
        "description": "Allow RDP",
        "protocol": "Tcp",
        "sourcePortRange": "*",
        "destinationPortRange": "3389",
        "sourceAddressPrefix": "Internet",
        "destinationAddressPrefix": "*",
        "access": "Allow",
        "priority": 100,
        "direction": "Inbound"
      }
    },
    {
      "name": "web-rule",
      "properties": {
        "description": "Allow WEB",
        "protocol": "Tcp",
        "sourcePortRange": "*",
        "destinationPortRange": "80",
        "sourceAddressPrefix": "Internet",
        "destinationAddressPrefix": "*",
        "access": "Allow",
        "priority": 101,
        "direction": "Inbound"
      }
    }
  ]
}
```

To associate the NSG to the front-end subnet, you have to change the subnet definition in the template, and use the reference id for the NSG.

```json
"subnets": [
  {
    "name": "[parameters('frontEndSubnetName')]",
    "properties": {
      "addressPrefix": "[parameters('frontEndSubnetPrefix')]",
      "networkSecurityGroup": {
      "id": "[resourceId('Microsoft.Network/networkSecurityGroups', parameters('frontEndNSGName'))]"
      }
    }
  }, 
```

Notice the same being done for the back-end NSG and the back-end subnet in the template.

## Deploy the ARM template by using PowerShell
To deploy the ARM template you downloaded by using PowerShell, follow the steps below.

1. If you have never used Azure PowerShell, follow the instructions in the [How to Install and Configure Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs) to install and configure it.
2. Run the **`New-AzureRmResourceGroup`** cmdlet to create a resource group using the template.

    ```powershell
    New-AzureRmResourceGroup -Name TestRG -Location chinanorth `
    -TemplateFile 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.json' `
    -TemplateParameterFile 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.parameters.json'
    ```

    Expected output:

        ResourceGroupName : TestRG
        Location          : chinanorth
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
                            Actions  NotActions
                            =======  ==========
                            *                  

        Resources         :
                            Name                Type                                     Location
                            ==================  =======================================  ========
                            sqlAvSet            Microsoft.Compute/availabilitySets       chinanorth  
                            webAvSet            Microsoft.Compute/availabilitySets       chinanorth  
                            SQL1                Microsoft.Compute/virtualMachines        chinanorth  
                            SQL2                Microsoft.Compute/virtualMachines        chinanorth  
                            Web1                Microsoft.Compute/virtualMachines        chinanorth  
                            Web2                Microsoft.Compute/virtualMachines        chinanorth  
                            TestNICSQL1         Microsoft.Network/networkInterfaces      chinanorth  
                            TestNICSQL2         Microsoft.Network/networkInterfaces      chinanorth  
                            TestNICWeb1         Microsoft.Network/networkInterfaces      chinanorth  
                            TestNICWeb2         Microsoft.Network/networkInterfaces      chinanorth  
                            NSG-BackEnd         Microsoft.Network/networkSecurityGroups  chinanorth  
                            NSG-FrontEnd        Microsoft.Network/networkSecurityGroups  chinanorth  
                            TestPIPSQL1         Microsoft.Network/publicIPAddresses      chinanorth  
                            TestPIPSQL2         Microsoft.Network/publicIPAddresses      chinanorth  
                            TestPIPWeb1         Microsoft.Network/publicIPAddresses      chinanorth  
                            TestPIPWeb2         Microsoft.Network/publicIPAddresses      chinanorth  
                            TestVNet            Microsoft.Network/virtualNetworks        chinanorth  
                            testvnetstorageprm  Microsoft.Storage/storageAccounts        chinanorth  
                            testvnetstoragestd  Microsoft.Storage/storageAccounts        chinanorth  

        ResourceId        : /subscriptions/[Subscription Id]/resourceGroups/TestRG

## Deploy the ARM template by using the Azure CLI
To deploy the ARM template by using the Azure CLI, follow the steps below.

1. If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.
2. Run the **`azure config mode`** command to switch to Resource Manager mode, as shown below.

    ```azurecli
    azure config mode arm
    ```

    The following is the expected output for the command:

        info:    New mode is arm

3. Run the **`azure group deployment create`** cmdlet to deploy the new VNet by using the template and parameter files you downloaded and modified above. The list shown after the output explains the parameters used.

    ```azurecli
    azure group create -n TestRG -l chinanorth -f 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.json' -e 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.parameters.json'
    ```

    Expected output:

        info:    Executing command group create
        info:    Getting resource group TestRG
        info:    Creating resource group TestRG
        info:    Created resource group TestRG
        info:    Initializing template configurations and parameters
        info:    Creating a deployment
        info:    Created template deployment "azuredeploy"
        data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG
        data:    Name:                TestRG
        data:    Location:            chinanorth
        data:    Provisioning State:  Succeeded
        data:    Tags: null
        data:    
        info:    group create command OK

    * **-n (or --name)**. Name of the resource group to be created.
    * **-l (or --location)**. Azure region where the resource group will be created.
    * **-f (or --template-file)**. Path to your ARM template file.
    * **-e (or --parameters-file)**. Path to your ARM parameters file.