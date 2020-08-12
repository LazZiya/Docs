---
title: Setup ExpressLocalization for MVC
keywords: localization, asp.net-core, mvc
description: Learn how to setup ExpressLocalization for Asp.Net Core MVC.
author: Ziya Mollamahmut
date: 08-Aug-2020
versions: 1.x, 2.x, 3.x, 4.x
---

# Setup ExpressLocalization for MVC

By [Ziya Mollamahmut](https://github.com/LazZiya)

Configure _ExpressLocalization_ in `startup.cs`:
````csharp
using System.Globalization;
using LazZiya.ExpressLocalization;
using Microsoft.AspNetCore.Localization;

//setup express localization under ConfigureServices method:
public void ConfigureServices(IServiceCollection services)
{
    // Other configuration settings....
    
    var cultures = new CultureInfo[]
    {
        new CultureInfo("en"),
        new CultureInfo("tr"),
        new CultureInfo("ar")
    };

    services.AddControllersWithViews()
        .AddExpressLocalization<LocalizationResource>(
            ops =>
            {
                ops.ResourcesPath = "LocalizationResources";
                ops.RequestLocalizationOptions = o =>
                {
                    o.SupportedCultures = cultures;
                    o.SupportedUICultures = cultures;
                    o.DefaultRequestCulture = new RequestCulture("en");
                };
            });
}
````

Use `RequestLocalization` middleware :
````csharp
public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
{
    // Other codes...
    
    // Use localization middleware
    app.UseRequestLocalization();

    // Add {culture} to the route
    app.UseEndpoints(endpoints =>
    {
        endpoints.MapControllerRoute(
            name: "default",
            pattern: "{culture=en}/{controller=Home}/{action=Index}/{id?}");
    });
}
````