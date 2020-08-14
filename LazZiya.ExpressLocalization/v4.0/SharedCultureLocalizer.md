<!-- meta tags details, will be assigned to meta tags inside header by js -->
<div id="meta-info">
<details><summary>meta info</summary>

> * Title: <i id="md-title">SharedCultureLocalizaer for ExpressLocalization</i>
> * Keywords: <i id="md-keywords">localization, asp.net-core, mvc</i>
> * Description: <i id="md-description">SharedCultureLocalizder in ExpressLocalization for Asp.Net Core.</i>
> * Author: <i id="md-author">Ziya Mollamahmut</i>
> * Date: <i id="md-date">08-Aug-2020</i>
> * Image: <i id="md-image">https://github.com/LazZiya/Docs/raw/master/LazZiya.ExpressLocalization/v4.0/images/lazziya-express-localization-logo.png</i>
> * Image-alt: <i id="md-image-alt">LazZiya.ExpressLocalization Logo</i>
> * Version: <i id="md-version">v4.0</i>

</details>
</div>

# SharedCultureLocalizaer for ExpressLocalization

By [Ziya Mollamahmut](https://github.com/LazZiya)

The other option to localize views is using the built-in [`ISharedCultureLocalizer`][1]

- Inject [`ISharedCultureLocalizer`][1] into the view:
````html
@using LazZiya.ExpressLocalization
@inject ISharedCultureLocalizer _loc
````
- call localization function to get localized strings in views:
````html
<h1 class="display-4">@_loc["Welcome"]</h1>
````

But when it comes to localize long strings with html tags this approach become unfriendly. That's why the recommended localization approach is using [`Localize TagHelper`][2].

[1]:https://github.com/LazZiya/ExpressLocalization/blob/master/LazZiya.ExpressLocalization/ISharedCultureLocalizer.cs
[2]:Localize-TagHelper.md

### Applies to ExpressLocalization versions:
 4.0