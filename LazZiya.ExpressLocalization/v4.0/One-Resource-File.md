<!-- meta tags details, will be assigned to meta tags inside header by js -->
<div id="meta-info">
<details><summary>meta info</summary>

> * Title: <i id="md-title">One resource file for each culture</i>
> * Keywords: <i id="md-keywords">localization, asp.net-core, express-localization</i>
> * Description: <i id="md-description">Use one resource file for each culture in ExpressLocalization.</i>
> * Author: <i id="md-author">Ziya Mollamahmut</i>
> * Date: <i id="md-date">08-Aug-2020</i>
> * Image: <i id="md-image">https://github.com/LazZiya/Docs/raw/master/LazZiya.ExpressLocalization/v4.0/images/lazziya-express-localization-logo.png</i>
> * Image-alt: <i id="md-image-alt">LazZiya.ExpressLocalization Logo</i>
> * Version: <i id="md-version">v4.0</i>

</details>
</div>

> #### IMPORTANT NOTICE!
> This library is not maintained. Please upgrade to [XLocalizer][0] for a newer and easier localization experience.

# One resource file for each culture

By [Ziya Mollamahmut](https://github.com/LazZiya)

### One resource file for each culture:
All localized strings for views, data annotations, identity errors ...etc. will take place in one resource file.
- Create a new folder named "LocalizationResources" and create an empty class inside it and name it `LocSource.cs`
````csharp
public class LocSource
{
}
````
- Setup `ExpressLocalization` to use one resource file:
````csharp
services.AddRazorPages()
    .AddExpressLocalization<LocSource>(ops => 
    {
        /* Add options here */
    });
````


> Notice: the above code demonstrats only the differentiated part for localizing with one resource file, the rest of the code must be done as described in **[Setup for Razor Pages][1]**


- Create one resource file for each culture in the same folder with our dummy class `LocSource.cs`:
  - LocSource.tr.resx
  - LocSource.ar.resx

[0]:https://docs.ziyad.info/en/XLocalizer/v1.0/index.md
[1]:Setup-for-Razor-Pages.md