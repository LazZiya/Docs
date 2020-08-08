---
title: One resource file for each culture
keywords: localization, asp.net-core, express-localization
description: Use one resource file for each culture in ExpressLocalization.
author: Ziya Mollamahmut
date: 08-Aug-2020
versions: 1.x, 2.x, 3.x, 4.x
---

# One resource file for each culture

By [Ziya Mollamahmut](https://github.com/LazZiya)

### One resource file for each culture:
All localized strings for views, data annotations, identity errors ...etc. will take place in one resource file.
- Create a new folder named "LocalizationResources" and create an empty class inside it and name it `LocSource.cs`
````csharp
public class LocSource
{
}
````
- Setup `ExpressLocalization` to use one resource file:
````csharp
services.AddRazorPages()
    .AddExpressLocalization<LocSource>(ops => 
    {
        /* Add options here */
    });
````


> Notice: the above code demonstrats only the differentiated part for localizing with one resource file, the rest of the code must be done as described in **[Setup for Razor Pages][1]**


- Create one resource file for each culture in the same folder with our dummy class `LocSource.cs`:
  - LocSource.tr.resx
  - LocSource.ar.resx

[1]:../LazZiya.ExpressLocalization/Setup-for-Razor-Pages.md