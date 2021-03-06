<!-- meta tags details, will be assigned to meta tags inside header by js -->
<div id="meta-info">
<details><summary>meta info</summary>

> * Title: <i id="md-title">Culture Fallback Behavior</i>
> * Keywords: <i id="md-keywords">localization, asp.net-core, express-localization, culture, fallback, behavior</i>
> * Description: <i id="md-description">Learn how ExpressLocalization chooses the culture in a localized Asp.Net Core web app.</i>
> * Author: <i id="md-author">Ziya Mollamahmut</i>
> * Date: <i id="md-date">27-Sep-2019</i>
> * Image: <i id="md-image">https://github.com/LazZiya/Docs/raw/master/LazZiya.ExpressLocalization/v3.0/images/lazziya-express-localization-logo.png</i>
> * Image-alt: <i id="md-image-alt">LazZiya.ExpressLocalization Logo</i>
> * Version: <i id="md-version">v3.0</i>

</details>
</div>

# Culture Fallback Behavior

By [Ziya Mollamahmut](https://github.com/LazZiya)

Asp.Net Core uses [localization culture providers][5] to detect the request culture and respond accordingly. The culture checking process goes one by one through all registered providers, whenever a request culture is detected the check process stops and the localization process starts accordingly.

If the request culture is not found in the first provider, next provider will be checked. Finally if no culture is detected the default culture will be used.

_ExpressLocalization_ is using the below order for request culture providers:
1) [RouteSegmentCultureProvider][6]
2) [QueryStringRequestCultureProvider][7]
3) [CookieRequestCultureProvider][3]
4) [AcceptedLanguageHeaderRequestCultureProvider][4]
5) Use default request culture from startup settings

In order to restrict culture fallback to route culture provider only use below implementation in startup:
````csharp
services.AddRazorPages()
        .AddExpressLocalization<LocalizationResource>(ops =>
        {
            // Use only route segment culture provider
             ops.UseAllCultureProviders = false;
               
            // the rest of the code...
        });
````
_reference to issue [#13][8]_

[6]: https://github.com/LazZiya/ExpressLocalization/blob/master/LazZiya.ExpressLocalization/RouteSegmentCultureProvider.cs
[7]: https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.localization.querystringrequestcultureprovider
[3]: https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.localization.cookierequestcultureprovider
[4]: https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.localization.acceptlanguageheaderrequestcultureprovider
[5]: https://docs.microsoft.com/en-us/aspnet/core/fundamentals/localization-extensibility?view=aspnetcore-3.1#localization-culture-providers
[8]: https://github.com/LazZiya/ExpressLocalization/issues/13
