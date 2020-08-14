<!-- meta tags details, will be assigned to meta tags inside header by js -->
<div id="meta-info">
<details><summary>meta info</summary>

> * Title: <i id="md-title">Localizing Custom Backend Messages</i>
> * Keywords: <i id="md-keywords">localization, asp.net-core, backend, error, messages, custom</i>
> * Description: <i id="md-description">Learn how to localize custom backend error messages in Asp.Net Core web app.</i>
> * Author: <i id="md-author">Ziya Mollamahmut</i>
> * Date: <i id="md-date">08-Aug-2020</i>
> * Image: <i id="md-image">https://github.com/LazZiya/Docs/raw/master/XLocalizer/v1.0/images/xlocalizer-logo.png</i>
> * Image-alt: <i id="md-image-alt">XLocalizer Logo</i>
> * Version: <i id="md-version">v1.0</i>

</details>
</div>

# Localizing Custom Backend Messages

By [Ziya Mollamahmut](https://github.com/LazZiya)

Custom backend error messages can be localized by injecting `IStringLocalizer`, `IHtmlLocalizer`, `IStringLocalizerFactory` or `IHtmlLocalizerFactory` to the controller or PageModel as below:

````csharp
using LazZiya.ExpressLocalization

public class IndexModel : PageModel
{
    private readonly IStringLocalizer _loc;

    public string CustomMessage { get; set; }

    public IndexModel(IStringLocalizer loc)
    {
        _loc = loc;
    }

    public void OnGet() 
    {
        CustomMessage = _loc["Localized custom backend message"];
    }
}
````

By default, XLocalizer will use one shared resource _the one we used in startup setup **LocSource**_.

If you want to use a different resource, just pass its type into the localizer interface, :
````csharp
private readonly IStringLocalizer _loc;

public IndexModel(IStringLocalizer<IndexModel> loc)
{
    _loc = loc;
}
```` 

Or create the localizer using the factory:
````csharp
private readonly IStringLocalizer _loc;

public IndexModel(IStringLocalizerFactory factory)
{
    _loc = factory.Create(typeof(MyResourcetype));
}
```` 

Notices
 - **XML based localization:** If the resource file is not found it will be created automatically by `XLocalizer`, but the folder must exists.
 - **RESX based localization:** The resource file must be created manually, or can be created automatically by exporting from XML or DB.
 - **DB based localization:** The type passed must be relevant to an existing DB table that implements [`IXDbResource`][1] interface.


#
### Next: [Add language navigation][2]
#


[1]:https://github.com/LazZiya/XLocalizer.DB/blob/master/XLocalizer.DB/Models/IXDbResource.cs
[2]:language-navigation.md
