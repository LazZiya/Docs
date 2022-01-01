<!-- meta tags details, will be assigned to meta tags inside header by js -->
<div id="meta-info">
<details><summary>meta info</summary>

> * Title: <i id="md-title">MVC Routing Setup</i>
> * Keywords: <i id="md-keywords">localization, asp.net-core, xml, resource, files, routing, mvc</i>
> * Description: <i id="md-description">Localization setup of Asp.Net Mvc Core with XLocalizer.</i>
> * Author: <i id="md-author">Ziya Mollamahmut</i>
> * Date: <i id="md-date">01-Jan-2022</i>
> * Image: <i id="md-image">https://github.com/LazZiya/Docs/raw/master/XLocalizer/v1.0/images/xlocalizer-logo.png</i>
> * Image-alt: <i id="md-image-alt">XLocalizer Logo</i>
> * Version: <i id="md-version">v1.0</i>

</details>
</div>

# MVC/Razor Pages and XML Based Localization Setup

By [Ziya Mollamahmut](https://github.com/LazZiya)

There are multiple ways to configure routing for localization in MVC projects, and you may get routing errors if the routing setup is not configured correctly.

### Option 1 - Routing Setup Using Model Convention
 - Configure `MvcOptions` by inserting model convention in startup, this will add `{culture}` route segment automatically to all routes in the application.
````csharp
services.AddMvc()
    .AddMvcOptions(ops => ops.Conventions.Insert(0, new RouteTemplateModelConventionMvc()))
    .AddXLocalizer<...>(...);
````

 - Define a route for each action
 ````csharp
 public class HomeController : Controller
 {
     [Route("")]
     public IActionResult Index() { ... }

     [Route("privacy")]
     public IActionResult Privacy() { ... }

     [Route("error")]
     public IActionResult Error() { ... }
 }
 ````

 ### Option 2 - Routing Setup Using Route Pattern
 Just add `{culture=en}` to te route pattern:
 ````csharp
 app.MapControllerRoute(
    name: "default",
    pattern: "{culture=en}/{controller=Home}/{action=Index}/{id?}");
 ```` 
> Thank to [@Julian](http://disq.us/p/2lqb5yn) for his comment