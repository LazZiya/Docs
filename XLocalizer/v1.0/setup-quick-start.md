<!-- meta tags details, will be assigned to meta tags inside header by js -->
<div id="meta-info">
<details><summary>meta info</summary>

> * Title: <i id="md-title">XLocalizer - Quick Start</i>
> * Keywords: <i id="md-keywords">localization, asp.net-core</i>
> * Description: <i id="md-description">A quick start to setup XLocalizer in Asp.Net Core.</i>
> * Author: <i id="md-author">Ziya Mollamahmut</i>
> * Date: <i id="md-date">08-Aug-2020</i>
> * Image: <i id="md-image">https://github.com/LazZiya/Docs/raw/master/XLocalizer/v1.0/images/xlocalizer-logo.png</i>
> * Image-alt: <i id="md-image-alt">XLocalizer Logo</i>
> * Version: <i id="md-version">v1.0</i>

</details>
</div>

# XLocalizer - Quick Start

By [Ziya Mollamahmut](https://github.com/LazZiya)

In this page I will show quickly how to setup `XLocalizer` with _XML_ resources and enabling `AutoKeyAdding` and `AutoTranslate` options.

### Table of contents
- [Install](#install)
- [Create resources folder](#create-resources-folder)
- [User secrets](#user-secrets)
- [Startup code](#startup-code)

#### Install
To use `XLocalizer` with online translation we need two nugets:
````
PM > Install-Package XLocalizer
PM > Install-Package XLocalizer.Translate.MyMemoryTranslate
````

> Notice: To install the latest preview add `-Pre` to the command line

#### Create resources folder
- Create a new folder under the root of the project and name it **`LocalizationResources`** or anything else...
- Create a new class inside **`LocalizationResources`** folder and name it **`LocSource`** or anything else...

The folder structure will be like below:
> - ProjectRoot/
>   - LocalizationResources/
>     - LocSource.cs

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

#### Startup code
````csharp
using XLocalizer;
using XLocalizer.Xml;
using XLocalizer.Routing;
using XLocalizer.Translate;
using XLocalizer.Translate.MyMemoryTranslate;
using XmlLocalizationSample.LocalizationResources;

namespace XmlLocalizationSample
{
    public class Startup
    {
        // other code ommitted

        public void ConfigureServices(IServiceCollection services)
        {
            // ...
            
            // Configure request localization options
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
            // ...

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


