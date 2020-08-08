---
title: Custom Resource Provider
keywords: localization, asp.net-core, resource, provider, cusotm
description: Learn how to create custom resource provider to store localized resources in custom file types files with XLocalizer.
author: Ziya Mollamahmut
date: 08-Aug-2020
versions: 1.0
---

# Custom Resource Provider

By [Ziya Mollamahmut](https://github.com/LazZiya)

Resource providers are responsible for doing read/write operations for the resource files. `XLocalizer` has built-in support for _.resx, .xml_ file types. Additionally it has support for DB with EF (requires [`XLocalizer.DB`][1]).

#### Extending source types
You can use any custom file/db type for storing localized strings by implementing [`IXResourceProvider`][2] interface for file based types (e.g.: json, csv, ...etc.) or [`IDbResourceProvider`][3] interface for DB sources.


#### File based sources
A good sample is the built-in [`XmlResourceProvider`][4]. All you have to do after implementing your custom provider is to register it in startup:

````csharp
services.AddSingleton<IXResourceProvider, MyCustomProvider>();

services.AddRazorPages()
        .AddXLocalizer<LocSource>(...)
````

#### DB sources
You can have a look at the [`EFDbResourceProvider`][5], it has been built with EF support, but you can create your own DB resource provider by implementing [`IDbResourceProvider`][3] and registering it in startup:

````csharp
services.AddSingleton<IXDbResourceProvider, MyCustomDbProvider>();

services.AddRazorPages()
        .AddXDbLocalizer<ApplicatonDbContext>(...)
````


[1]:../XLocalizer/setup-db.md
[2]:https://github.com/LazZiya/XLocalizer/blob/master/XLocalizer/IXResourceProvider.cs
[3]:https://github.com/LazZiya/XLocalizer.DB/blob/master/XLocalizer.DB/IDbResourceProvider.cs
[4]:https://github.com/LazZiya/XLocalizer/blob/master/XLocalizer/Xml/XmlResourceProvider.cs
[5]:https://github.com/LazZiya/XLocalizer.DB/blob/master/XLocalizer.DB/EF/EFDbResourceProvider.cs