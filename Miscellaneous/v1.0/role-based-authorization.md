<!-- meta tags details, will be assigned to meta tags inside header by js -->
<div id="meta-info">
<details><summary>meta info</summary>

> * Title: <i id="md-title">Asp.Net Core - Role Based Policy Authorization</i>
> * Keywords: <i id="md-keywords">asp.net,core,authentication,role,policy,login,time,custom login,identity</i>
> * Description: <i id="md-description">How to create a role based policy authorization for Asp.Net Core.</i>
> * Author: <i id="md-author">Ziya Mollamahmut</i>
> * Date: <i id="md-date">14-Apr-2021</i>
> * Image: <i id="md-image">https://github.com/LazZiya/Docs/raw/master/Miscellaneous/v1.0/images/ziya-logo.png</i>
> * Image-alt: <i id="md-image-alt">Miscellaneous Logo</i>
> * Version: <i id="md-version">v1.0</i>

</details>
</div>


# Role Based Policy Authentication
By [Ziya Mollamahmut](https://github.com/LazZiya)

#### What is it that causes a page to redirect to Login and another to not?

- If the page or controller is configured to allow anonymous it will not redirect to login

````csharp
[AllowAnonymous]
public class HomePage : PageModel
{
    //...
}
````
- If the page/folder or area is configured to allow authorized users only, either by using `[Authorize]` attribute or in `startup.cs` it will redirect the user to the login page if he/she is not logged in.
````csharp
[Authorize]
public ContactModel : PageModel
{
    // ...
}
````

Here is a sample configuration for authorization in startup, where we do create a role based policy named `RequireAdmins` for a role name `Admins`:
````csharp
services.AddRazorPages()
    .AddRazorPagesOptions(ops =>
    {
        ops.Conventions.AuthorizeAreaFolder("Panel", "/", "RequireAdmins");
        ops.Conventions.AuthorizeFolder("/", "RequireAdmins");
        ops.Conventions.AllowAnonymousToAreaPage("Identity", "/Account/AccessDenied");
    });

services.AddAuthorization(ops =>
{
    ops.AddPolicy("RequireAdmins", policy => policy.RequireRole("Admins"));
});
````