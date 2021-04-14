<!-- meta tags details, will be assigned to meta tags inside header by js -->
<div id="meta-info">
<details><summary>meta info</summary>

> * Title: <i id="md-title">Culture Fallback Behavior</i>
> * Keywords: <i id="md-keywords">localization, asp.net-core, xlocalizer, culture,fallback,behavior</i>
> * Description: <i id="md-description">Learn how the app chooses the culture in a localized Asp.Net Core web app.</i>
> * Author: <i id="md-author">Ziya Mollamahmut</i>
> * Date: <i id="md-date">14-Apr-2021</i>
> * Image: <i id="md-image">https://github.com/LazZiya/Docs/raw/master/XLocalizer/v1.0/images/xlocalizer-logo.png</i>
> * Image-alt: <i id="md-image-alt">XLocalizer Logo</i>
> * Version: <i id="md-version">v1.0</i>

</details>
</div>

# Culture Fallback Behavior

By [Ziya Mollamahmut](https://github.com/LazZiya)

Asp.Net Core uses [localization culture providers][5] to detect the request culture and respond accordingly. The culture checking process goes one by one through all registered providers, whenever a request culture is detected the check process stops and the localization process starts accordingly.

By default `XLocalizer` will use below `RequestCultureProviders` in order to detect the request culture (_It may change depending on the startup configuration_):

1) [RouteSegmentRequestCultureProvider][6]
2) [QueryStringRequestCultureProvider][7]
3) [CookieRequestCultureProvider][3]
4) [AcceptedLanguageHeaderRequestCultureProvider][4]

Depending on the supported cultures list provided in startup, it will try to match cultures in the list by the request culture in the providers till it find the first match and respond accordingly.

So when a request is made, the localization middleware will start looking for the `culture` value in the defined providers.

- First try with `RouteSegmentRequestCultureProvider` to look for `{culture}` value in the route `https://localhost:1234/xx`.
- If there is no `{culture}` provided in the route, the next provider will be checked `QueryStringRequestCultureProvider` to find `culture` value in the query string `https://localhost:1234/?culture=xx`, 
- Again if there is no culture value in the query string, it will go ahead to the next provider `CookieRequestCultreProvider` (below is a sample culture cookie for `TR` culture.)

[![Asp.Net Core Culture Cookie][1]][1]

- If there is no culture param in the cookie it will check the last culture provider `AcceptedLanguageHeaderRequestCultureProvider` which provides a list of accepted cultures. (_Below you can see a screenshot of chrome supported cultures list, you may change the order of your browsers cultures and see how it affect the request culture._)_

[![Chrome Browser Accepted Languages][2]][2]

Finally, if it can't detect the request culture in any of the above providers then it will use the `DefaultRequestCulture` that has been defined in `RequestLocalizationOptions` in startup.

````csharp
services.Configure<RequestLocalizationOption>(ops =>
{
    // ...
    ops.DefaultRequestCulture = new RequestCulture("en");
});
````


[1]: https://github.com/LazZiya/Docs/raw/master/LazZiya.XLocalizer/v1.0/images/culture-cookie-localization.jpg
[2]: https://github.com/LazZiya/Docs/raw/master/LazZiya.XLocalizer/v1.0/images/culture-browser-accepted-headers.jpg
[6]: https://github.com/LazZiya/XLocalizer/blob/master/XLocalizer/Routing/RouteSegmentRequestCultureProvider.cs
[7]: https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.localization.querystringrequestcultureprovider
[3]: https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.localization.cookierequestcultureprovider
[4]: https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.localization.acceptlanguageheaderrequestcultureprovider
[5]: https://docs.microsoft.com/en-us/aspnet/core/fundamentals/localization-extensibility?view=aspnetcore-3.1#localization-culture-providers
