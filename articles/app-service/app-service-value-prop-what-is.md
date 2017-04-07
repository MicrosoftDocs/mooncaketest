---
title: Azure App Service for web, mobile, and API apps | Azure
description: Learn how Azure App Service helps you develop, deploy, and manage web and mobile apps.
keywords: app service, azure app service, app service cost, scale, scalable, app deployment, azure app deployment, paas, platform-as-a-service, website, web site, web, azure mobile
services: app-service
documentationcenter: ''
author: omarkmsft
manager: erikre
editor: cephalin

ms.assetid: 979cafa8-eeb6-4d3b-87cf-764a821c3e4f
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 12/02/2016
wacn.date: ''
ms.author: byvinyal

---
# What is Azure App Service?
*App Service* is a [platform-as-a-service](https://zh.wikipedia.org/wiki/平台即服务) (PaaS) offering of Azure. Create web and mobile apps for any platform or device. Integrate your apps with SaaS solutions, connect with on-premises applications, and automate your business processes. Azure runs your apps on fully managed virtual machines (VMs), with your choice of shared VM resources or dedicated VMs.

App Service includes the web and mobile capabilities that we previously delivered separately as Azure Websites and Azure Mobile Services. It also includes new capabilities for automating business processes and hosting cloud APIs. As a single integrated service, App Service lets you compose various components -- websites, mobile app back ends, RESTful APIs, and business processes -- into a single solution.

## Why use App Service?
Here are some key features and capabilities of App Service:

* **Multiple languages and frameworks** - App Service has first-class support for ASP.NET, Node.js, Java, PHP, and Python. You can also run [Windows PowerShell and other scripts or executables](../app-service-web/web-sites-create-web-jobs.md) on App Service VMs.
* **DevOps optimization** - Set up [continuous integration and deployment](../app-service-web/app-service-continuous-deployment.md) with GitHub. Promote updates through [test and staging environments](../app-service-web/web-sites-staged-publishing.md). Perform [A/B testing](../app-service-web/app-service-web-test-in-production-get-start.md). Manage your apps in App Service by using [Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs) or the [cross-platform command-line interface (CLI)](../cli-install-nodejs.md).
* **Global scale with high availability** - Scale [up](../app-service-web/web-sites-scale.md) or [out](../monitoring-and-diagnostics/insights-how-to-scale.md) manually or automatically. Host your apps anywhere in Azure China's datacenter infrastructure, and the App Service [SLA](https://www.azure.cn/support/sla/app-service/) promises high availability.
* **Connections to SaaS platforms and on-premises data** - Choose from more than 50 connectors for enterprise systems (such as SAP, Siebel, and Oracle), SaaS services (such as Salesforce and Office 365), and internet services (such as Facebook and Twitter). Access on-premises data using [Azure Virtual Networks](../app-service-web/app-service-vnet-integration-powershell.md).
* **Security and compliance** - App Service is [ISO, SOC, and PCI compliant](https://www.trustcenter.cn/).
* **Visual Studio integration** - Dedicated tools in Visual Studio streamline the work of creating, deploying, and debugging.

## App types in App Service
App Service offers several *app types*, each of which is intended to host a specific workload:

* [**Web Apps**](../app-service-web/app-service-web-overview.md) - For hosting websites and web applications.
* [**Mobile Apps**](../app-service-mobile/app-service-mobile-value-prop.md) For hosting mobile app back ends.
* [**API Apps**](../app-service-api/app-service-api-apps-why-best-platform.md) - For hosting RESTful APIs.

The word *app* here refers to the hosting resources dedicated to running a workload. Taking "web app" as an example, you're probably accustomed to thinking of a web app as both the compute resources and application code that together deliver functionality to a browser. But in App Service a *web app* is the compute resources that Azure provides for hosting your application code. 

Your application may be composed of multiple App Service apps of different kinds. For example If your application is composed of a web front end and a RESTful API back end you could:

- Deploy both (front end and api) to a single web app  
- Deploy your front-end code to a web app and your back-end code to an API app. 

## App Service plans
[App Service plans](azure-web-sites-web-hosting-plans-in-depth-overview.md) represent the collection of physical resources used to host your apps.

App Service plans define:

- **Region** (China North, China East)
- **Scale count** (one, two, three instances, etc.)
- **Instance size** (Small, Medium, Large)
- **SKU** (Free, Shared, Basic, Standard, Premium)

All applications assigned to an **App Service plan** share the resources defined by it allowing you to save cost when hosting multiple apps.

Your **App Service plan** can scale from **Free** and **Shared** SKUs to **Basic**, **Standard**, and **Premium** SKUs giving you access to more resources and features along the way. Once your App Service Plan is set to **Basic** or higher you can also control the **size** and scale count of the VMs.

The **SKU** and **Scale** of the App Service plan determines the cost and not the number of apps hosted in it. 

## Pricing
For information about how much App Service costs, see [App Service Pricing](https://www.azure.cn/pricing/details/app-service/).

## Test-drive App Service

Open a [trial Azure account](https://www.azure.cn/pricing/1rmb-trial/), and try one of our getting-started tutorials:

* [Tutorial: Create a web app](../app-service-web/app-service-web-get-started.md)
* [Tutorial: Create a mobile app](../app-service-mobile/app-service-mobile-android-get-started.md)
* [Tutorial: Create an API app](../app-service-api/app-service-api-dotnet-get-started.md)