## Overview of Azure Resource Manager templates

>[!NOTE]
> Templates you downloaded from the GitHub Repo "azure-quickstart-templates" must be modified in order to fit in the Azure China Cloud Environment. For example, replace some endpoints -- "blob.core.windows.net" by "blob.core.chinacloudapi.cn", "cloudapp.azure.com" by "chinacloudapp.cn"; change some unsupported VM images; and, changes some unsupported VM sizes.

Azure Resource Manager templates allows you to declaratively specify the Azure IaaS infrastructure in JSON language by defining the dependencies between resources.

See  [Authoring extension templates](../articles/virtual-machines/virtual-machines-windows-extensions-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) to learn more about authoring templates for using extensions.

In this article we'll learn about troubleshooting some of the common VM extension failures.