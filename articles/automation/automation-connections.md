---
title: Connection assets in Azure Automation | Azure
description: Connection assets in Azure Automation contain the information required to connect to an external service or application from a runbook. This article explains the details of connections and how to work with them in both textual and graphical authoring.
services: automation
documentationcenter: ''
author: mgoedtel
manager: jwhit
editor: tysonn

ms.assetid: f0239017-5c66-4165-8cca-5dcb249b8091
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/13/2017
wacn.date: ''
ms.author: magoedte; bwren
---

# Connection assets in Azure Automation

An Automation connection asset contains the information required to connect to an external service or application from a runbook. This may include information required for authentication such as a username and password in addition to connection information such as a URL or a port. The value of a connection is keeping all of the properties for connecting to a particular application in one asset as opposed to creating multiple variables. The user can edit the values for a connection in one place, and you can pass the name of a connection to a runbook in a single parameter. The properties for a connection can be accessed in the runbook with the **Get-AutomationConnection** activity.

When you create a connection, you must specify a *connection type*. The connection type is a template that defines a set of properties. The connection defines values for each property defined in its connection type. Connection types are added to Azure Automation in integration modules or created with the [Azure Automation API](http://msdn.microsoft.com/zh-cn/library/azure/mt163818.aspx). The only connection types that are available when you create a connection are those installed in your Automation account.

>[!NOTE] 
>Secure assets in Azure Automation include credentials, certificates, connections, and encrypted variables. These assets are encrypted and stored in the Azure Automation using a unique key that is generated for each automation account. This key is encrypted by a master certificate and stored in Azure Automation. Before storing a secure asset, the key for the automation account is decrypted using the master certificate and then used to encrypt the asset.

## Windows PowerShell Cmdlets

The cmdlets in the following table are used to create and manage Automation connections with Windows PowerShell. They ship as part of the [Azure PowerShell module](https://docs.microsoft.com/powershell/azureps-cmdlets-docs) which is available for use in Automation runbooks.

|Cmdlet|Description|
|:---|:---|
|[Get-AzureAutomationConnection](https://docs.microsoft.com/zh-cn/powershell/servicemanagement/azure.automation/v1.6.1/Get-AzureAutomationConnection)|Retrieves a connection. Includes a hash table with the values of the connection's fields.|
|[New-AzureAutomationConnection](https://docs.microsoft.com/zh-cn/powershell/servicemanagement/azure.automation/v1.6.1/New-AzureAutomationConnection)|Creates a new connection.|
|[Remove-AzureAutomationConnection](https://docs.microsoft.com/zh-cn/powershell/servicemanagement/azure.automation/v1.6.1/Remove-AzureAutomationConnection)|Remove an existing connection.|
|[Set-AzureAutomationConnectionFieldValue](https://docs.microsoft.com/zh-cn/powershell/servicemanagement/azure.automation/v1.6.1/Set-AzureAutomationConnectionFieldValue?redirectedfrom=msdn) |Sets the value of a particular field for an existing connection.|

## Activities

The activities in the following table are used to access connections in a runbook.

|Activities|Description|
|---|---|
|[Get-AutomationConnection](https://docs.microsoft.com/powershell/servicemanagement/azure.automation/v1.6.1/Get-AzureAutomationConnection?redirectedfrom=msdn)|Gets a connection to use. Returns a hash table with the properties of the connection.|

>[!NOTE] 
>You should avoid using variables with the -Name parameter of **Get- AutomationConnection** since this can complicate discovering dependencies between runbooks and connection assets at design time.

## Creating a New Connection

### To create a new connection with the Azure Classic Management Portal

1. From your automation account, click **Assets** at the top of the window.
2. At the bottom of the window, click **Add Setting**.
3. Click **Add Connection**.
4. In the **Connection Type** dropdown, select the type of connection you want to create.  The wizard will present the properties for that particular type.
5. Complete the wizard and click the checkbox to save the new connection.

### To create a new connection with Windows PowerShell

Create a new connection with Windows PowerShell using the [New-AzureAutomationConnection](https://docs.microsoft.com/zh-cn/powershell/servicemanagement/azure.automation/v1.6.1/New-AzureAutomationConnection) cmdlet. This cmdlet has a parameter named **ConnectionFieldValues** that expects a [hash table](http://technet.microsoft.com/zh-cn/library/hh847780.aspx) defining values for each of the properties defined by the connection type.

The following sample commands create a new connection for [Twilio](http://www.twilio.com) which is a telephony service that allows you to send and receive text messages.  A sample integration module that includes a Twilio connection type is available in [Script Center](http://gallery.technet.microsoft.com/scriptcenter/Twilio-PowerShell-Module-8a8bfef8).  This connection type defines properties for Account SID and Authorization Token, which are required to validate your account when connecting to Twilio.  You must [download this module](http://gallery.technet.microsoft.com/scriptcenter/Twilio-PowerShell-Module-8a8bfef8) and install it in your automation account for this sample code to work.

    $AccountSid = "DAf5fed830c6f8fac3235c5b9d58ed7ac5"
    $AuthToken  = "17d4dadfce74153d5853725143c52fd1"
    $FieldValues = @{"AccountSid" = $AccountSid;"AuthToken"=$AuthToken}

    New-AzureAutomationConnection -AutomationAccountName "MyAutomationAccount" -Name "TwilioConnection" -ConnectionTypeName "Twilio" -ConnectionFieldValues $FieldValues

## Using a connection in a runbook
You retrieve a connection in a runbook with the **Get-AutomationConnection** cmdlet.  This activity retrieves the values of the different fields in the connection and returns them as a [hash table](https://technet.microsoft.com/zh-cn/library/hh847780.aspx) which can then be used with the appropriate commands in the runbook.

### Textual runbook sample

The following sample commands show how to use the Run As account mentioned earlier, to authenticate with Azure Resource Manager resources in your runbook.  It uses the connection asset representing the Run As account, which references the certificate-based service principal, not credentials.  

    $Conn = Get-AutomationConnection -Name AzureRunAsConnection 
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID -ApplicationId $Conn.ApplicationID -CertificateThumbprint

