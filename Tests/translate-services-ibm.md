---
title: Use IBM Watson Language Translator For Localization
keywords: localization, asp.net-core, translate, online, ibm, watson, language, translator, service
description: Learn how to use ibm watson language translator service for localization of Asp.Net Core web apps with XLocalizer.Translate.
author: Ziya Mollamahmut
date: 08-Aug-2020
versions: 1.0
---

# Use IBM Watson Language Translator For Localization

By [Ziya Mollamahmut][0]

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

[0]:https://github.com/LazZiya