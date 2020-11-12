<!-- meta tags details, will be assigned to meta tags inside header by js -->
<div id="meta-info">
<details><summary>meta info</summary>

> * Title: <i id="md-title">Use Microsoft Translation For Localization</i>
> * Keywords: <i id="md-keywords">localization, asp.net-core, translate, online, microsoft, service</i>
> * Description: <i id="md-description">Learn how to use mymemory translation service for localization of Asp.Net Core web apps with XLocalizer.Translate.</i>
> * Author: <i id="md-author">Ziya Mollamahmut</i>
> * Date: <i id="md-date">12-Nov-2020</i>
> * Image: <i id="md-image">https://github.com/LazZiya/Docs/raw/master/XLocalizer/v1.0/images/xlocalizer-logo.png</i>
> * Image-alt: <i id="md-image-alt">XLocalizer Logo</i>
> * Version: <i id="md-version">v1.0</i>

</details>
</div>

# Use Microsoft Translate For Localization

By [Ziya Mollamahmut](https://github.com/LazZiya)

This nuget containes two services, you can use any of them depending on your requirements:

- [`MicrosoftTranslateService`](#MicrosoftTranslateService): Directly connected to Microsoft Azure Translate Api's
- [`MicrosoftTranslateServiceRapidApi`](#MicrosoftTranslateServiceRapidApi): Based on Microsoft Translate services via RapidApi

> See [GitHub repo](https://github.com/LazZiya/XLocalizer.Translate.MicrosoftTranslate)

**Install**
````
PM > Install-Package XLocalizer.Translate.MicrosoftTranslate
````

### MicrosoftTranslateService
This service is directly connected to Microsoft Azure Translate Api's, and it offers free usage, but it requires a subscription!  

- [Click here to subscribe to Microsoft Azure Translation Api][1]
- After activating your account and adding Translator services, goto **Keys And Endpoints** and get the Api key and location _(Microsoft provides two keys but only one is enough)_.
- Add the key and the location to user secrets
````json
{
  "XLocalizer.Translate": {
    "Microsoft": {
        "Key": "...",
        "Location": "global"
    }
  }
}
````
> <small>Right click on the project name and select **_Manage User Secrets_**</small>

- Register in startup
````csharp
services.AddHttpClient<ITranslator, MicrosoftTranslateService>();
````

- Use with XLocalizer
````csharp
services.AddRazorPages()
        .AddXLocalizer<LocSource, MicrosoftTranslateService>(ops =>
        {
            // ...
            ops.AutoTranslate = true;
        });
````


---


### MicrosoftTranslateServiceRapidApi
This service is connected to RapidApi, and it requires a RapidApi key and a subscription to any paid or free plan. 
- [Click here to choose the right plan for you][3]
- [Click here to get a RapidApi key][4]

- Add RapidAPI key to user secrets
````json
{
  "XLocalizer.Translate": {
    "RapidApiKey": "...",
  }
}
````
> <small>Right click on the project name and select **_Manage User Secrets_**</small>

- Register in startup
````csharp
services.AddHttpClient<ITranslator, MicrosoftTranslateServiceRapidApi>();
````

- Use with XLocalizer
````csharp
services.AddRazorPages()
        .AddXLocalizer<LocSource, MicrosoftTranslateServiceRapidApi>(ops =>
        {
            // ...
            ops.AutoTranslate = true;
        });
````


[1]:https://azure.microsoft.com/en-us/services/cognitive-services/translator/
[2]:https://console.cloud.google.com/apis/credentials
[3]:https://rapidapi.com/microsoft-azure-org-microsoft-cognitive-services/api/microsoft-translator-text/pricing
[4]:https://rapidapi.com/developer/apps