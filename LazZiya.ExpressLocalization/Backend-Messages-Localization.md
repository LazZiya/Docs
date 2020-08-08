---
title: Localization of Custom Backend Messages
keywords: localization, asp.net-core, express-localization, backend, error, custom
description: Localize custom backend error messages with ExpressLocalization in Asp.Net Core.
author: Ziya Mollamahmut
date: 08-Aug-2020
versions: 1.x, 2.x, 3.x, 4.x
---

# Localization of Custom Backend Messages

By [Ziya Mollamahmut](https://github.com/LazZiya)

Custom error messages can be localized by injecting [`ISharedCultureLocalizer`][1] to the controller or PageModel as below:

````csharp
using LazZiya.ExpressLocalization

public class IndexModel : PageModel
{
    private readonly ISharedCultureLocalizer _loc;

    public string CustomMessage { get; set; }

    public IndexModel(ISharedCultureLocalizer loc)
    {
        _loc = loc;
    }

    public void OnGet() 
    {
        CustomMessage = _loc["Localized custom backend message"];
    }
}
````


> Extra: If you want to have bootstrap styled messages (Success, Warning, Danger, etc.) I suggest you have a look at [AlertTagHelper][2] in [LazZiya.TagHelpers][3] nuget package.

[1]:https://github.com/LazZiya/ExpressLocalization/blob/master/LazZiya.ExpressLocalization/ISharedCultureLocalizer.cs
[2]:../LazZiya.TagHelpers/Alert-TagHelper-Overview.md
[3]:../LazZiya.TagHelpers/index.md