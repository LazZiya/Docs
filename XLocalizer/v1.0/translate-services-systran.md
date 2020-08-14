<!-- meta tags details, will be assigned to meta tags inside header by js -->
<div id="meta-info">
<details><summary>meta info</summary>

> * Title: <i id="md-title">Use SYSTRAN.io Translation For Localization</i>
> * Keywords: <i id="md-keywords">localization, asp.net-core, translate, online, systran.io, service</i>
> * Description: <i id="md-description">Learn how to use systran.io translation service for localization of Asp.Net Core web apps with XLocalizer.Translate.</i>
> * Author: <i id="md-author">Ziya Mollamahmut</i>
> * Date: <i id="md-date">08-Aug-2020</i>
> * Image: <i id="md-image">https://github.com/LazZiya/Docs/raw/vNext/XLocalizer/v1.0/images/xlocalizer-logo.png</i>
> * Image-alt: <i id="md-image-alt">XLocalizer Logo</i>
> * Version: <i id="md-version">v1.0</i>

</details>
</div>

# Use SYSTRAN.io Translate For Localization

By [Ziya Mollamahmut](https://github.com/LazZiya)

This nuget is based on the free plan of [Systran Translate via RapidAPI](https://rapidapi.com/systran/api/systran-io-translation-and-nlp).

> See [GitHub repo](https://github.com/LazZiya/XLocalizer.Translate.SystranTranslate)

**Install**
````
PM > Install-Package XLocalizer.Translate.SystranTranslate
````

**Add RapidAPI key to user secrets**
> Right click on the project name and select _Manage User Secrets_, then add the API key as below:

````json
{
  "XLocalizer.Translate": {
    "RapidApiKey": "xxx-rapid-api-key-xxx",
  }
}
````

**Register in startup**
````csharp
using XLocalizer.Translate
using XLocalizer.Translate.YandexTranslate

services.AddHttpClient<ITranslator, SystranTranslateService>();
````

**Use with XLocalizer**
````csharp
// Configure XLocalizer to use the translation service 
// and enable online translation
services.AddRazorPages()
        .AddXLocalizer<LocSource, SystranTranslateService>(ops =>
        {
            // ...
            ops.AutoTranslate = true;
        });
````


