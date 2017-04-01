---
title: Azure AD .NET web API Getting Started | Azure
description: How to build a .NET MVC web API that integrates with Azure AD for authentication and authorization.
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: ''

ms.assetid: 67e74774-1748-43ea-8130-55275a18320f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
wacn.date: ''
ms.author: dastrock
---

# Help protect a web API by using bearer tokens from Azure AD
[!INCLUDE [active-directory-devguide](../../includes/active-directory-devguide.md)]

If you’re building an application that provides access to protected resources, you need to know how to prevent unwarranted access to those resources.
Azure Active Directory (Azure AD) makes it simple and straightforward to help protect a web API by using OAuth 2.0 bearer access tokens with only a few lines of code.

In ASP.NET web apps, you can accomplish this protection by using the Microsoft implementation of the community-driven OWIN middleware included in .NET Framework 4.5. Here we’ll use OWIN to build a "To Do List" web API that:

- Designates which APIs are protected.
- Validates that the web API calls contain a valid access token.

To build the To Do List API, you first need to:

1. Register an application with Azure AD.
2. Set up the app to use the OWIN authentication pipeline.
3. Configure a client application to call the web API.

To get started, [download the app skeleton](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/skeleton.zip) or [download the completed sample](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip). Each is a Visual Studio 2013 solution. You also need an Azure AD tenant in which to register your application. If you don't have one already, [learn how to get one](./active-directory-howto-tenant.md).

## Step 1: Register an application with Azure AD
To help secure your application, you first need to create an application in your tenant and provide Azure AD with a few key pieces of information.

- Sign into the [Azure Management Portal](https://manage.windowsazure.cn)
- In the left hand nav, click on **Active Directory**
- Select a tenant in which to register the application.
- Click the **Applications** tab, and click **Add** in the bottom drawer.
- Follow the prompts and create a new **Web Application and/or WebAPI**.
    - The **Name** of the application will describe your application to end-users.  Enter "To Do List Service".
    - The **Redirect Uri** is a scheme and string combination that Azure AD would use to return any tokens your app requested. Enter `https://localhost:44321/` for this value.
- Once you’ve completed registration, navigate to **Configure** tab and locate the **App ID URI** field.  Enter a tenant-specific identifier for this value, e.g. `https://contoso.partner.onmschina.cn/TodoListService`
- Save the configuration.  Leave the portal open - you'll also need to register your client application shortly.

## Step 2: Set up the app to use the OWIN authentication pipeline
To validate incoming requests and tokens, you need to set up your application to communicate with Azure AD.

1. To begin, open the solution and add the OWIN middleware NuGet packages to the TodoListService project by using the Package Manager Console.

    ```
    PM> Install-Package Microsoft.Owin.Security.ActiveDirectory -ProjectName TodoListService
    PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoListService
    ```

2. Add an OWIN Startup class to the TodoListService project called `Startup.cs`.  Right-click the project, select **Add** > **New Item**, and then search for **OWIN**. The OWIN middleware will invoke the `Configuration(…)` method when your app starts.

3. Change the class declaration to `public partial class Startup`. We’ve already implemented part of this class for you in another file. In the `Configuration(…)` method, make a call to `ConfgureAuth(…)` to set up authentication for your web app.

    ```C#
    public partial class Startup
    {
        public void Configuration(IAppBuilder app)
        {
            ConfigureAuth(app);
        }
    }
    ```

4. Open the file `App_Start\Startup.Auth.cs` and implement the `ConfigureAuth(…)` method. The parameters that you provide in `WindowsAzureActiveDirectoryBearerAuthenticationOptions` will serve as coordinates for your app to communicate with Azure AD.

    ```C#
    public void ConfigureAuth(IAppBuilder app)
    {
        app.UseWindowsAzureActiveDirectoryBearerAuthentication(
            new WindowsAzureActiveDirectoryBearerAuthenticationOptions
            {
                Audience = ConfigurationManager.AppSettings["ida:Audience"],
                Tenant = ConfigurationManager.AppSettings["ida:Tenant"]
            });
    }
    ```

5. Now you can use `[Authorize]` attributes to help protect your controllers and actions with JSON Web Token (JWT) bearer authentication. Decorate the `Controllers\TodoListController.cs` class with an authorize tag. This will force the user to sign in before accessing that page.

    ```C#
    [Authorize]
    public class TodoListController : ApiController
    {
    ```

    When an authorized caller successfully invokes one of the `TodoListController` APIs, the action might need access to information about the caller. OWIN provides access to the claims inside the bearer token via the `ClaimsPrincpal` object.  

6. A common requirement for web APIs is to validate the "scopes" present in the token. This ensures that the user has consented to the permissions required to access the To Do List Service.

    ```C#
    public IEnumerable<TodoItem> Get()
    {
        // user_impersonation is the default permission exposed by applications in Azure AD
        if (ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/scope").Value != "user_impersonation")
        {
            throw new HttpResponseException(new HttpResponseMessage {
              StatusCode = HttpStatusCode.Unauthorized,
              ReasonPhrase = "The Scope claim does not contain 'user_impersonation' or scope claim not found"
            });
        }
        ...
    }
    ```

7. Open the `web.config` file in the root of the TodoListService project, and enter your configuration values in the `<appSettings>` section.
  - `ida:Tenant` is the name of your Azure AD tenant--for example, contoso.partner.onmschina.cn.
  - `ida:Audience` is the App ID URI of the application that you entered in the Azure portal.

## Step 3: Configure a client application and run the service
Before you can see the To Do List Service in action, you need to configure the To Do List client so it can get tokens from Azure AD and make calls to the service.

- Navigate back to the [Azure Management Portal](https://manage.windowsazure.cn)
- Create a new application in your Azure AD tenant, and select **Native Client Application** in the resulting prompt.
    - The **Name** of the application will describe your application to end-users
    - Enter `http://TodoListClient/` for the **Redirect Uri** value.
- Once you’ve completed registration, AAD will assign your app a unique **Client Id**. You’ll need this value in the next steps, so copy it from the Configure tab.
- Also in **Configure** tab, locate the "Permissions to Other Applications" section. Click "Add Application." Select "All Apps" in the "Show" dropdown, and click the upper check mark. Locate & click on your To Do List Service, and click the bottom check mark to add the application. Select "Access To Do List Service" from the "Delegated Permissions" dropdown, and save the configuration.

- In Visual Studio, open `App.config` in the TodoListClient project and enter your configuration values in the `<appSettings>` section.

  - The `ida:Tenant` is the name of your Azure AD tenant, e.g. "contoso.partner.onmschina.cn".
  - Your `ida:ClientId` app ID you copied from the Azure Portal.
  - Your `todo:TodoListResourceId` is the App ID URI of the To Do List Service application that you entered in the Azure Portal.

## Next steps
Finally, clean, build, and run each project. If you haven’t already, now is the time to create a new user in your tenant with a *.partner.onmschina.cn domain. Sign in to the To Do List client with that user, and add some tasks to the user's to-do list.

For reference, the completed sample (without your configuration values) is available in [GitHub](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip). You can now move on to more identity scenarios.

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../includes/active-directory-devquickstarts-additional-resources.md)]