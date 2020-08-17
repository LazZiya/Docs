<!-- meta tags details, will be assigned to meta tags inside header by js -->
<div id="meta-info">
<details><summary>meta info</summary>

> * Title: <i id="md-title">Use IBM Watson Language Translator For Localization</i>
> * Keywords: <i id="md-keywords">localization, asp.net-core, translate, online, ibm, watson, language, translator, service</i>
> * Description: <i id="md-description">Learn how to use ibm watson language translator service for localization of Asp.Net Core web apps with XLocalizer.Translate.</i>
> * Author: <i id="md-author">Ziya Mollamahmut</i>
> * Date: <i id="md-date">08-Aug-2020</i>
> * Image: <i id="md-image">https://github.com/LazZiya/Docs/raw/master/XLocalizer/v1.0/images/xlocalizer-logo.png</i>
> * Image-alt: <i id="md-image-alt">XLocalizer Logo</i>
> * Version: <i id="md-version">v1.0</i>

</details>
</div>

# Use IBM Watson Language Translator For Localization

By [Ziya Mollamahmut](https://github.com/LazZiya)

This nuget is based on the free plan of [IBM Watson Language Translator](https://cloud.ibm.com/catalog/services/language-translator).

> See [GitHub repo](https://github.com/LazZiya/XLocalizer.Translate.IBMWatsonTranslate)

**Install**
````
PM > Install-Package XLocalizer.Translate.IBMWatsonTranslate
````

**Add API keys to user secrets**
> Right click on the project name and select _Manage User Secrets_, then add the API key as below:

````json
{
  "XLocalizer.Translate": {
    "IBMWatsonTranslateApiKey": "xxx-imb-watson-cloud-api-key-xxx",
    "IBMWatsonTranslateServiceUrl": "xxx-ibm-service-instance-xxx",
    "IBMWatsonTranslateServiceVersionDate": "xxx-ibm-service-version-date-xxx"
  }
}
````

**Register in startup**
````csharp
using XLocalizer.Translate
using XLocalizer.Translate.IBMWatsonTranslate

services.AddSingleton<ITranslator, IBMWatsonTranslateService>();
````

**Use with XLocalizer**
````csharp
// Configure XLocalizer to use the translation service 
// and enable online translation
services.AddRazorPages()
        .AddXLocalizer<LocSource, IBMWatsonTranslateService>(ops =>
        {
            // ...
            ops.AutoTranslate = true;
        });
````


