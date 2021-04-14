<!-- meta tags details, will be assigned to meta tags inside header by js -->
<div id="meta-info">
<details><summary>meta info</summary>

> * Title: <i id="md-title">Asp.Net Core - Configure Authentication Cookie</i>
> * Keywords: <i id="md-keywords">asp.net,core,authentication,cookie,login,time,custom login,identity</i>
> * Description: <i id="md-description">How to configure authentication cookie to define custom login path and extend session time.</i>
> * Author: <i id="md-author">Ziya Mollamahmut</i>
> * Date: <i id="md-date">14-Apr-2021</i>
> * Image: <i id="md-image">https://github.com/LazZiya/Docs/raw/master/Miscellaneous/v1.0/images/ziya-logo.png</i>
> * Image-alt: <i id="md-image-alt">Miscellaneous Logo</i>
> * Version: <i id="md-version">v1.0</i>

</details>
</div>


# Configuring Authentication Cookie
By [Ziya Mollamahmut](https://github.com/LazZiya)

#### where do I configure Account/Login path that I want to redirect to?

The configuration can be done in startup using custom authentication cookie:
````csharp
public class XCookieAuthEvents : CookieAuthenticationEvents
{
    public override Task RedirectToLogin(RedirectContext<CookieAuthenticationOptions> context)
    {
        context.RedirectUri = $"/Identity/Account/CustomLogin";
        return base.RedirectToLogin(context);
    }

    public override Task RedirectToLogout(RedirectContext<CookieAuthenticationOptions> context)
    {
        context.RedirectUri = $"/Identity/Account/CustomLogout";
        return base.RedirectToLogout(context);
    }

    public override Task RedirectToAccessDenied(RedirectContext<CookieAuthenticationOptions> context)
    {
        context.RedirectUri = $"/Identity/Account/CustomAccessDenied";
        return base.RedirectToAccessDenied(context);
    }

    public override Task RedirectToReturnUrl(RedirectContext<CookieAuthenticationOptions> context)
    {
        context.RedirectUri = $"/CustomReturnUrl";
        return base.RedirectToReturnUrl(context);
    }
}
````

Then register in startup:
````csharp
services.AddScoped<XCookieAuthEvents>();

// optional: customize cookie expiration time
services.ConfigureApplicationCookie(ops =>
{
    ops.EventsType = typeof(XCookieAuthEvents);
    ops.ExpireTimeSpan = TimeSpan.FromMinutes(30);
    ops.SlidingExpiration = true;
});
````