<!-- meta tags details, will be assigned to meta tags inside header by js -->
<div id="meta-info">
<details><summary>meta info</summary>

> * Title: <i id="md-title">XLocalizer for Asp.Net Core</i>
> * Keywords: <i id="md-keywords">localization, asp.net-core, xlocalizer</i>
> * Description: <i id="md-description">Learn about localizing Asp.Net Core web apps with XLocalizer powered by auto translate and auto key adding.</i>
> * Author: <i id="md-author">Ziya Mollamahmut</i>
> * Date: <i id="md-date">21-Jun-2021</i>
> * Image: <i id="md-image">https://github.com/LazZiya/Docs/raw/master/XLocalizer/v1.0/images/xlocalizer-logo.png</i>
> * Image-alt: <i id="md-image-alt">XLocalizer Logo</i>
> * Version: <i id="md-version">v1.0</i>

</details>
</div>

# XLocalizer for Asp.Net Core

By [Ziya Mollamahmut](https://github.com/LazZiya)

Goodbye _"manually creating localization resources"_, welcome **XLocalizer**...! 

### What is XLocalizer
This is a nuget package that offers localization for Asp.Net Core based on _.resx_, _.xml_, _db_ or any other custom _file/db_ type. Powered by online translation and auto resource creating. XLocalizer has many powerful features and can be extended with custom tools. 

- Online Translation: Auto translation of missed localized values.
- Auto Key Adding: Auto adding missing keys to the resources files.
- Multiple Resource Type Support: Built-in localization support based on _.RESX_, _.XML_, _DB_. Extendable localization support based on any custom file/db type.
- Export to Resx: Resources from any source type can be exported to _.RESX_ files via built-in exporters.
- Do it Fast: Custom cache support for speeding up the process of getting localized values from sources.
- Standard interfaces: Easy to use due to using the standard localization interfaces: `IStringLocalizer`, `IHtmlLocalizer`, `IStringLocalizerFactory` and `IHtmlLocalizerFactory`.

### How it Works
`XLocalizer` will translate and save localized keys into automatically created resource files. Since `XLocalizer` modules are implementing the default localization interfaces _(`IStringLocalizer`, etc.)_ so any text passed into the localization services will be translated automatically and added into the relevant resource file/db. 

Additionally, `XLocalizer` has built-in modules to localize all system error messages like _(DataAnnotations, ModelBinding and Identity errors)_ without any additional workload.

![XLocalizer Simplified Workflow](https://github.com/LazZiya/Docs/raw/master/XLocalizer/v1.0/images/XLocalizer-Flowchart-Sample.jpg)

### Quick Setup
````csharp
services.AddRazorPages()
    .AddXLocalizer<LocSource, GoogleTranslateService>(ops =>
    {
        ops.ResourcesPath = "LocalizationResources";
        ops.AutoTranslate = true;
        ops.AutoAddKeys = true;
        ops.UseExpressMemoryCache = true;
        ops.TranslateFromCulture = "en";
    });
````

For more details see setup instructions based on project type:
 - [MVC/Razor Pages and XML Resource][2]
 - [MVC/Razor Pages and DB Resource][3]
 - [MVC/Razor Pages and RESX Resource][4]
 - [Blazor and XML Resource][4]
 - [Best Practices and Recommendations][6]


### Disclaimer Third Parties

All product and company names of translation services are trademarks™ or registered® trademarks of their respective holders. Use of them does not imply any affiliation with or endorsement by them.

During the development of `XLocalizer` I've used many online translation services with the freemium plan, but it is up to you to use a priced plan from the respective service.

 Each translation service has its pros and cons. [MyMemory Translate][1] provided the best results for the languages I've been working with _(in terms performans and amount of free translation requests)_. So, in this documentation you will see most samples refering to [MyMemory Translate][1] as the translation service. But you are free to use any other service that fits your needs.
#
### Next: [Xml based localization setup][2]
#


[1]:https://rapidapi.com/translated/api/mymemory-translation-memory
[2]:setup-xml.md
[3]:setup-db.md
[4]:setup-resx.md
[5]:setup-blazor.md
[6]:best-practice.md