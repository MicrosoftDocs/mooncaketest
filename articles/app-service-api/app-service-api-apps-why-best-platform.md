---
title: API Apps introduction | Azure
description: Learn how Azure App Service helps you develop, host, and consume RESTful APIs.
services: app-service\api
documentationcenter: .net
author: tdykstra
manager: erikre
editor: ''

ms.assetid: 60049a16-8159-47aa-a34b-110be0d8dab6
ms.service: app-service-api
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/23/2016
wacn.date: ''
ms.author: rachelap

---
# API Apps overview

[!INCLUDE [azure-sdk-developer-differences](../../includes/azure-sdk-developer-differences.md)]

API apps in Azure App Service offer features that make it easier to develop, host, and consume APIs in the cloud and on-premises. With API apps you get enterprise grade security, simple access control, and automatic SDK generation.

[Azure App Service](../app-service/app-service-value-prop-what-is.md) is a fully managed platform for web, mobile, and integration scenarios. API Apps is one of three app types offered by [Azure App Service](../app-service/app-service-value-prop-what-is.md).

![App types in Azure App Service](./media/app-service-api-apps-why-best-platform/appservicesuite.png)

## Why use API Apps?
Here are some key features of API Apps:

* **Bring your existing API as-is** - You don't have to change any of the code in your existing APIs to take advantage of API Apps -- just deploy your code to an API app. Your API can use any language or framework supported by App Service, including ASP.NET and C#, Java, PHP, Node.js, and Python.
* **Easy consumption** - Integrated support for [Swagger API metadata](http://swagger.io/) makes your APIs easily consumable by a variety of clients.  Automatically generate client code for your APIs in a variety of languages including C#, Java, and Javascript. Easily configure [CORS](app-service-api-cors-consume-javascript.md) without changing your code. For more information, see [App Service API Apps metadata for API discovery and code generation](app-service-api-metadata.md) and [Consume an API app from JavaScript using CORS](app-service-api-cors-consume-javascript.md). 
* **Simple access control** - Protect an API app from unauthenticated access with no changes to your code. Built-in authentication services secure APIs for access by other services or by clients representing users. Supported identity providers include Azure Active Directory and Microsoft Account. Clients can use Active Directory Authentication Library (ADAL) or the Mobile Apps SDK. For more information, see [Authentication and authorization for API Apps in Azure App Service](app-service-api-authentication.md).
* **Visual Studio integration** - Dedicated tools in Visual Studio streamline the work of creating, deploying, consuming, debugging, and managing API apps. For more information, see [Announcing the Azure SDK 2.8.1 for .NET](https://azure.microsoft.com/blog/announcing-azure-sdk-2-8-1-for-net/).

In addition, an API app can take advantage of features offered by [Web Apps](../app-service-web/app-service-web-overview.md) and [Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md). The reverse is also true: if you use a web app or mobile app to host an API, it can take advantage of API Apps features such as Swagger metadata for client code generation and CORS for cross-domain browser access. The only difference between the three app types (API, web, mobile) is the name and icon used for them in the Azure portal preview.

## Getting started
To get started with API Apps by deploying sample code to one, see the tutorial for whichever framework you prefer:

* [ASP.NET](app-service-api-dotnet-get-started.md) 
* [Node.js](app-service-api-nodejs-api-app.md) 
* [Java](app-service-api-java-api-app.md) 

To ask questions about API apps, start a thread in the [API Apps forum](https://social.msdn.microsoft.com/Forums/zh-cn/home?forum=AzureAPIApps).