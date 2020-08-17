<!-- meta tags details, will be assigned to meta tags inside header by js -->
<div id="meta-info">
<details><summary>meta info</summary>

> * Title: <i id="md-title">Localizing AlertTaghelper Contents in Asp.Net Core</i>
> * Keywords: <i id="md-keywords">asp.net-core, taghelpers, localizatin, alerts</i>
> * Description: <i id="md-description">Learn how to localize contents of AlertTagHelper from LazZiya.TagHelpers for Asp.Net Core.</i>
> * Author: <i id="md-author">Ziya Mollamahmut</i>
> * Date: <i id="md-date">08-Aug-2020</i>
> * Image: <i id="md-image">https://github.com/LazZiya/Docs/raw/master/LazZiya.TagHelpers/v5.0/images/lazziya-tagheleprs-logo.png</i>
> * Image-alt: <i id="md-image-alt">LazZiya.TagHelpers Logo</i>
> * Version: <i id="md-version">v5.0</i>

</details>
</div>

# Localizing AlertTaghelper Contents in Asp.Net Core

By [Ziya Mollamahmut](https://github.com/LazZiya)

All front-end and back-end alerts can be localized by parsing `IStringLocalizer` instance to the alert tag:

````html
@inject IStringLocalizer _localizer

<alert localizer="_localizer"></alert>
````

Or if hyou are using [`LazZiya.ExpressLocalization`][1] you can pass instance of [`ISharedCultureLocalizer`][2] as well:

````html
@inject ISharedCultureLocalizer _localizer

<alert localizer="_localizer"></alert>
````

---
### Applies to version:
5.0

[1]:../../LazZiya.ExpressLocalization/v4.0/index.md
[2]:https://github.com/LazZiya/ExpressLocalization/blob/master/LazZiya.ExpressLocalization/ISharedCultureLocalizer.cs