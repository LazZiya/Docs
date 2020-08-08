---
title: Two resource files for each culture
keywords: localization, asp.net-core, express-localization
description: Use two resource files for each culture in ExpressLocalization.
author: Ziya Mollamahmut
date: 08-Aug-2020
versions: 1.x, 2.x, 3.x, 4.x
---

# Two resource files for each culture

By [Ziya Mollamahmut](https://github.com/LazZiya)

Some localized resources are fixed for all projects (e.g.: Data annotations errors, identity errors, model binding errors). So, it can be useful to have separate resource file for these framework messages, and another resource file for views.
- Create empty class for framework messages under _LocalizationResources_ folder and name it: `LocSourceData.cs`
````csharp
public class LocSourceData
{
}
````

- Create empty class for views localization under _LocalizationResources_ folder and name it: `LocSourceViews.cs`
````csharp
public class LocSourceViews
{
}
````

- Setup ExpressLocalization to use two resource files:
````csharp
services.AddRazorPages()
    .AddExpressLocalization<LocSourceData, LocSourceViews>(ops => 
    {
        /* Add options here*/
    });
````


> Notice: the above code demonstrats only the differentiated part for localizing with two resource files, the rest of the code must be done as described in **[Setup for Razor Pages][1]**


- Create two resource files for each culture in the same folder for our dummy classes:
  - Turkish culture:
    - LocSourceData.tr.resx
    - LocSourceViews.tr.resx
  - Arabic culture:
    - LocSourceData.ar.resx
    - LocSourceViews.ar.resx

[1]:../LazZiya.ExpressLocalization/Setup-for-Razor-Pages.md