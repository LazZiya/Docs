<!-- meta tags details, will be assigned to meta tags inside header by js -->
<div id="meta-info">
<details><summary>meta info</summary>

> * Title: <i id="md-title">Setup ExpressLocalization for Razor Pages</i>
> * Keywords: <i id="md-keywords">localization, asp.net-core, razor, pages</i>
> * Description: <i id="md-description">Learn how to setup ExpressLocalization for Asp.Net Core Razor Pages.</i>
> * Author: <i id="md-author">Ziya Mollamahmut</i>
> * Date: <i id="md-date">08-Aug-2020</i>
> * Image: <i id="md-image">https://github.com/LazZiya/Docs/raw/master/LazZiya.ExpressLocalization/v4.0/images/lazziya-express-localization-logo.png</i>
> * Image-alt: <i id="md-image-alt">LazZiya.ExpressLocalization Logo</i>
> * Version: <i id="md-version">v4.0</i>

</details>
</div>

# Setup ExpressLocalization for Razor Pages

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

    services.AddRazorPages()
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

    app.UseEndpoints(endpoints =>
    {
        endpoints.MapRazorPages();
    });
}
````

### Applies to ExpressLocalization versions:
 4.0, 3.2, 3.1, 3.0, 2.0, 1.1, 1.0