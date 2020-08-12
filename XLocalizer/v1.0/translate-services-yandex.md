---
title: Use Yandex Translate For Localization
keywords: localization, asp.net-core, translate, online, yandex, service
description: Learn how to use yandex translation service for localization of Asp.Net Core web apps with XLocalizer.Translate.
author: Ziya Mollamahmut
date: 08-Aug-2020
versions: 1.0
---

# Use Yandex Translate For Localization

By [Ziya Mollamahmut](https://github.com/LazZiya)

This nuget is based on the free plan of [Yandex Translate](https://tech.yandex.com/translate/).

> See [GitHub repo](https://github.com/LazZiya/XLocalizer.Translate.YandexTranslate)

**Install**
````
PM > Install-Package XLocalizer.Translate.YandexTranslate
````

**Add Yandex Translate API key to user secrets**
> Right click on the project name and select _Manage User Secrets_, then add the API key as below:

````json
{
  "XLocalizer.Translate": {
    "YandexTranslateApiKey": "xxx-yandex-translate-api-key-xxx"
  }
}
````

**Register in startup**
````csharp
using XLocalizer.Translate
using XLocalizer.Translate.YandexTranslate

services.AddHttpClient<ITranslator, YandexTranslateService>();
````

**Use with XLocalizer**
````csharp
// Configure XLocalizer to use the translation service 
// and enable online translation
services.AddRazorPages()
        .AddXLocalizer<LocSource, YandexTranslateService>(ops =>
        {
            // ...
            ops.AutoTranslate = true;
        });
````


