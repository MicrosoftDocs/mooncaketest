---
title: Azure App Service and its impact on existing Azure services
description: Explains how the new Azure App Service and its features impact existing services in Azure.
services: app-service
documentationcenter: ''
author: yochay
manager: nirma
editor: ''

ms.assetid: 86c6a292-3c33-49f4-890c-89cc0321b397
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/12/2016
wacn.date: ''
ms.author: yochaykk

---
# Azure App Service and existing Azure services
This article outlines the changes to existing Azure services as part of the change to bring together several Azure services into [Azure App Service](https://www.azure.cn/home/features/app-service/), a new integrated offering.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## Overview
[Azure App Service](https://www.azure.cn/home/features/app-service/) is a new and unique cloud service that enables developers to create web and mobile apps for any platform and any device. App Service is an integrated solution designed to streamline repeated coding functions, integrate with enterprise and SaaS systems, and automate business processes while meeting your needs for security, reliability, and scalability.

App Service brings together the following existing Azure services - [Websites](https://www.azure.cn/home/features/app-service/web-apps/) and [Mobile Services](https://www.azure.cn/home/features/mobile-services/) into a single combined service, while adding powerful new capabilities.  App Service allows you to host the following app types:

* Web Apps
* Mobile Apps
* API Apps

The following table explains how existing Azure services map to App Service and the app types available within it.

<table>
<thead>
<tr class="header">
<th align="left", style="width:10%">Existing Azure Service</th>
<th align="left", style="width:10%">Azure App Service</th>
<th align="left", style="width:80%">What changed</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">Azure Websites</td>
<td align="left">Web Apps</td>
<td align="left"><li>For Azure Websites, App Service is strictly limited to changing the name  Websites to Web Apps.
<p><li>All your existing instances of Websites are now Web Apps in App Service.</p>
<p><li>You can access your existing websites via the <a href="/azure/app-service-web/app-service-web-app-azure-portal/">Azure Portal Preview</a>, where you will find all your existing sites under <em>App Service</em>.</p>
<p><li><em>Web Hosting Plan</em> is now <em>App Service Plan</em>. An <em>App Service Plan</em> can host any app type of App Service, such as Web, Mobile, or API apps.</p>
<p><li>Azure App Service Web Apps is in General Availability.</p>
<p><li><a href="https://www.azure.cn/home/features/app-service/web-apps/">Learn more about Web Apps</a>.</p></td>
</tr>
<tr class="even">
<td align="left">Azure Mobile Services</td>
<td align="left">Mobile Apps</td>
<td align="left"><p><li>Mobile Services continue to be available as a standalone service and remain fully supported.</p>
<p><li>Mobile Apps is an app type in App Service, which integrates all of the functionality of Mobile Services and more.</p>
<p><li>It is easy to <a href="/azure/app-service-mobile/app-service-mobile-migrating-from-mobile-services/">migrate from Mobile Services to Mobile Apps</a>.</p>
<p><li>As part of App Service, Mobile Apps get new capabilities beyond Mobile Services, such as  integration with on-premises and SaaS systems, staging slots, WebJobs, better scaling options, and more.</p>
<p><li><a href="https://www.azure.cn/home/features/app-service/mobile-apps/">Learn more about Mobile Apps</a>.</p>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left">API Apps</td>
<td align="left">
<p><li>API Apps is a new app type in App Service that lets you easily build and consume APIs in the cloud.</p>
<p><li><a href="https://www.azure.cn/home/features/app-service/api-apps/">Learn more about API Apps</a>.</p></td>
</tr>
</tbody>
</table>

To learn more, please visit [App Service documentation](/azure/app-service/).