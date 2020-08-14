<!-- meta tags details, will be assigned to meta tags inside header by js -->
<div id="meta-info">
<details><summary>meta info</summary>

> * Title: <i id="md-title">Configure Cookie RedirectTo Paths</i>
> * Keywords: <i id="md-keywords">localization, asp.net-core, xlocalizer, cookie, redirectto, path</i>
> * Description: <i id="md-description">Configure localized cookie redirect to paths in Asp.Net Core web app.</i>
> * Author: <i id="md-author">Ziya Mollamahmut</i>
> * Date: <i id="md-date">08-Aug-2020</i>
> * Image: <i id="md-image">https://github.com/LazZiya/Docs/raw/vNext/XLocalizer/v1.0/images/xlocalizer-logo.png</i>
> * Image-alt: <i id="md-image-alt">XLocalizer Logo</i>
> * Version: <i id="md-version">v1.0</i>

</details>
</div>

# Configure Cookie RedirectTo Paths

By [Ziya Mollamahmut](https://github.com/LazZiya)

`XLocalizer` will automatically configure app cookie to add culture value to the redirect path when redirect events are invoked.

The default events and paths are: 
- OnRedirectToLogin : `{culture}/Identity/Account/Login/`
- OnRedirectToLogout : `{culture}/Identity/Account/Logout/`
- OnRedirectToAccessDenied : `{culture}/Identity/Account/AccessDenied/`

You can define custom paths for login, logout and access denied using _ExpressLocalization_ as below:

````cs
services.AddRazorPages()
    .AddXLocalizer<LocSource>(
        ops =>
        {
            ops.RedirectToLoginPath = "/CustomLoginPath/";
            ops.RedirectToLogoutPath = "/CustomLogoutPath/";
            ops.RedirectToAcceddDeniedPath = "/CustomAccessDeniedPath/";
        });
````

Or if you need to completely use custom cookie configurations using the identity extensions method, you need to set the value of `ConfigureRedirectPaths` to false as below:

````cs
services.AddRazorPages()
    .AddXLocalizer<LocSource>(
        ops =>
        {            
            // don't configure redirect to paths on redirect events
            ops.ConfigureRedirectPaths = false;
            
            // ...
        });
````

in this case you need to manually configure the app cookie to handle the culture value on redirect events as described in [issue #2][2]


[2]: https://github.com/LazZiya/ExpressLocalization/issues/6
