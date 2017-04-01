---
title: Web Apps overview | Azure
description: Learn how Azure App Service helps you develop and host web applications
services: app-service\web
documentationcenter: ''
author: cephalin
manager: erikre
editor: ''

ms.assetid: 94af2caf-a2ec-4415-a097-f60694b860b3
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/04/2017
wacn.date: ''
ms.author: cephalin

---
# Web Apps overview
*App Service Web Apps* is a fully managed compute platform that is optimized for hosting websites and web applications. This [platform-as-a-service](https://zh.wikipedia.org/wiki/平台即服务) (PaaS) offering of Azure lets you focus on your business logic while Azure takes care of the infrastructure to run and scale your apps.

## What is a web app in App Service?
In App Service, a *web app* is the compute resources that Azure provides for hosting a website or web application.  

The compute resources may be on shared or dedicated virtual machines (VMs), depending on the pricing tier that you choose. Your application code runs in a managed VM that is isolated from other customers.

Your code can be in any language or framework that is supported by [Azure App Service](../app-service/app-service-value-prop-what-is.md), such as ASP.NET, Node.js, Java, PHP, or Python. You can also run scripts that use [PowerShell and other scripting languages](web-sites-create-web-jobs.md#acceptablefiles) in a web app.

For examples of typical application scenarios that you can use Web Apps for, see the **Scenarios and recommendations** section of [Azure App Service, Virtual Machines, Service Fabric, and Cloud Services comparison](choose-web-site-cloud-service-vm.md#scenarios).

## Why use Web Apps?
Here are some key features of App Service that apply to Web Apps:

* **Multiple languages and frameworks** - App Service has first-class support for ASP.NET, Node.js, Java, PHP, and Python. You can also run [PowerShell and other scripts or executables](web-sites-create-web-jobs.md) on App Service VMs.
* **DevOps optimization** - Set up [continuous integration and deployment](app-service-continuous-deployment.md) with GitHub. Promote updates through [test and staging environments](web-sites-staged-publishing.md). Perform [A/B testing](app-service-web-test-in-production-get-start.md). Manage your apps in App Service by using [Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs) or the [cross-platform command-line interface (CLI)](../cli-install-nodejs.md).
* **Global scale with high availability** - Scale [up](web-sites-scale.md) or [out](../monitoring-and-diagnostics/insights-how-to-scale.md) manually or automatically. Host your apps anywhere in Azure.cn's national datacenter infrastructure, and the App Service [SLA](https://www.azure.cn/support/sla/app-service/) promises high availability.
* **Connections to SaaS platforms and on-premises data** - Choose from more than 50 connectors for enterprise systems (such as SAP, Siebel, and Oracle), SaaS services (such as Salesforce and Office 365), and internet services. Access on-premises data using [Azure Virtual Networks](app-service-vnet-integration-powershell.md).
* **Security and compliance** - App Service is [ISO, SOC, and PCI compliant](https://www.trustcenter.cn/).
* **Visual Studio integration** - Dedicated tools in Visual Studio streamline the work of creating, deploying, and debugging.

In addition, a web app can take advantage of features offered by [API Apps](../app-service-api/app-service-api-apps-why-best-platform.md) (such as CORS support) and [Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) (such as push notifications). For more information about app types in App Service, see [Azure App Service overview](../app-service/app-service-value-prop-what-is.md).

Besides Web Apps in App Service, Azure offers other services that can be used for hosting websites and web applications. For most scenarios, Web Apps is the best choice.  For microservice architecture, consider [Service Fabric](/azure/service-fabric), and if you need more control over the VMs that your code runs on, consider [Azure Virtual Machines](/azure/virtual-machines/). For more information about how to choose between these Azure services, see [Azure App Service, Virtual Machines, Service Fabric, and Cloud Services comparison](choose-web-site-cloud-service-vm.md).

## Getting started
To get started by deploying sample code to a new web app in App Service, follow one of the tutorials in the following dropdown box. You'll need a trial Azure account.

> [!div class="op_single_selector"]
> * [Deploy your first HTML site to Azure in 5 minutes](app-service-web-get-started-html-cli-nodejs.md)
> * [Deploy your first ASP.NET web app to Azure in 5 minutes](app-service-web-get-started-dotnet-cli-nodejs.md)
> * [Deploy your first PHP web app to Azure in 5 minutes](app-service-web-get-started-php-cli-nodejs.md)
> * [Deploy your first Node.js web app to Azure in 5 minutes](app-service-web-get-started-nodejs-cli-nodejs.md)
> * [Deploy your first Python web app to Azure in 5 minutes](app-service-web-get-started-python-cli-nodejs.md)
> * [Deploy your first Java web app to Azure in 5 minutes](app-service-web-get-started-java.md)
> 
> 
