---
title: SharedCultureLocalizaer for ExpressLocalization
keywords: localization, asp.net-core, mvc
description: SharedCultureLocalizder in ExpressLocalization for Asp.Net Core.
author: Ziya Mollamahmut
date: 08-Aug-2020
versions: 1.x, 2.x, 3.x, 4.x
---

# SharedCultureLocalizaer for ExpressLocalization

By [Ziya Mollamahmut](https://github.com/LazZiya)

The other option to localize views is using the built-in [`ISharedCultureLocalizer`][1]

- Inject [`ISharedCultureLocalizer`][1] into the view:
````html
@using LazZiya.ExpressLocalization
@inject ISharedCultureLocalizer _loc
````
- call localization function to get localized strings in views:
````html
<h1 class="display-4">@_loc["Welcome"]</h1>
````

But when it comes to localize long strings with html tags this approach become unfriendly. That's why the recommended localization approach is using [`Localize TagHelper`][2].

[1]:https://github.com/LazZiya/ExpressLocalization/blob/master/LazZiya.ExpressLocalization/ISharedCultureLocalizer.cs
[2]:../LazZiya.ExpressLocalization/Localize-TagHelper.md

### Applies to ExpressLocalization versions:
 4.0