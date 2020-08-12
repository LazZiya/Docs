---
title: Localization of Blazor Server Projects
keywords: localization, asp.net-core, blazor
description: Learn how to localize Blazor server app with XLocalizer.
author: Ziya Mollamahmut
date: 08-Aug-2020
versions: 1.0
---

# Localization of Blazor Server Projects

By [Ziya Mollamahmut](https://github.com/LazZiya)

Localization of Blazor projects is very similar to Razor or MVC projects with a few restrictions/changes listed below.

> - No support for route based localization, cookie based localization can be used instead.
> - No support for [`LocalizeTagHelper`][2], traditional way of injecting `IStringLocailzer` to the views can be used instead.
> - No support for `IHtmlLocalizer`, only `IStringLocalizer` can be used instead.

### Table of contents
- [Install](#install)
- [Create resources folder](#create-resources-folder)
- [Startup settings](#startup-settings)
- [User secrets](#user-secrets)
- [Caching](#caching)
- [Localizing view](#localizing-view)
- [Setup culture cookie](#setup-culture-cookie)
- [Language navigation](#language-navigation)
- [Full startup code for Blazor Server project](#full-startup-code-for-blazor-server-project)
- [Sample project](#sample-project)


#### Install
Install nuget package:
````
PM > Install-Package XLocalizer
PM > Install-Package XLocalizer.Translate.MyMemoryTranslate
````

#### Create resources folder
Let's start by creating a folder and a dummy class for our localized resources.

- Create a new folder under the root of the project and name it **`LocalizationResources`** _or anything else..._
- Create a new class inside **`LocalizationResources`** folder and name it **`LocSource`** _or anything else..._
- Do not create resource files manually! they will be created automatically by `XLocalizer`.

The folder structure will be like below:
> - ProjectRoot/
>   - LocalizationResources/
>     - LocSource.cs

`LocSource` is empty class, it will be used only to refere to _.resx_ resource files inside the code.
````csharp
public class LocSource
{
}
````

#### Startup settings

- Configure request localization options and optionally add `RouteSegmentRequestCultureProvider` :
````csharp
// Configure request localization options
services.Configure<RequestLocalizationOptions>(ops => 
{
    // Define supported cultures
    var cultures = new CultureInfo[] { new CultureInfo("en"), new CultureInfo("tr"), new CultureInfo("ar") };
    ops.SupportedCultures = cultures;
    ops.SupportedUICultures = cultures;
    ops.DefaultRequestCulture = new RequestCulture("en");
});        
````

- Register xml resource provider: By default `XLocalizer` works with _.resx_ resource files. But to enable auto key adding we need to register `XmlResourceProvider` :
````csharp
services.AddSingleton<IXResourceProvider, XmlResourceProvider>();
````

> You can provide localization support based on any custom file type by implementing `IXResourceProvider` interface.


- Register a translation service to enable auto translation option:
````csharp
services.AddHttpClient<ITranslator, MyMemoryTranslateService>();
````

> You can provide translation support based on any custom provider type by implementing `ITranslator` interface.


- Add `XLocalizer` setup and enable `AutoAddKeys` and `AutoTranslate` options:
````csharp
services.AddRazorPages()
        .AddXLocalizer<LocSource, MyMemoryTranslateService>(ops => 
        {
            ops.ResourcesPath = "LocalizationResources";
            ops.AutoAddKeys = true;
            ops.AutoTranslate = true;
        });
````

- Configure the app to use request localization middleware:
````csharp
app.UseRequestLocalization();
````

#### User secrets
Our translation service is based on RapidAPI, so we need to add the relevant API key to the user secrets file.
> Right click on the project name and select _Manage User Secrets_, then add the API key as below:

````json
{
  "XLocalizer.Translate": {
    "RapidApiKey": "xxx-rapid-api-key-xxx",
  }
}
````
Read more about translation services in [Translation services][1].


##### Caching
`XLocalizer` has built-in caching enabled by default. Caching helps to speedup the retriving of localized resources. But, it is recommended to switch caching off during development to avoid caching values that are subject to change frequently.

````csharp
ops.UseExpressMemoryCache = false;
```` 

#### Localizing View
Inject `IStringLocalizer` and use it as below:
````html
@inject IStringLocalizer _loc

<h1>@_loc["Welcome"]</h1>
````

#### Setup Culture Cookie
Open `_Host.cshtml` file and add cookie code inside the `<body>` tag:
````html
<body>
    @{
        this.HttpContext.Response.Cookies.Append(
            CookieRequestCultureProvider.DefaultCookieName,
            CookieRequestCultureProvider.MakeCookieValue(
                new RequestCulture(
                    CultureInfo.CurrentCulture,
                    CultureInfo.CurrentUICulture)));
    }
    ....
</body>
````

#### Language Navigation
Language navigation requruires adding a controller with the cookie code inside it, so before creating the language navigation we need to add controller support:
* Add controllers support in startup:
````csharp
services.AddControllers();
````

* Map controllers endpoints:
````csharp
app.UseEndpoints(endpoints =>
{
    endpoints.MapControllers();
    endpoints.MapBlazorHub();
    endpoints.MapFallbackToPage("/_Host");
});
````

* Create a new controller and use the below SetCulture method inside it:
````csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Threading.Tasks;
using Microsoft.AspNetCore.Localization;
using Microsoft.AspNetCore.Mvc;

namespace BlazorLocalizationSample.Controllers
{
    [Route("[controller]/[action]")]
    public class CultureController : Controller
    {
        public IActionResult SetCulture(string culture, string redirectUri)
        {
            if (culture != null)
            {
                HttpContext.Response.Cookies.Append(
                    CookieRequestCultureProvider.DefaultCookieName,
                    CookieRequestCultureProvider.MakeCookieValue(
                        new RequestCulture(culture)));
            }

            return LocalRedirect(redirectUri);
        }
    }
}
````
* Create a new razor component named `LanguageNav.razor` under Shared folde:
````html
@inject NavigationManager NavigationManager

<select @onchange="OnSelected" class="form-control col-2">
    @foreach (var c in SupportedCultures)
    {
        var culture = System.Globalization.CultureInfo.GetCultureInfo(c);
        if (CurrentCultureName == c)
        {
            <option value="@c" selected>@culture.EnglishName</option>
        }
        else
        {

            <option value="@c">@culture.EnglishName</option>
        }
    }
</select>

@code {
    private void OnSelected(ChangeEventArgs e)
    {
        var culture = (string)e.Value;
        var uri = new Uri(NavigationManager.Uri)
            .GetComponents(UriComponents.PathAndQuery, UriFormat.Unescaped);
        var query = $"?culture={Uri.EscapeDataString(culture)}&" +
            $"redirectUri={Uri.EscapeDataString(uri)}";

        NavigationManager.NavigateTo("/Culture/SetCulture" + query, forceLoad: true);
    }

    private string CurrentCultureName = System.Globalization.CultureInfo.CurrentCulture.Name;
    private string[] SupportedCultures = { "en", "tr", "ar" };
}
````

* Use the language component in the `MainLayout.razor` page where you want the language navigation to appear:
````html
@inherits LayoutComponentBase

<div class="sidebar">
    <NavMenu />
</div>

<div class="main">
    <div class="top-row px-4">
        <LanguageNav></LanguageNav>
        <a href="https://docs.microsoft.com/aspnet/" target="_blank">@_loc["About"]</a>
    </div>

    <div class="content px-4">
        @Body
    </div>
</div>
````

#### Full startup code for Blazor Server project
````csharp
using Microsoft.AspNetCore.Builder;
using Microsoft.AspNetCore.Hosting;
using Microsoft.Extensions.Configuration;
using Microsoft.Extensions.DependencyInjection;
using Microsoft.Extensions.Hosting;
using BlazorLocalizationSample.Data;
using System.Globalization;
using XLocalizer.Translate;
using XLocalizer.Translate.MyMemoryTranslate;
using XLocalizer;
using XLocalizer.Xml;
using BlazorLocalizationSample.LocalizationResources;

namespace BlazorLocalizationSample
{
    public class Startup
    {
        public Startup(IConfiguration configuration)
        {
            Configuration = configuration;
        }

        public IConfiguration Configuration { get; }

        // This method gets called by the runtime. Use this method to add services to the container.
        // For more information on how to configure your application, visit https://go.microsoft.com/fwlink/?LinkID=398940
        public void ConfigureServices(IServiceCollection services)
        {
            services.Configure<RequestLocalizationOptions>(ops =>
            {
                var cultures = new CultureInfo[] { new CultureInfo("en"), new CultureInfo("tr"), new CultureInfo("ar") };
                ops.SupportedCultures = cultures;
                ops.SupportedUICultures = cultures;
                ops.DefaultRequestCulture = new Microsoft.AspNetCore.Localization.RequestCulture("en");
            });

            services.AddHttpClient<ITranslator, MyMemoryTranslateService>();
            services.AddSingleton<IXResourceProvider, XmlResourceProvider>();

            services.AddControllers();
            services.AddRazorPages()
                .AddXLocalizer<LocSource, MyMemoryTranslateService>(ops =>
                {
                    ops.ResourcesPath = "LocalizationResources";
                    ops.AutoAddKeys = true;
                    ops.AutoTranslate = true;
                });
            services.AddServerSideBlazor();
            services.AddSingleton<WeatherForecastService>();
        }

        // This method gets called by the runtime. Use this method to configure the HTTP request pipeline.
        public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
        {
            if (env.IsDevelopment())
            {
                app.UseDeveloperExceptionPage();
            }
            else
            {
                app.UseExceptionHandler("/Error");
                // The default HSTS value is 30 days. You may want to change this for production scenarios, see https://aka.ms/aspnetcore-hsts.
                app.UseHsts();
            }

            app.UseHttpsRedirection();
            app.UseStaticFiles();

            app.UseRouting();
            app.UseRequestLocalization();
            app.UseEndpoints(endpoints =>
            {
                endpoints.MapControllers();
                endpoints.MapBlazorHub();
                endpoints.MapFallbackToPage("/_Host");
            });
        }
    }
}
````

#### Sample project
[Download sample project from GitHub][3]

#### References:
- [ASP.NET Core Blazor globalization and localization][5]


[1]:translate-services.md
[2]:localizing-views.md
[3]:https://github.com/LazZiya/XLocalizer.Samples/tree/master/BlazorLocalizationSample
[4]:localizing-views.md#traditional-localization-for-views
[5]:https://docs.microsoft.com/en-us/aspnet/core/blazor/globalization-localization?view=aspnetcore-3.1
