<!-- meta tags details, will be assigned to meta tags inside header by js -->
<div id="meta-info">
<details><summary>meta info</summary>

> * Title: <i id="md-title">Customized Setup</i>
> * Keywords: <i id="md-keywords">localization, asp.net-core, express-localization, custom, setup</i>
> * Description: <i id="md-description">Learn how use a custom setup of ExpressLocalization.</i>
> * Author: <i id="md-author">Ziya Mollamahmut</i>
> * Date: <i id="md-date">08-Aug-2020</i>
> * Image: <i id="md-image">https://github.com/LazZiya/Docs/raw/master/LazZiya.ExpressLocalization/v4.0/images/lazziya-express-localization-logo.png</i>
> * Image-alt: <i id="md-image-alt">LazZiya.ExpressLocalization Logo</i>
> * Version: <i id="md-version">v4.0</i>

</details>
</div>

# Customized Setup

By [Ziya Mollamahmut](https://github.com/LazZiya)

If you don't want to use all localization settings in one step, you can use customized setup methods as described below.

````csharp
// Configure request localization options
services.Configure<RequestLocalizationOptions>(
    ops =>
    {
        ops.SupportedCultures = cultures;
        ops.SupportedUICultures = cultures;
        ops.DefaultRequestCulture = new RequestCulture("en");
    });
    
services.AddRazorPages()
    // Add view localization
    .AddViewLocalization(ops => { ops.ResourcesPath = "LocalizationResources"; })
    
    // Register route value request culture provider, 
    // and add route parameter {culture} at the beginning of every url
    .ExAddRouteValueRequestCultureProvider(cultures, "en")

    // Add view localization with shared resource, 
    .ExAddSharedCultureLocalizer<ViewLocalizationResource>()

    // Add DataAnnotations localization
    .ExAddDataAnnotationsLocalization<DataAnnotationsResource>()

    // Add ModelBinding localization
    .ExAddModelBindingLocalization<ModelBindingResource>()

    // Add IdentityErrors localization
    .ExAddIdentityErrorMessagesLocalization<IdentityErrorsResource>()
    
    // Register client side validation scripts taghelper 
    .ExAddClientSideLocalizationValidationScripts();
    
    // Configure identity redirect to paths (without culture value)
    .ExConfigureApplicationCookie(string loginPath, string logoutPath, string accessDeniedPath, string defCulture);
````

### Applies to ExpressLocalization versions:
 4.0, 3.2, 3.1, 3.0, 2.0, 1.1, 1.0