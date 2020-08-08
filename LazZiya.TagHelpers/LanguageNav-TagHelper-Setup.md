---
title: Add a Language Dropdown with LanguageNav TagHelper
keywords: asp.net-core, taghelpers, language, dropdown, localization
description: Add a language navigation dropdown to Asp.Net Core web apps easily with LanguageNav TagHelper.
author: Ziya Mollamahmut
date: 08-Aug-2020
versions: 1.x, 2.x, 3.x, 4.x, 5.x
---

# Add a Language DropDown with LanguageNav TagHelper

By [Ziya Mollamahmut](https://github.com/LazZiya)

Adds a language navigation that lists all supported cultures.

### Quick Navigation
- [Redirect to URL](#redirect-to-url)
- [Redirect to the same page](#redirect-to-the-same-page)
- [Show country flags](#show-country-flags)
- [Set culture cookie](#set-culture-cookie)

* Install package
````
PM > Install-Package LazZiya.TagHelpers
````

* Add to _VÝewImports.cshtml:
````html
@addTagHelper *, LazZiya.TagHelpers
````

Add the language navigation to the __layout.cshtml_ or any other page:
````html
<language-nav></language-nav>
````

![LanguageNav Default](https://github.com/LazZiya/WebXRObjects/raw/master/Shared/Images/LazZiya.TagHelpers/languagenav-taghelper-default.PNG)

Basically, this is enough to create a language dropdown that is able to switch the culture and set new culture value in the url. But to save the current culture value in a cookie as well, we need two additional steps. See [Culture cookie](#set-culture-cookie) for further details.

### Redirect to url
By default language tag helper will redirect to the home page on culture change. But we can specify different url to redirect to:
````html
<language-nav redirect-to-url="@(Url.Page("/Index", new { culture="{0}" }))">
</language-nav>
````

The `culture` value must be specified as a placeholder "{0}" in the dictionary of route values, and the tag helper will take care of replacing it with the relevant culture name.

### Redirect to the same page
To redirect to the same page one of below methods can help:
 - Get current page name (or controller/action) and pass them to the Url helper
````html
<language-nav redirect-to-url="@(Url.Page(ViewContext.RouteData.Values["Page"].ToString(), new { culture = "{0}" }))">
</language-nav>
````

 - Another way is to get all route data and replace only the culture value with a place holder then recreate the url:
````html
@{ 
    var routeData = ViewContext.RouteData.Values;
    routeData["culture"] = "{0}";
}
<language-nav redirect-to-url="@(Url.RouteUrl(routeData))"></language-nav>
````

### Show country flags
If you have country specific content and not culture specific, it is recommended to use cultures that are specific to that country. 

E.g. if we have our cultures like: "tr-tr", "ar-sy", and "en-us" we can use flags beside each culture name in the dropdown. But if our cultures are not country specific "en", "tr" and "ar" so flags will not shown.

````html
<!-- add reference to flag-icon-css -->
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/flag-icon-css/3.4.6/css/flag-icon.min.css" />

<!-- enable flags in language navigation -->
<language-nav flags="true"></language-nav>
````

![LanguageNav with Flags](https://github.com/LazZiya/Docs/raw/master/images/LazZiya.TagHelpers/languagenav-taghelper-with-flags.PNG)

> Flags are svg files that shown with css thanks to [flag-icon-css][3].

### Set culture cookie
1- Create the handler that will save the culture value to cookie. E.g. create it under `Index.cshtml.cs`:

````cs
// Add required namespaces
using Microsoft.AspNetCore.Localization;
using Microsoft.AspNetCore.Http;

/// <summary>
/// Set culture cookie value
/// </summary>
/// <param name="cltr">Culture name</param>
/// <param name="returnUrl">The url to return to after setting the cookie</param>
public IActionResult OnGetSetCultureCookie(string cltr, string returnUrl)
{
    Response.Cookies.Append(
        CookieRequestCultureProvider.DefaultCookieName,
        CookieRequestCultureProvider.MakeCookieValue(new RequestCulture(cltr)),
        new CookieOptions { Expires = DateTimeOffset.UtcNow.AddYears(1) }
    );

    return LocalRedirect(returnUrl);
}
````

2- Set the culture cookie handler url in the language-nav taghelper:
````html
<language-nav cookie-handler-url="@Url.Page("/Index", "SetCultureCookie", new { area="", cltr="{0}", returnUrl="{1}" })">
</language-nav>
````

The place holders "{0}" and "{1}" will be filled by the tag helper with reference to each listed culture.

See samples in [demo page][2]

[1]: .
[2]:http://demo.ziyad.info/en/LanguageNav
[3]:https://github.com/lipis/flag-icon-css