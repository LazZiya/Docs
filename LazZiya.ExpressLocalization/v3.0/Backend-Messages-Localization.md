<!-- meta tags details, will be assigned to meta tags inside header by js -->
<div id="meta-info">
<details><summary>meta info</summary>

> * Title: <i id="md-title">Localization of Custom Backend Messages</i>
> * Keywords: <i id="md-keywords">localization, asp.net-core, express-localization, backend, error, custom</i>
> * Description: <i id="md-description">Localize custom backend error messages with ExpressLocalization in Asp.Net Core.</i>
> * Author: <i id="md-author">Ziya Mollamahmut</i>
> * Date: <i id="md-date">27-Sep-2019</i>
> * Image: <i id="md-image">https://github.com/LazZiya/Docs/raw/master/LazZiya.ExpressLocalization/v3.0/images/lazziya-express-localization-logo.png</i>
> * Image-alt: <i id="md-image-alt">LazZiya.ExpressLocalization Logo</i>
> * Version: <i id="md-version">v3.0</i>

</details>
</div>

# Localization of Custom Backend Messages

By [Ziya Mollamahmut](https://github.com/LazZiya)

Custom error messages can be localized by injecting [`ISharedCultureLocalizer`][1] to the controller or PageModel as below:

````csharp
using LazZiya.ExpressLocalization

public class IndexModel : PageModel
{
    private readonly ISharedCultureLocalizer _loc;

    public string CustomMessage { get; set; }

    public IndexModel(ISharedCultureLocalizer loc)
    {
        _loc = loc;
    }

    public void OnGet() 
    {
        CustomMessage = _loc["Localized custom backend message"];
    }
}
````


> Extra: If you want to have bootstrap styled messages (Success, Warning, Danger, etc.) I suggest you have a look at [AlertTagHelper][2] in [LazZiya.TagHelpers][3] nuget package.

[1]:https://github.com/LazZiya/ExpressLocalization/blob/master/LazZiya.ExpressLocalization/ISharedCultureLocalizer.cs
[2]:Alert-TagHelper-Overview.md
[3]:index.md