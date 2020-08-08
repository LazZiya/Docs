---
title: Four resource files for each culture
keywords: localization, asp.net-core, express-localization
description: Use four resource files for each culture in ExpressLocalization.
author: Ziya Mollamahmut
date: 08-Aug-2020
versions: 1.x, 2.x, 3.x, 4.x
---

# Four resource files for each culture

By [Ziya Mollamahmut](https://github.com/LazZiya)

If you still want to split error messages to different resource files, you can create a resource file for each type as below:
- Create a dummy class for views localization `LocSourceViews.cs`
````csharp
public class LocSourceViews
{
}
````

- Create a dummy class for data annotations errors localization `LocSourceData.cs`
````csharp
public class LocSourceData
{
}
````

- Create a dummy class for model binding errors localization `LocSourceModelBinding.cs`
````csharp
public class LocSourceModelBinding
{
}
````

- Create a dummy class for identity errors localization `LocSourceIdentity.cs`
````csharp
public class LocSourceIdentity
{
}
````

- Setup `ExpressLocalization` to use four resource files:
````csharp
services.AddRazorPages()
    .AddExpressLocalization<LocSourceViews, LocSourceData, LocSourceModelBinding, LocSourceDataIdentity>(ops => 
    {
        /* Add options here */
    });
````

> Notice: the above code demonstrats only the differentiated part for localizing with four resource files, the rest of the code must be done as described in **[Setup for Razor Pages][1]**


- Create four resource files for each culture in the same folder with the dummy classes:
  - Turkish culture:
    - LocSourceViews.tr.resx
    - LocSourceData.tr.resx
    - LocSourceModelBinding.tr.resx
    - LocSourceIdentity.tr.resx
  - Arabic culture:
    - LocSourceViews.ar.resx
    - LocSourceData.ar.resx
    - LocSourceModelBinding.ar.resx
    - LocSourceIdentity.ar.resx

[1]:../LazZiya.ExpressLocalization/Setup-for-Razor-Pages.md