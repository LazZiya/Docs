<!-- meta tags details, will be assigned to meta tags inside header by js -->
<div id="meta-info">
<details><summary>meta info</summary>

> * Title: <i id="md-title">XLocalizer Setup</i>
> * Keywords: <i id="md-keywords">localization, asp.net-core, setup, startup, xml, db, resx</i>
> * Description: <i id="md-description">Learn how to setup XLocalizer for localization of Asp.Net Core web app.</i>
> * Author: <i id="md-author">Ziya Mollamahmut</i>
> * Date: <i id="md-date">08-Aug-2020</i>
> * Image: <i id="md-image">https://github.com/LazZiya/Docs/raw/vNext/XLocalizer/v1.0/images/xlocalizer-logo.png</i>
> * Image-alt: <i id="md-image-alt">XLocalizer Logo</i>
> * Version: <i id="md-version">v1.0</i>

</details>
</div>

# XLocalizer Setup

By [Ziya Mollamahmut](https://github.com/LazZiya)

Install main package from nuget:
````
PM > Install-Package XLocalizer
````

Because XLocalizer supports multiple source types, you can use any of the below setups:

- [Common localization settings](#common-localization-settings)
- [Localization setup based on XML][1]
- [Localization setup based on DB][2]
- [Localization setup based on RESX][3]

#### Common localization settings
This is the common configuration for all localization setup types. After finishing this step you can choose the setup mode to use.

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

To support route value based localization we need to configure `{culture}` route in every page for razor pages or MVC. So we can have all our routes setup with the culture parameter defined as: *`/{culture}/Index`*

> These optional steps required only for enabling localization based on route value

**- Razor Pages**
````csharp
services.AddRazorPages()
        .AddRazorPagesOptions(ops => { ops.Conventions.Insert(0, new RouteTemplateModelConventionRazorPages()); });
````

**- MVC**
````csharp
services.AddMvc()
        .AddMvcOptions(ops => { ops.Conventions.Insert(0, new RouteTemplateModelConventionMvc()); });
````


[1]:setup-xml.md
[2]:setup-db.md
[3]:setup-resx.md
