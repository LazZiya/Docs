<!-- meta tags details, will be assigned to meta tags inside header by js -->
<div id="meta-info">
<details><summary>meta info</summary>

> * Title: <i id="md-title">Use MyMemory Translation For Localization</i>
> * Keywords: <i id="md-keywords">localization, asp.net-core, translate, online, mymemory, service</i>
> * Description: <i id="md-description">Learn how to use mymemory translation service for localization of Asp.Net Core web apps with XLocalizer.Translate.</i>
> * Author: <i id="md-author">Ziya Mollamahmut</i>
> * Date: <i id="md-date">12-Nov-2020</i>
> * Image: <i id="md-image">https://github.com/LazZiya/Docs/raw/master/XLocalizer/v1.0/images/xlocalizer-logo.png</i>
> * Image-alt: <i id="md-image-alt">XLocalizer Logo</i>
> * Version: <i id="md-version">v1.0</i>

</details>
</div>

# Use MyMemory Translate For Localization

By [Ziya Mollamahmut](https://github.com/LazZiya)

This nuget containes two services, you can use any of them depending on your requirements:

- [`MyMemoryTranslateService`](#MyMemoryTranslateService): Directly connected to MyMemory Api's
- [`MyMemoryTranslateServiceRapidApi`](#MyMemoryTranslateServiceRapidApi): Based on MyMemory services via RapidApi

> See [GitHub repo](https://github.com/LazZiya/XLocalizer.Translate.MyMemoryTranslate)

**Install**
````
PM > Install-Package XLocalizer.Translate.MyMemoryTranslate
````

### MyMemoryTranslateService
This service is directly connected to MyMemory Api's, and it offers free anonymous usage, but the [daily limit][1] is low! However, you can increase the free daily usage by providing a valid email address and an API key that can be generated via [MyMemory: API key generator][2]. 

- [Click here to goto MyMemory API key generator][2]
- Add the key and a valid email address to user secrets
````json
{
  "XLocalizer.Translate": {
    "MyMemory": {
        "Key": "...",
        "Email": "..."
    }
  }
}
````
> <small>Right click on the project name and select **_Manage User Secrets_**</small>

- Register in startup
````csharp
services.AddHttpClient<ITranslator, MyMemoryTranslateService>();
````

- Use with XLocalizer
````csharp
services.AddRazorPages()
        .AddXLocalizer<LocSource, MyMemoryTranslateService>(ops =>
        {
            // ...
            ops.AutoTranslate = true;
        });
````


---


### MyMemoryTranslateServiceRapidApi
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
services.AddHttpClient<ITranslator, MyMemoryTranslateServiceRapidApi>();
````

- Use with XLocalizer
````csharp
services.AddRazorPages()
        .AddXLocalizer<LocSource, MyMemoryTranslateServiceRapidApi>(ops =>
        {
            // ...
            ops.AutoTranslate = true;
        });
````


[1]:https://mymemory.translated.net/doc/usagelimits.php
[2]:https://mymemory.translated.net/doc/keygen.php
[3]:https://rapidapi.com/translated/api/mymemory-translation-memory/pricing
[4]:https://rapidapi.com/developer/apps