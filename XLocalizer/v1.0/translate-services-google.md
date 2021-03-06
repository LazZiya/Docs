<!-- meta tags details, will be assigned to meta tags inside header by js -->
<div id="meta-info">
<details><summary>meta info</summary>

> * Title: <i id="md-title">Use Google Translation For Localization</i>
> * Keywords: <i id="md-keywords">localization, asp.net-core, translate, online, google, service</i>
> * Description: <i id="md-description">Learn how to use mymemory translation service for localization of Asp.Net Core web apps with XLocalizer.Translate.</i>
> * Author: <i id="md-author">Ziya Mollamahmut</i>
> * Date: <i id="md-date">12-Nov-2020</i>
> * Image: <i id="md-image">https://github.com/LazZiya/Docs/raw/master/XLocalizer/v1.0/images/xlocalizer-logo.png</i>
> * Image-alt: <i id="md-image-alt">XLocalizer Logo</i>
> * Version: <i id="md-version">v1.0</i>

</details>
</div>

# Use Google Translate For Localization

By [Ziya Mollamahmut](https://github.com/LazZiya)

This nuget containes two services, you can use any of them depending on your requirements:

- [`GoogleTranslateService`](#GoogleTranslateService): Directly connected to Google Translate Api's
- [`GoogleTranslateServiceRapidApi`](#GoogleTranslateServiceRapidApi): Based on Google Translate services via RapidApi

> See [GitHub repo](https://github.com/LazZiya/XLocalizer.Translate.GoogleTranslate)

**Install**
````
PM > Install-Package XLocalizer.Translate.GoogleTranslate
````

### GoogleTranslateService
This service is directly connected to Google Translate Api's, and it offers free usage, but it requires a subscription!  

- [Click here to subscribe to Google Cloud Translation Api][1]
- [Click here to create a credential and get an API key][2]
- Add the key and a valid email address to user secrets
````json
{
  "XLocalizer.Translate": {
    "Google": {
        "Key": "..."
    }
  }
}
````
> <small>Right click on the project name and select **_Manage User Secrets_**</small>

- Register in startup
````csharp
services.AddHttpClient<ITranslator, GoogleTranslateService>();
````

- Use with XLocalizer
````csharp
services.AddRazorPages()
        .AddXLocalizer<LocSource, GoogleTranslateService>(ops =>
        {
            // ...
            ops.AutoTranslate = true;
        });
````


---


### GoogleTranslateServiceRapidApi
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
services.AddHttpClient<ITranslator, GoogleTranslateServiceRapidApi>();
````

- Use with XLocalizer
````csharp
services.AddRazorPages()
        .AddXLocalizer<LocSource, GoogleTranslateServiceRapidApi>(ops =>
        {
            // ...
            ops.AutoTranslate = true;
        });
````


[1]:https://console.cloud.google.com/apis/library/translate.googleapis.com
[2]:https://console.cloud.google.com/apis/credentials
[3]:https://rapidapi.com/googlecloud/api/google-translate1/pricing
[4]:https://rapidapi.com/developer/apps