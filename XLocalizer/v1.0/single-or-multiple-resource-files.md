<!-- meta tags details, will be assigned to meta tags inside header by js -->
<div id="meta-info">
<details><summary>meta info</summary>

> * Title: <i id="md-title">XLocalizer - Working with Single or Multiple Resource Files</i>
> * Keywords: <i id="md-keywords">localization, asp.net-core, xlocalizer, understanding, single, multiple, resource, files</i>
> * Description: <i id="md-description">Understand how XLocalizer creates resource files, and how to create more resource files for localization.</i>
> * Author: <i id="md-author">Ziya Mollamahmut</i>
> * Date: <i id="md-date">01-Jul-2021</i>
> * Image: <i id="md-image">https://github.com/LazZiya/Docs/raw/master/XLocalizer/v1.0/images/xlocalizer-logo.png</i>
> * Image-alt: <i id="md-image-alt">XLocalizer Logo</i>
> * Version: <i id="md-version">v1.0</i>

</details>
</div>

# Working with Single or Multiple Resource Files
`XLocalizer` can work with single or multiple resource files. In other words, all localized texts for each single culture can be placed in one resource file, or you can use multiple resource files for each culture to split the contents as required. Read below details to have full insights on how to work with single or multiple resource files.

## Understading Resource Files
When you work with [XML based resources][1], XLocalizer automatically creates `.xml` resource files for each culture automatically. The files will be created according to the setup in `startup.cs` file.

````csharp
// Define supported cultures
services.Configure<RequestLocalizationOptions>(ops => 
{
    // Define supported cultures
    var cultures = new CultureInfo[] { new CultureInfo("en"), new CultureInfo("tr"), new CultureInfo("ar") };
    ops.SupportedCultures = cultures;
    ...
});  

// Register XmlResourceProvider to use XML files as resource files.
services.AddSingleton<IXResourceProvider, XmlResourceProvider>();

services.AddRazorPages()
        // LocSource: Dummy class for defining resource file object
        .AddXLocalizer<LocSource, MyMemoryTranslateService>(ops => 
        {
            // ResourcePath: The folder path to create resource files in
            ops.ResourcesPath = "LocalizationResources";
            ...
        });
````

So we have;
- three culture `en, ar, tr` 
- default resource type is `LocSource`
- resources folder is `LocalizationResources`

With this setup the resource files will be created as below:
````
> ProjectRootFolder\LocalizationResources\LocSource.en.xml
> ProjectRootFolder\LocalizationResources\LocSource.tr.xml
> ProjectRootFolder\LocalizationResources\LocSource.ar.xml
````

## When does XLocalizer creates resource files?
The resource files are created during runtime, once the page is visited `IStringLocalizer` will call the underlayer of the resource provider `XmlResourceProvider`, and it will create the relevant resource file for the **current culture**.

## How many resource files are created?
By default `XLocalizer` will create one resource file for each culture, but you are free to use as much resource files as you need depending on your project setup and requirements.

Let's assume that you are using below code for localizing a text in the view or in the backend, if you use `IStringLocalizer` as below only one resouerce file for each culture will be created:

````html
<!-- sample with XLocalizer.TagHelpers -->
<h1 localize-content>Welcome</h1>
````

or the equavilant traditional setup:
````html
<!-- sample without XLocalizer.TagHelpers -->
@inject Microsoft.Extensions.Localization.IStringLocalizer Localizer
<h1>@Localizer["Welcome"]</h1>
````

or the setup in the backend:
````csharp
public class IndexModel : PageModel
{
    private readonly IStringLocalizer _localizer;
    public IndexModel(IStringLocalizer localizer)
    {
        _localizer = localizer;
    }

    public IActionResult OnGet()
    {
        var welcomText = _localizer["Welcome"];
    }
}
````

## Adding more resource files for each culture
You can use more resource files for each culture as much as you need by defining the new resource type in `IStringLocalizer<T>`. You can create a new resource type as a dummy class or just use any class/page type as type parameter:
````html
<!-- sample with XLocalizer.TagHelpers -->
<h1 localize-resource="typeof(IndexModel)">Welcome</h1>
````

or the equavilant traditional setup:
````html
<!-- sample without XLocalizer.TagHelpers -->
@inject Microsoft.Extensions.Localization.IStringLocalizer<IndexModel> Localizer
<h1>@Localizer["Welcome"]</h1>
````

or the setup in the backend:
````csharp
namespace MyProject.Pages
{
    public class IndexModel : PageModel
    {
        private readonly IStringLocalizer _localizer;
        public IndexModel(IStringLocalizer<IndexModel> localizer)
        {
            _localizer = localizer;
        }

        public IActionResult OnGet()
        {
            var welcomText = _localizer["Welcome"];
        }
    }
}
````

In this case `XLocalizer` will create another resource file with the fully qualified name for each culture in addition to the default one defined in startup which is mandatory.
````
> ProjectRootFolder\LocalizationResources\LocSource.en.xml
> ProjectRootFolder\LocalizationResources\LocSource.tr.xml
> ProjectRootFolder\LocalizationResources\LocSource.ar.xml

> ProjectRootFolder\LocalizationResources\Pages.IndexModel.en.xml
> ProjectRootFolder\LocalizationResources\Pages.IndexModel.tr.xml
> ProjectRootFolder\LocalizationResources\Pages.IndexModel.ar.xml
````

There is no specific implementation type for the new resource type, any class type will do the job. So if you are working on a big project with many different areas, you may create one resource file for each area, or just add as much resource files as you need for each culture, or just use one resource file for each culture.

### Notice
When you use more than one resource file for each culture, the default error messages for [data annotations][3], [model binding][4] and [identity errors][5] will be located in the default resource type defined in startup.

## Creating RESX resources
With the [built-in exporter][2] you can export all your automatically created resources to resx resources with their respective naming kept.

## What about DB based localization
The way of dealing with resources in [DB based localization][6] is quite the same, the difference is in DB we use tables instead of files, and the tables must be existing in advance. So, if you want to use more than one table for localized resources you need to create them first then use the relevant table type as parameter with `IStringLocalizer<T>`.

[1]:setup-xml.md
[2]:export-xml-to-resx.md
[3]:localizing-validation-attributes-errors.md
[4]:model-binding-errors.md
[5]:identity-errors.md
[6]:setup-db.md