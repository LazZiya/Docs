<!-- meta tags details, will be assigned to meta tags inside header by js -->
<div id="meta-info">
<details><summary>meta info</summary>

> * Title: <i id="md-title">Two resource files for each culture</i>
> * Keywords: <i id="md-keywords">localization, asp.net-core, express-localization</i>
> * Description: <i id="md-description">Use two resource files for each culture in ExpressLocalization.</i>
> * Author: <i id="md-author">Ziya Mollamahmut</i>
> * Date: <i id="md-date">08-Aug-2020</i>
> * Image: <i id="md-image">https://github.com/LazZiya/Docs/raw/master/LazZiya.ExpressLocalization/v4.0/images/lazziya-express-localization-logo.png</i>
> * Image-alt: <i id="md-image-alt">LazZiya.ExpressLocalization Logo</i>
> * Version: <i id="md-version">v4.0</i>

</details>
</div>

> #### IMPORTANT NOTICE!
> This library is not maintained. Please upgrade to [XLocalizer][0] for a newer and easier localization experience.

# Two resource files for each culture

By [Ziya Mollamahmut](https://github.com/LazZiya)

Some localized resources are fixed for all projects (e.g.: Data annotations errors, identity errors, model binding errors). So, it can be useful to have separate resource file for these framework messages, and another resource file for views.
- Create empty class for framework messages under _LocalizationResources_ folder and name it: `LocSourceData.cs`
````csharp
public class LocSourceData
{
}
````

- Create empty class for views localization under _LocalizationResources_ folder and name it: `LocSourceViews.cs`
````csharp
public class LocSourceViews
{
}
````

- Setup ExpressLocalization to use two resource files:
````csharp
services.AddRazorPages()
    .AddExpressLocalization<LocSourceData, LocSourceViews>(ops => 
    {
        /* Add options here*/
    });
````


> Notice: the above code demonstrats only the differentiated part for localizing with two resource files, the rest of the code must be done as described in **[Setup for Razor Pages][1]**


- Create two resource files for each culture in the same folder for our dummy classes:
  - Turkish culture:
    - LocSourceData.tr.resx
    - LocSourceViews.tr.resx
  - Arabic culture:
    - LocSourceData.ar.resx
    - LocSourceViews.ar.resx

[0]:https://docs.ziyad.info/en/XLocalizer/v1.0/index.md
[1]:Setup-for-Razor-Pages.md