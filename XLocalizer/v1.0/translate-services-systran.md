<!-- meta tags details, will be assigned to meta tags inside header by js -->
<div id="meta-info">
<details><summary>meta info</summary>

> * Title: <i id="md-title">Use SYSTRAN.io Translation For Localization</i>
> * Keywords: <i id="md-keywords">localization, asp.net-core, translate, online, systran.io, service</i>
> * Description: <i id="md-description">Learn how to use systran.io translation service for localization of Asp.Net Core web apps with XLocalizer.Translate.</i>
> * Author: <i id="md-author">Ziya Mollamahmut</i>
> * Date: <i id="md-date">08-Aug-2020</i>
> * Image: <i id="md-image">https://github.com/LazZiya/Docs/raw/master/XLocalizer/v1.0/images/xlocalizer-logo.png</i>
> * Image-alt: <i id="md-image-alt">XLocalizer Logo</i>
> * Version: <i id="md-version">v1.0</i>

</details>
</div>

# Use SYSTRAN.io Translate For Localization

By [Ziya Mollamahmut](https://github.com/LazZiya)

This nuget is based on the free plan of [Systran Translate via RapidAPI][2].

> See [GitHub repo](https://github.com/LazZiya/XLocalizer.Translate.SystranTranslate)

**Install**
````
PM > Install-Package XLocalizer.Translate.SystranTranslate
````

- [Click here to get an API key from RapidApi][1]
- Add RapidAPI key to user secrets

````json
{
  "XLocalizer.Translate": {
    "RapidApiKey": "...",
  }
}
````
> <small>Right click on the project name and select **_Manage User Secrets_**</small>

**Register in startup**
````csharp
services.AddHttpClient<ITranslator, SystranTranslateServiceRapidApi>();
````

**Use with XLocalizer**
````csharp
// Configure XLocalizer to use the translation service 
// and enable online translation
services.AddRazorPages()
        .AddXLocalizer<LocSource, SystranTranslateServiceRapidApi>(ops =>
        {
            // ...
            ops.AutoTranslate = true;
        });
````



[1]:https://rapidapi.com/developer/apps
[2]:https://rapidapi.com/systran/api/systran-io-translation-and-nlp