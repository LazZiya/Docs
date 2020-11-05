<!-- meta tags details, will be assigned to meta tags inside header by js -->
<div id="meta-info">
<details><summary>meta info</summary>

> * Title: <i id="md-title">XML Based Localization Setup</i>
> * Keywords: <i id="md-keywords">localization, asp.net-core, xml, resource, files</i>
> * Description: <i id="md-description">Localization setup of Asp.Net Core based on XML resource files with XLocalizer.</i>
> * Author: <i id="md-author">Ziya Mollamahmut</i>
> * Date: <i id="md-date">02-Sep-2020</i>
> * Image: <i id="md-image">https://github.com/LazZiya/Docs/raw/master/XLocalizer/v1.0/images/xlocalizer-logo.png</i>
> * Image-alt: <i id="md-image-alt">XLocalizer Logo</i>
> * Version: <i id="md-version">v1.0</i>

</details>
</div>

# XML Based Localization Setup

By [Ziya Mollamahmut](https://github.com/LazZiya)

Localization based on _XML_ files works very similar to _RESX_ process, we only use _.xml_ files instead of _.resx_ to store resources. But the ability to edit _XML_ files at run time gives us the flexibility of automtically adding missing resources to _XML_ resource files.

### Table of contents
- [Install](#install)
- [Create resources folder](#create-resources-folder)
- [Startup settings](#startup-settings)
- [User secrets](#user-secrets)
- [Caching](#caching)
- [Full startup code for XML](#full-startup-code-for-xml)
- [Sample project](#sample-project)
- [Next: Localizing views][2]


#### Install
Install nuget package:
````
PM > Install-Package XLocalizer
PM > Install-Package XLocalizer.Translate.MyMemoryTranslate
````

> Notice: To install the latest preview add `-Pre` to the command line

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
// Add namespace for optional routing setup
using XLocalizer.Routing;

// Configure request localization options
services.Configure<RequestLocalizationOptions>(ops => 
{
    // Define supported cultures
    var cultures = new CultureInfo[] { new CultureInfo("en"), new CultureInfo("tr"), new CultureInfo("ar") };
    ops.SupportedCultures = cultures;
    ops.SupportedUICultures = cultures;
    ops.DefaultRequestCulture = new RequestCulture("en");

    // Optional: add custom provider to support localization based on {culture} route value
    ops.RequestCultureProviders.Insert(0, new RouteSegmentRequestCultureProvider(cultures));
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

- Add route based localization for razor pages:
````csharp
services.AddRazorPages()
        .AddRazorPagesOptions(ops => { ops.Conventions.Insert(0, new RouteTemplateModelConventionRazorPages()); });
````

Or if you are using MVC:
````csharp
services.AddMvc()
        .AddMvcOptions(ops => { ops.Conventions.Insert(0, new RouteTemplateModelConventionMvc()); });
````

and make sure that all controllers and actions have `[Route("...")]` attribute.

- Add `XLocalizer` setup and enable `AutoAddKeys` and `AutoTranslate` options:
````csharp
services.AddRazorPages()
        .AddRazorPagesOptions(ops => { ops.Conventions.Insert(0, new RouteTemplateModelConventionRazorPages()); });
        .AddXLocalizer<LocSource, MyMemoryTranslateService>(ops => 
        {
            ops.ResourcesPath = "LocalizationResources";
            ops.AutoAddKeys = true;
            ops.AutoTranslate = true;
            ops.TranslateFromCulture = "en"
        });
````

If `TranslateFromCulture` is not defined, the default request culture will be used as source culture for translation.

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

#### Full startup code for XML
````csharp
using Microsoft.AspNetCore.Builder;
using Microsoft.AspNetCore.Hosting;
using Microsoft.Extensions.Configuration;
using Microsoft.Extensions.DependencyInjection;
using Microsoft.Extensions.Hosting;
using XLocalizer.Translate;
using XLocalizer;
using XLocalizer.Xml;
using System.Globalization;
using XLocalizer.Routing;
using XLocalizer.Translate.MyMemoryTranslate;
using XmlLocalizationSample.LocalizationResources;

namespace XmlLocalizationSample
{
    public class Startup
    {
        public Startup(IConfiguration configuration)
        {
            Configuration = configuration;
        }

        public IConfiguration Configuration { get; }

        // This method gets called by the runtime. Use this method to add services to the container.
        public void ConfigureServices(IServiceCollection services)
        {
            services.Configure<RequestLocalizationOptions>(ops =>
            {
                var cultures = new CultureInfo[] { new CultureInfo("en"), new CultureInfo("tr"), new CultureInfo("ar") };
                ops.SupportedCultures = cultures;
                ops.SupportedUICultures = cultures;
                ops.DefaultRequestCulture = new Microsoft.AspNetCore.Localization.RequestCulture("en");

                // Optional: add custom provider to support localization based on route value {culture}
                ops.RequestCultureProviders.Insert(0, new RouteSegmentRequestCultureProvider(cultures));
            });
            
            // Optional: To enable online translation register one or more translation services
            services.AddHttpClient<ITranslator, MyMemoryTranslateService>();

            // Comment below line to switch to RESX based localization.
            services.AddSingleton<IXResourceProvider, XmlResourceProvider>();

            services.AddRazorPages()
                // Optional: Add {culture} route template to all razor pages routes e.g. /en/Index
                .AddRazorPagesOptions(ops => { ops.Conventions.Insert(0, new RouteTemplateModelConventionRazorPages()); })

                // Add XLocalization with a default resource <LocSource>
                // and specify a service for handling translation requests
                .AddXLocalizer<LocSource, MyMemoryTranslateService>(ops =>
                {
                    ops.ResourcesPath = "LocalizationResources";
                    ops.AutoAddKeys = true;
                    ops.AutoTranslate = true;
                });
        }

        // This method gets called by the runtime. Use this method to configure the HTTP request pipeline.
        public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
        {
            if (env.IsDevelopment())
            {
                app.UseDeveloperExceptionPage();
                app.UseDatabaseErrorPage();
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

            // Use request localization middleware
            app.UseRequestLocalization();

            app.UseEndpoints(endpoints =>
            {
                endpoints.MapRazorPages();
            });
        }
    }
}

````

#### Sample project
[Download sample project from GitHub][3]

#
#### Next: [Localizing views][2]
#


[1]:translate-services.md
[2]:localizing-views.md
[3]:https://github.com/LazZiya/XLocalizer.Samples/tree/master/XmlLocalizationSample