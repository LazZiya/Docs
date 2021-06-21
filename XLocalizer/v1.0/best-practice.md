<!-- meta tags details, will be assigned to meta tags inside header by js -->
<div id="meta-info">
<details><summary>meta info</summary>

> * Title: <i id="md-title">XLocalizer Best Practice and Recommendations</i>
> * Keywords: <i id="md-keywords">localization, asp.net-core, xlocalizer, best, practice</i>
> * Description: <i id="md-description">Best practices and recomendations to get the best performance and optimal results from XLocalizer.</i>
> * Author: <i id="md-author">Ziya Mollamahmut</i>
> * Date: <i id="md-date">21-Jun-2021</i>
> * Image: <i id="md-image">https://github.com/LazZiya/Docs/raw/master/XLocalizer/v1.0/images/xlocalizer-logo.png</i>
> * Image-alt: <i id="md-image-alt">XLocalizer Logo</i>
> * Version: <i id="md-version">v1.0</i>

</details>
</div>

# Best Practices To Get The Best From XLocalizer
Here are the recommended steps for developers to follow to achive the best performance and results from XLocalizer. However, depending on your setup and project you may follow different steps according to your requirements.

1. Use [XML][2] or [DB][3] as resource provider.
2. Register any supported [online translation service][6].
3. While in **development mode**, disable `AutoTranslate`, `AutoAddKeys` and `UseExpressMemoryCache` on XLocalizer options.
````csharp
ops.AutoTranslate = false;
ops.AutoAddKeys = false;
ops.UseExpressMemoryCache = false;
````
> The reasone why: during development many texts are subject to change, so you don't need to translate and add unnessary keys to the resource files.

4. When you are sure that all the texts _or most of them_ are fixed, enable `AutoTranslate`, `AutoAddKeys` and keep `UseExpressMemoryCache` disabled till all translation are done, saved and validated.
````csharp
ops.AutoTranslate = true;
ops.AutoAddKeys = true;
ops.UseExpressMemoryCache = false;
````
5. Run the app and switch to all available cultures till you are sure that all pages are visited. So `XLocalizer` can add all keys and translations to the resource files/db.
6. _(recommended)_ After all translations are done correctly, you can enable `UseExpressMemoryCache` in XLocalizer options; this will cache localized keys in memory for faster access.
7. _(optional)_ Disable `AutoTranslate` and `AutoAddKeys` in XLocalizer options.
8. _(optional)_ if you want to use [RESX][4] as resource files for localization in production, you can use the built-in export module to export the localized keys to .resx files.
- [Export from XML to RESX][7]
- [Export from DB to RESX][8]
9. Add a star to [XLocalizer in github][9] :) [![GitHub Stars](https://shields.io/github/stars/LazZiya/XLocalizer?label=Stars&style=social)](https://github.com/LazZiya/XLocalizer)


[1]:.
[2]:setup-xml.md
[3]:setup-db.md
[4]:setup-resx.md
[5]:.
[6]:translate-services.md
[7]:export-xml-to-resx.md
[8]:export-db-to-resx.md
[9]:https://github.com/LazZiya/XLocalizer