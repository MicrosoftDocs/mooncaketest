> [!NOTE]
> In order to use the China Cloud Environment, the following Azure PowerShell commands need to add **"-Environment AzureChinaCloud"** parameter.<br />
>	`Add-AzureAccount` <br />
>	`Get-AzurePublishSettingsFile` <br />
>	`Import-AzurePublishSettingsFile` <br />
>	`New-AzureProfile` <br />
>	`New-AzureStorageContext` <br />
>	`Set-AzureSubscription` <br />
>	`Show-AzurePortal` <br />
>For example, `Add-AzureAccount -Credential $Cred -ErrorAction Stop` should become `Add-AzureAccount -Credential $Cred -ErrorAction Stop -Environment AzureChinaCloud`
>