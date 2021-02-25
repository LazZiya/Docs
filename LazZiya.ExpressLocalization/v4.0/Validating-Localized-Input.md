<!-- meta tags details, will be assigned to meta tags inside header by js -->
<div id="meta-info">
<details><summary>meta info</summary>

> * Title: <i id="md-title">Validating Localized Input</i>
> * Keywords: <i id="md-keywords">localization, asp.net-core, mvc</i>
> * Description: <i id="md-description">Validating localized input with ExpressLocalization for Asp.Net Core.</i>
> * Author: <i id="md-author">Ziya Mollamahmut</i>
> * Date: <i id="md-date">08-Aug-2020</i>
> * Image: <i id="md-image">https://github.com/LazZiya/Docs/raw/master/LazZiya.ExpressLocalization/v4.0/images/lazziya-express-localization-logo.png</i>
> * Image-alt: <i id="md-image-alt">LazZiya.ExpressLocalization Logo</i>
> * Version: <i id="md-version">v4.0</i>

</details>
</div>

> #### IMPORTANT NOTICE!
> This library is not maintained. Please upgrade to [XLocalizer][0] for a newer and easier localization experience.

# Validating Localized Input

By [Ziya Mollamahmut](https://github.com/LazZiya)

Some input fields need to be localized (decimal numbers, dates, ...etc.). But without client side localizing libraries this could make problems with different cultures (e.g. decimal numbers 1.23 and 1,23).

To have client side validation full compatibility with all cultures see [`LocalizationValdiationScripts`][1] taghelper from [`LazZiya.TagHelpers`][2]

[0]:https://docs.ziyad.info/en/XLocalizer/v1.0/index.md
[1]:../../LazZiya.TagHelpers/v5.0/LocalizationValidationScripts-TagHelper-Setup.md
[2]:../../LazZiya.TagHelpers/v5.0/index.md

