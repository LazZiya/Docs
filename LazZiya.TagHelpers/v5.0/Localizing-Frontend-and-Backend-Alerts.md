---
title: Localizing AlertTaghelper Contents in Asp.Net Core
keywords: asp.net-core, taghelpers, localizatin, alerts
description: Learn how to localize contents of AlertTagHelper from LazZiya.TagHelpers for Asp.Net Core.
author: Ziya Mollamahmut
date: 08-Aug-2020
versions: 5.x
---

# Localizing AlertTaghelper Contents in Asp.Net Core

By [Ziya Mollamahmut](https://github.com/LazZiya)

All front-end and back-end alerts can be localized by parsing `IStringLocalizer` instance to the alert tag:

````html
@inject IStringLocalizer _localizer

<alert localizer="_localizer"></alert>
````

Or if hyou are using [`LazZiya.ExpressLocalization`][1] you can pass instance of [`ISharedCultureLocalizer`][2] as well:

````html
@inject ISharedCultureLocalizer _localizer

<alert localizer="_localizer"></alert>
````

---
### Applies to version:
5.0

[1]:../../LazZiya.ExpressLocalization/v4.0/index.md
[2]:https://github.com/LazZiya/ExpressLocalization/blob/master/LazZiya.ExpressLocalization/ISharedCultureLocalizer.cs