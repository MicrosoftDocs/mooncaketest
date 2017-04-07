---
title: Deploy your app to Azure App Service | Azure 
description: Learn how to deploy your app to Azure App Service.
services: app-service
documentationcenter: ''
author: cephalin
manager: erikre
editor: ''

ms.assetid: f1464f71-2624-400e-86a2-e687e385804f
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/05/2017
wacn.date: ''
ms.author: cephalin;dariac

---
# Deploy your app to Azure App Service
This article helps you determine the best option to deploy the files for your web app, mobile app backend, or API app to [Azure App Service](/azure/app-service-web/app-service-changes-existing-services/), and then guides you to appropriate resources with instructions specific to your preferred option.

## <a name="overview"></a>Azure App Service deployment overview
Azure App Service maintains the application framework for you (ASP.NET, PHP, Node.js, etc). Some frameworks are enabled by default while others, like Java and Python, may need a simple checkmark configuration to enable it. In addition, you can customize your application framework, such as the PHP version or the bitness of your runtime. For more information, see [Configure your app in Azure App Service](web-sites-configure.md).

Since you don't have to worry about the web server or application framework, deploying your app to App Service is a matter of deploying your code, binaries, content files, and their respective directory structure, to the [**/site/wwwroot** directory](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure) in Azure (or the **/site/wwwroot/App_Data/Jobs/** directory for WebJobs). App Service supports three different deployment processes. All the deployment methods in this article use one of the 
following processes: 

* [FTP or FTPS](https://en.wikipedia.org/wiki/File_Transfer_Protocol): Use your favorite FTP or FTPS enabled tool to move your files to Azure, from [FileZilla](https://filezilla-project.org) to full-featured IDEs like [NetBeans](https://netbeans.org). This is strictly a file upload process. No additional services are provided by App Service, such as version control, file structure management, etc. 
* [Kudu (Git/Mercurial)](https://github.com/projectkudu/kudu/wiki/Deployment): Kudu is the [deployment engine](https://github.com/projectkudu/kudu/wiki) in App Service. Push your code to Kudu directly from any repository. Kudu also provides added services whenever code is pushed to it, including version control, package restore, MSBuild, and [web hooks](https://github.com/projectkudu/kudu/wiki/Web-hooks) for continuous deployment and other automation tasks. The Kudu deployment engine supports 2 different types of deployment sources:   

    * Repository-based continuous deployment with auto-sync from GitHub 
    * Repository-based deployment with manual sync from local Git  
* [Web Deploy](http://www.iis.net/learn/publish/using-web-deploy/introduction-to-web-deploy): Deploy code to App Service directly from your favorite Microsoft tools such as Visual Studio using the same tooling that automates deployment to IIS servers. This tool supports diff-only deployment, database creation, transforms of connection strings, etc. Web Deploy differs from Kudu in that application binaries are built before they are deployed to Azure. Similar to FTP, no additional services are provided by App Service.

Popular web development tools support one or more of these deployment processes. While the tool you choose determines the deployment processes you can leverage, the actual DevOps functionality at your disposal depends on the combination of the deployment process and the specific tools you choose. For example, if you perform Web Deploy from [Visual Studio with Azure SDK](#vspros), even though you don't get automation from Kudu, you do get package restore and MSBuild automation in Visual Studio. 

> [!NOTE]
> These deployment processes don't actually [provision the Azure resources](../azure-resource-manager/resource-group-template-deploy-portal.md) that your app may need. However, most of the linked how-to articles show you how to provision the app AND deploy your code to it end-to-end. You can also find additional options for provisioning Azure resources in the [Automate deployment by using command-line tools](#automate) section.
> 
> 

## <a name="ftp"></a>Deploy manually by uploading files with FTP
If you are used to manually copying your web content to a web server, you can use an [FTP](http://en.wikipedia.org/wiki/File_Transfer_Protocol) utility to copy files, such as Windows Explorer or [FileZilla](https://filezilla-project.org/).

The pros of copying files manually are:

* Familiarity and minimal complexity for FTP tooling. 
* Knowing exactly where your files are going.
* Added security with FTPS.

The cons of copying files manually are:

* Having to know how to deploy files to the correct directories in App Service. 
* No version control for rollback when failures occur.
* No built-in deployment history for troubleshooting deployment issues.
* Potential long deployment times because many FTP tools don't provide diff-only copying and simply copy all the files.  

### <a name="howtoftp"></a>How to upload files with FTP
The [Azure Portal Preview](https://portal.azure.cn) gives you all the information you need to connect to your app's directories using FTP or FTPS.

* [Deploy your app to Azure App Service using FTP](app-service-deploy-ftp.md)

## <a name="continuousdeployment"></a>Deploy continuously from a cloud-based source control service
If your development team uses a cloud-based source code management (SCM) service like [GitHub](https://www.github.com), you can configure App Service to integrate with your repository and deploy continuously. 

The pros of deploying from a cloud-based source control service are:

* Version control to enable rollback.
* Ability to configure continuous deployment for Git (and Mercurial where applicable) repositories. 
* Branch-specific deployment, can deploy different branches to different [slots](web-sites-staged-publishing.md).
* All functionality in the Kudu deployment engine is available (e.g. deployment versioning, rollback, package restore, automation).

The con of deploying from a cloud-based source control service is:

* Some knowledge of the respective SCM service required.

### <a name="vsts"></a>How to deploy continuously from a cloud-based source control service
In the Kudu, you can configure continuous deployment from GitHub.

* [Continous Deployment to Azure App Service](app-service-continuous-deployment.md). 

To find out how to configure continuous deployment manually from a cloud repository not listed by the Azure Portal Preview (such as [GitLab](https://gitlab.com/)), see
[Setting up continuous deployment using manual steps](https://github.com/projectkudu/kudu/wiki/Continuous-deployment#setting-up-continuous-deployment-using-manual-steps).

## <a name="localgitdeployment"></a>Deploy from local Git
If your development team uses an on-premises local source code management (SCM) service based on Git, you can configure this as a deployment source to App Service. 

Pros of deploying from local Git are:

* Version control to enable rollback.
* Branch-specific deployment, can deploy different branches to different [slots](web-sites-staged-publishing.md).
* All functionality in the Kudu deployment engine is available (e.g. deployment versioning, rollback, package restore, automation).

Con of deploying from local Git is:

* Some knowledge of the respective SCM system required.
* No turn-key solutions for continuous deployment. 

### <a name="vsts"></a>How to deploy from local Git
In the [Azure Portal Preview](https://portal.azure.cn), you can configure local Git deployment.

* [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md). 
* [Publishing to Web Apps from any git/hg repo](http://blog.davidebbo.com/2013/04/publishing-to-azure-web-sites-from-any.html).  

## Deploy using an IDE
If you are already using [Visual Studio](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) with an [Azure SDK](/downloads/), or other IDE suites like [Xcode](https://developer.apple.com/xcode/), [Eclipse](https://www.eclipse.org), and [IntelliJ IDEA](https://www.jetbrains.com/idea/), you can deploy to Azure directly from within your IDE. This option is ideal for an individual developer.

Visual Studio supports all three deployment processes (FTP, Git, and Web Deploy), depending on your preference, while other IDEs can deploy to App Service if they have FTP or Git integration (see [Overview of deployment processes](#overview)).

The pros of deploying using an IDE are:

* Potentially minimize the tooling for your end-to-end application life-cycle. Develop, debug, track, and deploy your app to Azure all without moving outside of your IDE. 

The cons of deploying using an IDE are:

* Added complexity in tooling.
* Still requires a source control system for a team project.

<a name="vspros"></a>
Additional pros of deploying using Visual Studio with Azure SDK are:

* Azure SDK makes Azure resources first-class citizens in Visual Studio. Create, delete, edit, start, and stop apps, query the backend SQL database, live-debug the Azure app, and much more. 
* Live editing of code files on Azure.
* Live debugging of apps on Azure.
* Integrated Azure explorer.
* Diff-only deployment. 

### <a name="vs"></a>How to deploy from Visual Studio directly
* [Get started with Azure and ASP.NET](web-sites-dotnet-get-started.md). How to create and deploy a simple ASP.NET MVC web project by using Visual Studio and Web Deploy.
* [How to Deploy Azure WebJobs using Visual Studio](websites-dotnet-deploy-webjobs.md). How to configure Console Application projects so that they deploy as WebJobs.  
* [Deploy a Secure ASP.NET MVC 5 app with Membership, OAuth, and SQL Database to Web Apps](web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md). How to create and deploy an ASP.NET MVC web project with a SQL database, by using Visual Studio, Web Deploy, and Entity Framework Code First Migrations.
* [ASP.NET Web Deployment using Visual Studio](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/introduction). A 12-part tutorial series that covers a more complete range of deployment tasks than the others in this list. Some Azure deployment features have been added since the tutorial was written, but notes added later explain what's missing.
* [Deploying an ASP.NET Website to Azure in Visual Studio 2012 from a Git Repository directly](http://www.dotnetcurry.com/ShowArticle.aspx?ID=881). Explains how to deploy an ASP.NET web project in Visual Studio, using the Git plug-in to commit the code to Git and connecting Azure to the Git repository. Starting in Visual Studio 2013, Git support is built-in and doesn't require installation of a plug-in.

## <a name="automate"></a>Automate deployment by using command-line tools
If you prefer the command-line terminal as the development environment of choice, you can script deployment tasks for your App Service app using command-line tools. 

Pros of deploying by using command-line tools are:

* Enables scripted deployment scenarios.
* Integrate provisioning of Azure resources and code deployment.
* Integrate Azure deployment into existing continous integration scripts.

Cons of deploying by using command-line tools are:

* Not for GUI-preferring developers.

### <a name="automatehow"></a>How to automate deployment with command-line tools

See [Automate deployment of your Azure app with command-line tools](app-service-deploy-command-line.md) for a list of command-line tools and links to tutorials. 

## <a name="nextsteps"></a>Next Steps
In some scenarios you might want to be able to easily switch back and forth between a staging and a production version of your app. For more information, see [Staged Deployment on Web Apps](web-sites-staged-publishing.md).

Having a backup and restore plan in place is an important part of any deployment workflow. For information about the App Service backup and restore feature, see [Web Apps Backups](web-sites-backup.md).  

For information about how to use Azure's Role-Based Access Control to manage access to App Service deployment, see [RBAC and Web App Publishing](https://azure.microsoft.com/blog/2015/01/05/rbac-and-azure-websites-publishing/).