<!-- meta tags details, will be assigned to meta tags inside header by js -->
<div id="meta-info">
<details><summary>meta info</summary>

> * Title: <i id="md-title">Using DB as Localization Source</i>
> * Keywords: <i id="md-keywords">localization, asp.net-core, db</i>
> * Description: <i id="md-description">Learn how to use database as source for localization with XLocalizer.DB in Asp.Net Core.</i>
> * Author: <i id="md-author">Ziya Mollamahmut</i>
> * Date: <i id="md-date">23-Jul-2022</i>
> * Image: <i id="md-image">https://github.com/LazZiya/Docs/raw/master/XLocalizer/v1.0/images/xlocalizer-logo.png</i>
> * Image-alt: <i id="md-image-alt">XLocalizer Logo</i>
> * Version: <i id="md-version">v1.0</i>

</details>
</div>

# MVC/Razor Pages and Using DB as Localization Source

By [Ziya Mollamahmut](https://github.com/LazZiya)

This pacakge adds database support for `XLocalizer`.

### Table of contents
- [Install](#install)
- [Startup settings](#startup-settings)
- [User secrets](#user-secrets)
- [Caching](#caching)
- [Localization stores setup](#localization-stores-setup)
- [ApplicationDbContext Lifetime](#applicationdbcontext-lifetime)
- [XLocalizer DB UI](#xlocalizer-db-ui)
- [Full startup code for DB setup](#full-startup-code-for-db-setup)
- [Sample project](#sample-project)
- [Next: Localizing Views][4]
- ##### [Recommended to read: Fixing concurrency issue][7]

#### Install
Install nuget package:
````
PM > Install-Package XLocalizer
PM > Install-Package XLocalizer.DB
PM > Install-Package XLocalizer.Translate.MymemoryTranslate

// Optional:
PM > Install-Package XLocalizer.DB.UI
````

> Notice: `XLocalizer.DB.UI` provides an interface to manage DB localization resources and cultures

#### Startup settings

- Configure request localization options and optionally add `RouteSegmentRequestCultureProvider` :
````csharp
// Add namespace for optional routing setup
using XLocalizer.Routing;

// Configure request localization options
services.Configure<RequestLocalizationOptions>(ops => 
{
    // Define supported cultures
    var cultures = new CultureInfo[] { new CultureInfo("en"), new CultureInfo("tr"), new CultureInfo("ar") };
    ops.SupportedCultures = cultures;
    ops.SupportedUICultures = cultures;
    ops.DefaultRequestCulture = new RequestCulture("en");

    // Optional: add custom provider to support localization based on {culture} route value
    ops.RequestCultureProviders.Insert(0, new RouteSegmentRequestCultureProvider(cultures));
});        
````

- Register a translation service to enable auto translation option:
````csharp
services.AddHttpClient<ITranslator, MyMemoryTranslateService>();
````

> You can provide translation support based on any custom provider type by implementing `ITranslator` interface.

- Add route based localization for razor pages:
````csharp
services.AddRazorPages()
        .AddRazorPagesOptions(ops => { ops.Conventions.Insert(0, new RouteTemplateModelConventionRazorPages()); });
````

Or if you are using MVC use;
````csharp
services.AddMvc()
        .AddMvcOptions(ops => { ops.Conventions.Insert(0, new RouteTemplateModelConventionMvc()); });
````

> See [MVC Routing][5] for more details.

- Add DB localization setup:
````csharp
using XLocalizer.DB;

// Register translation service
services.AddHttpClient<ITranslator, MyMemoryTranslateService>();

services.AddRazorPages()
        .AddXDbLocalizer<ApplicationDbContext, MyMemoryTranslate>(ops =>
        {
            ops.AutoAddKeys = true;
            ops.AutoTranslate = true;
        });
````


#### User secrets
MyMemory offers a free or paid subscriptions, and depending on your setup it may require an Api key to be provided, for more details see [MyMemoryTranslateService][6].

Read more about translation services in [Translation services][1].

##### Caching
`XLocalizer` has built-in caching enabled by default. Caching helps to speedup the retriving of localized resources. But, it is recommended to switch caching off during development to avoid caching values that are subject to change frequently.

````csharp
ops.UseExpressMemoryCache = false;
```` 

#### Localization stores setup
DB localization requires two stores in the database; one for the cultures, and one for the resources. The default models are already defined in `XLocalizer.DB.Models`, we only need to add them to our context:

Open `ApplicationDbContext.cs` file and add below setup:
````csharp
using XLocalizer.DB.Models;

public class ApplicationDbContext : IdentityDbContext
{
    public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options)
    : base(options)
    {
    }
        
    // Cultures table will hold the supported cultures entities
    public DbSet<XDbCulture> XDbCultures { get; set; }

    // All resources will be saved in this table
    public DbSet<XDbResource> XDbResources { get; set; }

    protected override void OnModelCreating(ModelBuilder builder)
    {
        builder.Entity<XDbResource>()
            .HasKey(r => r.ID);

        builder.Entity<XDbResource>()
            .HasIndex(r => new { r.CultureID, r.Key })
            .IsUnique();

        builder.Entity<XDbResource>()
            .HasOne(t => t.Culture)
            .WithMany(c => c.Translations as IEnumerable<XDbResource>)
            .OnDelete(DeleteBehavior.Cascade);
            
        builder.SeedCultures();
        builder.SeedResourceData();

        base.OnModelCreating(builder);
    }
}
````

> If you want to add more tables for resources similar to [`XDbResource`][3], just implement [`IXDbResource`][2] interface and add the relevant setup to `ApplicationDbContext`.

Just for starting with some data, create an extension method to seed initial data:
````csharp
public static class SeedXLocalizerValues
{
    public static void SeedCultures(this ModelBuilder modelBuilder)
    {
        // Seed initial data for localization stores
        modelBuilder.Entity<XDbCulture>().HasData(
                new XDbCulture { IsActive = true, IsDefault = true, ID = "en", EnglishName = "English" },
                new XDbCulture { IsActive = true, IsDefault = false, ID = "tr", EnglishName = "Turkish" },
                new XDbCulture { IsActive = true, IsDefault = false, ID = "ar", EnglishName = "Arabic" }
                );
    }

    public static void SeedResourceData(this ModelBuilder modelBuilder)
    {
        modelBuilder.Entity<XDbResource>().HasData(
                new XDbResource { ID = 1, Key = "Welcome", Value = "Hoşgeldin", CultureID = "tr", IsActive = true, Comment = "Created by XLocalizer" }
            );
    }
}
````

#### ApplicationDbContext LifeTime
Asp.Net Core expects localization services to be added as singleton, so we have to change the `ApplciationDbContext` lifetime to avoid scoped and singleton conflicts.
````csharp
services.AddDbContext<ApplicationDbContext>(options =>
                options.UseSqlServer(Configuration.GetConnectionString("DefaultConnection")), 
                ServiceLifetime.Transient, 
                ServiceLifetime.Transient);
````


Finally, create a migration and update the database:
````
PM > add-migration XLocalizerStores
PM > update-database
````

#### XLocalizer DB UI
This package provides a ready made user panel to manage XLocalizer DB resources. After installing the package simply use below links to access the management panel.

##### Bootstrap 4.x
```` HTML
<!-- /XLocalizer/Cultures/Index -->
<a asp-area="XLocalizer" asp-page="/Cultures/Index" localize-content>DB Cultures</a>

<a asp-area="XLocalizer" asp-page="/Resources/Index" localize-content>DB Resources</a>
````

##### Bootstrap 5.x
```` HTML
<!-- /XLocalizerBS5/Cultures/Index -->
<a asp-area="XLocalizerBS5" asp-page="/Cultures/Index" localize-content>DB Cultures</a>

<!-- /XLocalizerBS5/Resources/Index -->
<a asp-area="XLocalizerBS5" asp-page="/Resources/Index" localize-content>DB Resources</a>
````

The panel provides below editors for cultures and resources:

![XLocalizer DB UI - Cultures Editor](https://github.com/LazZiya/Docs/raw/master/XLocalizer/v1.0/images/xlocalizer-db-ui-cultures.png)

![XLocalizer DB UI - Resources Editor](https://github.com/LazZiya/Docs/raw/master/XLocalizer/v1.0/images/xlocalizer-db-ui-resources.png)



#### Full startup code for DB setup
````csharp
using Microsoft.AspNetCore.Builder;
using Microsoft.AspNetCore.Identity;
using Microsoft.AspNetCore.Hosting;
using Microsoft.EntityFrameworkCore;
using XmlLocalizationSample.Data;
using Microsoft.Extensions.Configuration;
using Microsoft.Extensions.DependencyInjection;
using Microsoft.Extensions.Hosting;
using XLocalizer.Translate;
using XLocalizer;
using XLocalizer.DB;
using System.Globalization;
using XLocalizer.Routing;
using XLocalizer.Translate.MyMemoryTranslate;
using DbLocalizationSample.LocalizationResources;

namespace DbLocalizationSample
{
    public class Startup
    {
        public Startup(IConfiguration configuration)
        {
            Configuration = configuration;
        }

        public IConfiguration Configuration { get; }

        // This method gets called by the runtime. Use this method to add services to the container.
        public void ConfigureServices(IServiceCollection services)
        {
            // Change DbContext lifetime to transient.
            // By default it is scoped, but this conflicts with singleton lifetime of localization services.
            services.AddDbContext<ApplicationDbContext>(options =>
                options.UseSqlServer(Configuration.GetConnectionString("DefaultConnection")), 
                ServiceLifetime.Transient, ServiceLifetime.Transient);

            services.AddDefaultIdentity<IdentityUser>(options => options.SignIn.RequireConfirmedAccount = true)
                .AddEntityFrameworkStores<ApplicationDbContext>();

            services.Configure<RequestLocalizationOptions>(ops =>
            {
                var cultures = new CultureInfo[] { new CultureInfo("en"), new CultureInfo("tr"), new CultureInfo("ar") };
                ops.SupportedCultures = cultures;
                ops.SupportedUICultures = cultures;
                ops.DefaultRequestCulture = new Microsoft.AspNetCore.Localization.RequestCulture("en");

                // Optional: add custom provider to support localization based on route value {culture}
                ops.RequestCultureProviders.Insert(0, new RouteSegmentRequestCultureProvider(cultures));
            });
            
            // Optional: To enable online translation register one or more translation services
            services.AddHttpClient<ITranslator, MyMemoryTranslateService>();

            services.AddRazorPages()
                // Optional: Add {culture} route template to all razor pages routes e.g. /en/Index
                .AddRazorPagesOptions(ops => { ops.Conventions.Insert(0, new RouteTemplateModelConventionRazorPages()); })

                // Add XLocalization with and specify a service for handling translation requests
                .AddXDbLocalizer<ApplicationDbContext, MyMemoryTranslateService>(ops =>
                {
                    // Resources folder path required in case of 
                    // exporting db resources to resx resource files.
                    ops.ResourcesPath = "LocalizationResources";
                    ops.AutoAddKeys = true;
                    ops.AutoTranslate = true;
                });
        }

        // This method gets called by the runtime. Use this method to configure the HTTP request pipeline.
        public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
        {
            if (env.IsDevelopment())
            {
                app.UseDeveloperExceptionPage();
                app.UseDatabaseErrorPage();
            }
            else
            {
                app.UseExceptionHandler("/Error");
                // The default HSTS value is 30 days. You may want to change this for production scenarios, see https://aka.ms/aspnetcore-hsts.
                app.UseHsts();
            }

            app.UseHttpsRedirection();
            app.UseStaticFiles();

            app.UseRouting();

            app.UseAuthentication();
            app.UseAuthorization();
            app.UseRequestLocalization();
            app.UseEndpoints(endpoints =>
            {
                endpoints.MapRazorPages();
            });
        }
    }
}

````

#### Sample project
[Download sample project from GitHub][5]

#
### Next: [Localizing views][4]
#


[1]:translate-services.md
[2]:https://github.com/LazZiya/XLocalizer/blob/master/XLocalizer.DB/Models/IXDbResource.cs
[3]:https://github.com/LazZiya/XLocalizer/blob/master/XLocalizer.DB/Models/XDbResource.cs
[4]:localizing-views.md
[5]:https://github.com/LazZiya/XLocalizer.Samples/tree/master/DbLocalizationSample
[6]:translate-services-mymemory.md
[7]:setup-db-factory-pattern.md