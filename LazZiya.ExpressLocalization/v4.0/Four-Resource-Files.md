<!-- meta tags details, will be assigned to meta tags inside header by js -->
<div id="meta-info">
<details><summary>meta info</summary>

> * Title: <i id="md-title">Four resource files for each culture</i>
> * Keywords: <i id="md-keywords">localization, asp.net-core, express-localization</i>
> * Description: <i id="md-description">Use four resource files for each culture in ExpressLocalization.</i>
> * Author: <i id="md-author">Ziya Mollamahmut</i>
> * Date: <i id="md-date">08-Aug-2020</i>
> * Image: <i id="md-image">https://github.com/LazZiya/Docs/raw/master/LazZiya.ExpressLocalization/v4.0/images/lazziya-express-localization-logo.png</i>
> * Image-alt: <i id="md-image-alt">LazZiya.ExpressLocalization Logo</i>
> * Version: <i id="md-version">v4.0</i>

</details>
</div>

# Four resource files for each culture

By [Ziya Mollamahmut](https://github.com/LazZiya)

If you still want to split error messages to different resource files, you can create a resource file for each type as below:
- Create a dummy class for views localization `LocSourceViews.cs`
````csharp
public class LocSourceViews
{
}
````

- Create a dummy class for data annotations errors localization `LocSourceData.cs`
````csharp
public class LocSourceData
{
}
````

- Create a dummy class for model binding errors localization `LocSourceModelBinding.cs`
````csharp
public class LocSourceModelBinding
{
}
````

- Create a dummy class for identity errors localization `LocSourceIdentity.cs`
````csharp
public class LocSourceIdentity
{
}
````

- Setup `ExpressLocalization` to use four resource files:
````csharp
services.AddRazorPages()
    .AddExpressLocalization<LocSourceViews, LocSourceData, LocSourceModelBinding, LocSourceDataIdentity>(ops => 
    {
        /* Add options here */
    });
````

> Notice: the above code demonstrats only the differentiated part for localizing with four resource files, the rest of the code must be done as described in **[Setup for Razor Pages][1]**


- Create four resource files for each culture in the same folder with the dummy classes:
  - Turkish culture:
    - LocSourceViews.tr.resx
    - LocSourceData.tr.resx
    - LocSourceModelBinding.tr.resx
    - LocSourceIdentity.tr.resx
  - Arabic culture:
    - LocSourceViews.ar.resx
    - LocSourceData.ar.resx
    - LocSourceModelBinding.ar.resx
    - LocSourceIdentity.ar.resx

[1]:Setup-for-Razor-Pages.md