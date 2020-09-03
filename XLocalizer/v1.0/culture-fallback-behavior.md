<!-- meta tags details, will be assigned to meta tags inside header by js -->
<div id="meta-info">
<details><summary>meta info</summary>

> * Title: <i id="md-title">Culture Fallback Behavior</i>
> * Keywords: <i id="md-keywords">localization, asp.net-core, xlocalizer, culture,fallback,behavior</i>
> * Description: <i id="md-description">Learn how the app chooses the culture in a localized Asp.Net Core web app.</i>
> * Author: <i id="md-author">Ziya Mollamahmut</i>
> * Date: <i id="md-date">08-Aug-2020</i>
> * Image: <i id="md-image">https://github.com/LazZiya/Docs/raw/master/XLocalizer/v1.0/images/xlocalizer-logo.png</i>
> * Image-alt: <i id="md-image-alt">XLocalizer Logo</i>
> * Version: <i id="md-version">v1.0</i>

</details>
</div>

# Culture Fallback Behavior

By [Ziya Mollamahmut](https://github.com/LazZiya)

Asp.Net Core uses [localization culture providers][5] to detect the request culture and respond accordingly. The culture checking process goes one by one through all registered providers, whenever a request culture is detected the check process stops and the localization process starts accordingly.

If the request culture is not found in the first provider, next provider will be checked. Finally if no culture is detected the default culture will be used.

`XLocalizer` is using the order defined in `startup` to check for the request culture, for example given the below setup:
````cs
services.Configure<RequestLocalizationOptions>(ops =>
{
    ops.SupportedCultures = cultures;
    ops.SupportedUICultures = cultures;
    ops.DefaultRequestCulture = new Microsoft.AspNetCore.Localization.RequestCulture("en");
    ops.RequestCultureProviders.Insert(0, new RouteSegmentRequestCultureProvider(cultures));
});
````

`XLocalizer` will use below order:
1) [RouteSegmentRequestCultureProvider][6]
2) [QueryStringRequestCultureProvider][7]
3) [CookieRequestCultureProvider][3]
4) [AcceptedLanguageHeaderRequestCultureProvider][4]


[6]: https://github.com/LazZiya/XLocalizer/blob/master/XLocalizer/Routing/RouteSegmentRequestCultureProvider.cs
[7]: https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.localization.querystringrequestcultureprovider
[3]: https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.localization.cookierequestcultureprovider
[4]: https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.localization.acceptlanguageheaderrequestcultureprovider
[5]: https://docs.microsoft.com/en-us/aspnet/core/fundamentals/localization-extensibility?view=aspnetcore-3.1#localization-culture-providers
