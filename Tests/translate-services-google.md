---
title: Use Google Translate For Localization
keywords: localization, asp.net-core, translate, online, google, service
description: Learn how to use google translate service for localization of Asp.Net Core web apps with XLocalizer.Translate.
author: Ziya Mollamahmut
date: 08-Aug-2020
versions: 1.0
---

# Use Google Translate For Localization

By [Ziya Mollamahmut][0]

This nuget is based on the freemium plan of [Google Translate via RapidAPI](https://rapidapi.com/googlecloud/api/google-translate1).
> See [GitHub repo](https://github.com/LazZiya/XLocalizer.Translate.GoogleTranslate/)

**Install**
````
PM > Install-Package XLocalizer.Translate.GoogleTranslate
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
using XLocalizer.Translate.GoogleTranslate

services.AddHttpClient<ITranslator, GoogleTranslateService>();
````

**Use with XLocalizer**
````csharp
// Configure XLocalizer to use the translation service 
// and enable online translation
services.AddRazorPages()
        .AddXLocalizer<LocSource, GoogleTranslateService>(ops =>
        {
            // ...
            ops.AutoTranslate = true;
        });
````

[0]:https://github.com/LazZiya