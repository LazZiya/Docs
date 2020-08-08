---
title: Use SYSTRAN.io Translation For Localization
keywords: localization, asp.net-core, translate, online, systran.io, service
description: Learn how to use systran.io translation service for localization of Asp.Net Core web apps with XLocalizer.Translate.
author: Ziya Mollamahmut
date: 08-Aug-2020
versions: 1.0
---

# Use SYSTRAN.io Translate For Localization

By [Ziya Mollamahmut][0]

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

[0]:https://github.com/LazZiya