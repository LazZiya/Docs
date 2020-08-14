<!-- meta tags details, will be assigned to meta tags inside header by js -->
<div id="meta-info">
<details><summary>meta info</summary>

> * Title: <i id="md-title">Express Localization</i>
> * Keywords: <i id="md-keywords">localization, asp.net-core, express-localization</i>
> * Description: <i id="md-description">All dirty localizaiton setup in simple steps.</i>
> * Author: <i id="md-author">Ziya Mollamahmut</i>
> * Date: <i id="md-date">08-Aug-2020</i>
> * Image: <i id="md-image">https://github.com/LazZiya/Docs/raw/master/LazZiya.ExpressLocalization/v4.0/images/lazziya-express-localization-logo.png</i>
> * Image-alt: <i id="md-image-alt">LazZiya.ExpressLocalization Logo</i>
> * Version: <i id="md-version">v4.0</i>

</details>
</div>

# Express Localization

By [Ziya Mollamahmut](https://github.com/LazZiya)

Less is more, do full localization in fewer steps...

Install from nuget :
````
Install-Package LazZiya.ExpressLocalization
````

## What is ExpressLocalization? 
A nuget package to simplify the localization setup of any Asp.Net Core web app to fewer steps. 

_ExpressLocalization_ does all below localization settings easily:

- Defines global route template by adding `{culture}` pattern to all routes, so urls will be like `http://www.example.com/en-US/`.
- Registers [`RouteSegmentRequestCultureProvider`][1], so culture selection can be based on route value.
- Defines [`SharedCultureLocalizer`][3] for localizing all razor pages depending on a shared resource.
- Localization of all DataAnnotations error messages.
- Localization of ModelBinding error messages.
- Localizing IdentityDescriber errors messages.
- Registers client side validation libraries for validating localized input fields like decimal numbers. 
- Configures app cookie to add `{culture}` value to the redirect paths when redirect events are invoked.

Some options requires installing additional nuget packages like : 
- [LazZiya.TagHelpers][5]

[1]:https://github.com/LazZiya/ExpressLocalization/blob/master/LazZiya.ExpressLocalization/RouteSegmentCultureProvider.cs
[3]:https://github.com/LazZiya/ExpressLocalization/blob/master/LazZiya.ExpressLocalization/SharedCultureLocalizer.cs
[5]:index.md