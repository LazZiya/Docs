<!-- meta tags details, will be assigned to meta tags inside header by js -->
<div id="meta-info">
<details><summary>meta info</summary>

> * Title: <i id="md-title">Export localized resources from XML to RESX</i>
> * Keywords: <i id="md-keywords">localization, asp.net-core, xlocalizer, export, xml, resx</i>
> * Description: <i id="md-description">Learn how to export the localized resources from xml to resx resource file with XLocalizer.</i>
> * Author: <i id="md-author">Ziya Mollamahmut</i>
> * Date: <i id="md-date">03-Sep-2020</i>
> * Image: <i id="md-image">https://github.com/LazZiya/Docs/raw/master/XLocalizer/v1.0/images/xlocalizer-logo.png</i>
> * Image-alt: <i id="md-image-alt">XLocalizer Logo</i>
> * Version: <i id="md-version">v1.0</i>

</details>
</div>

# Export localized resources from XML to RESX

By [Ziya Mollamahmut](https://github.com/LazZiya)

The ability to export resources provides flexibility in switching between different resource types, and ease of work on localization by exporting resources to any custom format using custom exporters. The built-in exporters supports exporting from XML to RESX, but you can implement your own exporter to any format.

#### How to use the built-in XML-to-RESX exporter
Simply inject [`IXResourceExporter`][1] and call the export method. Below is a razor page sample;

````csharp
public class ExportModel : PageModel
{
    private readonly IXResourceExporter _exporter;
    private readonly ILogger _logger;
    
    public ExportModel(IXResourceExporter exporter, ILogger<ExportModel> logger)
    {
        _exporter = exporter;
        _logger = logger;
    }

    public void OnGet() { }

    public async Task<IActionResult> OnPostAsync(string culture, bool approvedOnly, bool overwrite)
    {
        var totalExported = await _exporter.ExportToResxAsync<LocSource>(culture, approvedOnly, overwrite);

        _logger.LogInformation($"Total {totalExported} resources exported.");

        return Page();
    }
}
````

#### How to create custom resource exporter
Create a new class that implements [`IXResourceExporter`][1] and register it in startup.

````csharp
public class CustomResourceExporter : IXResourceExporter
{
    public CustomResourceExporter() 
    {
        // ...
    }

    public async Task<int> ExportToResxAsync<TResource>(string culture, bool approvedOnly, bool overwriteExistingKeys)
            where TResource : class
    {
        // ...
    }

    public async Task<int> ExportToResxAsync(Type type, string culture, bool approvedOnly, bool overwriteExistingKeys)
    {
        // ...
    }
}
````

Register in startup:
````csharp
services.AddTransient<IXResourceExporter, CustomResourceExporter>();
````

See the built-in xml resource exporter source code: [`XmlResourceExporter`][2]

**Export method parameters**
* TResource / type: Type of resource file
* culture: The culture to export its resources
* approvedOnly: Export only resources with approved translations. Auto translated xml resources has the attribute isActive set to false by default.
* overwriteExistingKeys: Over write existing resources if any...
    


[1]:https://github.com/LazZiya/XLocalizer/blob/master/XLocalizer/IXResourceExporter.cs
[2]:https://github.com/LazZiya/XLocalizer/blob/master/XLocalizer/Xml/XmlResourceExporter.cs