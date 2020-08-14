<!-- meta tags details, will be assigned to meta tags inside header by js -->
<div id="meta-info">
<details><summary>meta info</summary>

> * Title: <i id="md-title">Validating Localized Input</i>
> * Keywords: <i id="md-keywords">localization, asp.net-core, validatin, locailzed, input, decimal</i>
> * Description: <i id="md-description">Learn how to valdiate locaized input like decimal numbers in Asp.Net Core web apps with XLocalizer.</i>
> * Author: <i id="md-author">Ziya Mollamahmut</i>
> * Date: <i id="md-date">08-Aug-2020</i>
> * Image: <i id="md-image">https://github.com/LazZiya/Docs/raw/vNext/XLocalizer/v1.0/images/xlocalizer-logo.png</i>
> * Image-alt: <i id="md-image-alt">XLocalizer Logo</i>
> * Version: <i id="md-version">v1.0</i>

</details>
</div>

# Validating Localized Input

By [Ziya Mollamahmut](https://github.com/LazZiya)

Some input fields need to be localized (decimal numbers, dates, ...etc.). But without client side localizing libraries this could make problems with different cultures (e.g. decimal numbers 1.23 and 1,23).

To have client side validation full compatibility with all cultures see [`LocalizationValdiationScripts`][1] taghelper from [`LazZiya.TagHelpers`][2]


[1]:../../LazZiya.TagHelpers/v5.0/LocalizationValidationScripts-TagHelper-Setup.md
[2]:https://github.com/LazZiya/TagHelpers