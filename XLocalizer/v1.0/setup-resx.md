<!-- meta tags details, will be assigned to meta tags inside header by js -->
<div id="meta-info">
<details><summary>meta info</summary>

> * Title: <i id="md-title">RESX Based Localization Setup</i>
> * Keywords: <i id="md-keywords">localization, asp.net-core, resx, resource, files</i>
> * Description: <i id="md-description">Localization setup of Asp.Net Core based on RESX resource files with XLocalizer.</i>
> * Author: <i id="md-author">Ziya Mollamahmut</i>
> * Date: <i id="md-date">31-Mar-2021</i>
> * Image: <i id="md-image">https://github.com/LazZiya/Docs/raw/master/XLocalizer/v1.0/images/xlocalizer-logo.png</i>
> * Image-alt: <i id="md-image-alt">XLocalizer Logo</i>
> * Version: <i id="md-version">v1.0</i>

</details>
</div>

# MVC/Razor Pages and RESX Based Localization Setup

By [Ziya Mollamahmut](https://github.com/LazZiya)

_RESX_ resource files are the default file type for localization. But, _RESX_ files do not support editing at runtime! So if you do not want to fill them manually, start localization setup based on XML or DB, then export the resources to _RESX_ files.

### Table of contents
- [Install](#install)
- [Create resources folder](#create-resources-folder)
- [Startup settings](#startup-settings)
- [Full startup code for RESX](#full-startup-code-for-resx)
- [Sample peoject](#sample-project)


#### Install
Install nuget package:
````
PM > Install-Package XLocalizer
````

> Notice: To install the latest preview add `-Pre` to the command line

#### Create resources folder
Create a folder and a dummy class for our localized resources.

- Create a new folder under the root of the project and name it **`LocalizationResources`** or anything else...
- Create a new class inside **`LocalizationResources`** folder and name it **`LocSource`** or anything else...

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
Add `XLocalizer` setup:
````csharp
using XLocalizer;

services.AddRazorPages()
        .AddXLocalizer<LocSource>(ops => 
        {
            ops.ResourcesPath = "LocalizationResources";
        });
````

Then we can create our localized resources files under **`LocalizationResources`** folder as below:

 - LocSource.tr.resx
 - LocSource.ar.resx
 - ...


#### Full startup code for RESX:
````csharp
using Microsoft.AspNetCore.Builder;
using Microsoft.AspNetCore.Hosting;
using Microsoft.Extensions.Configuration;
using Microsoft.Extensions.DependencyInjection;
using Microsoft.Extensions.Hosting;
using System.Globalization;
using XLocalizer;
using XLocalizer.Routing;
using SampleProject.LocalizationResources;

namespace SampleProject
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
            
            services.AddRazorPages()
                // Optional: Add {culture} route template to all razor pages routes e.g. /en/Index
                .AddRazorPagesOptions(ops => { ops.Conventions.Insert(0, new RouteTemplateModelConventionRazorPages()); })

                // Add XLocalizer with a default resource <LocSource>
                .AddXLocalizer<LocSource>(ops =>
                {
                    ops.ResourcesPath = "LocalizationResources";
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
[Download sample project from GitHub][1]


[1]:https://github.com/LazZiya/XLocalizer.Samples/tree/master/ResxLocalizationSample