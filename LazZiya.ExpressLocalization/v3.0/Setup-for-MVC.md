<!-- meta tags details, will be assigned to meta tags inside header by js -->
<div id="meta-info">
<details><summary>meta info</summary>

> * Title: <i id="md-title">Setup ExpressLocalization for MVC</i>
> * Keywords: <i id="md-keywords">localization, asp.net-core, mvc</i>
> * Description: <i id="md-description">Learn how to setup ExpressLocalization for Asp.Net Core MVC.</i>
> * Author: <i id="md-author">Ziya Mollamahmut</i>
> * Date: <i id="md-date">27-Sep-2019</i>
> * Image: <i id="md-image">https://github.com/LazZiya/Docs/raw/master/LazZiya.ExpressLocalization/v3.0/images/lazziya-express-localization-logo.png</i>
> * Image-alt: <i id="md-image-alt">LazZiya.ExpressLocalization Logo</i>
> * Version: <i id="md-version">v3.0</i>

</details>
</div>

# Setup ExpressLocalization for MVC

By [Ziya Mollamahmut](https://github.com/LazZiya)

Configure _ExpressLocalization_ in `startup.cs`:
````csharp
using System.Globalization;
using LazZiya.ExpressLocalization;
using Microsoft.AspNetCore.Localization;

//setup express localization under ConfigureServices method:
public void ConfigureServices(IServiceCollection services)
{
    // Other configuration settings....
    
    var cultures = new CultureInfo[]
    {
        new CultureInfo("en"),
        new CultureInfo("tr"),
        new CultureInfo("ar")
    };

    services.AddControllersWithViews()
        .AddExpressLocalization<LocalizationResource>(
            ops =>
            {
                ops.ResourcesPath = "LocalizationResources";
                ops.RequestLocalizationOptions = o =>
                {
                    o.SupportedCultures = cultures;
                    o.SupportedUICultures = cultures;
                    o.DefaultRequestCulture = new RequestCulture("en");
                };
            });
}
````

Use `RequestLocalization` middleware :
````csharp
public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
{
    // Other codes...
    
    // Use localization middleware
    app.UseRequestLocalization();

    // Add {culture} to the route
    app.UseEndpoints(endpoints =>
    {
        endpoints.MapControllerRoute(
            name: "default",
            pattern: "{culture=en}/{controller=Home}/{action=Index}/{id?}");
    });
}
````