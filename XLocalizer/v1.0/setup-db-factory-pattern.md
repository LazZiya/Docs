<!-- meta tags details, will be assigned to meta tags inside header by js -->
<div id="meta-info">
<details><summary>meta info</summary>

> * Title: <i id="md-title">Using DB as Localization Source with IDbContextFactory pattern</i>
> * Keywords: <i id="md-keywords">localization, asp.net-core, db, IDbContextFactory</i>
> * Description: <i id="md-description">Learn how to use database as source for localization with XLocalizer.DB in Asp.Net Core using the IdbContextFactory patterns</i>
> * Author: <i id="md-author">Ziya Mollamahmut</i>
> * Date: <i id="md-date">26-Mar-2025</i>
> * Image: <i id="md-image">https://github.com/LazZiya/Docs/raw/master/XLocalizer/v1.0/images/xlocalizer-logo.png</i>
> * Image-alt: <i id="md-image-alt">XLocalizer Logo</i>
> * Version: <i id="md-version">v1.1</i>

</details>
</div>

## Fix for concurrency issue:
By default the `XLocalizer.DB` uses `DbContext` as a transient serivce, and this may cause concurrency issues in some cases. To fix this issue, you can use `IDbContextFactory` pattern to create a new instance of `DbContext` for each request.

### 1- Update nuget packages
- Update `XLocalizer` to [`1.1.0-preview-1`](https://www.nuget.org/packages/XLocalizer/1.1.0-preview-1)
- Update `XLocalizer.DB` to [`1.1.0-preivew-1`](https://www.nuget.org/packages/XLocalizer.DB/1.1.0-preview-1)
- Update `XLocalizer.DB.UI` to [`1.2.0-preview-1`](https://www.nuget.org/packages/XLocalizer.DB.UI/1.2.0-preview-1) (optional)

```
pm > NuGet\Install-Package XLocalizer -Version 1.1.0-preview-1
pm > NuGet\Install-Package XLocalizer.DB -Version 1.1.0-preview-1
pm > NuGet\Install-Package XLocalizer.DB.UI -Version 1.2.0-preview-1
```

### 2- Create custom `XLocalizerDbContext` with the relevant stores for localization:

```cs
public class XLocalizerDbContext : DbContext
{
    public XLocalizerDbContext(DbContextOptions<XLocalizerDbContext> options)
        : base(options)
    {
    }

    public DbSet<XDbCulture> XDbCultures { get; set; }
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
            .WithMany(t => t.Translations as IEnumerable<XDbResource>)
            .OnDelete(DeleteBehavior.Cascade);


        builder.SeedCultures();
        builder.SeedResourceData();


        base.OnModelCreating(builder);
    }
}
```

### 3- Register `XLocalizerDbContext` using factory pattern:
```cs
services.AddDbContextFactory<XLocalizerDbContext>(options => options.UseSqlServer(Configuration.GetConnectionString("XLocalizerDbConnection")));
```

### 4- Create the relevant database and  connection string under appsettings.json:
```json
{
  "ConnectionStrings": {
    "XLocalizerDbConnection": "Server=(localdb)\\mssqllocaldb;Database=XLocalizer-DB;Trusted_Connection=True;MultipleActiveResultSets=true"
  }
}
```

### 5- Add `XLocalizerDbFactory` to razor pages:
````cs
services.AddRazorPages()
    .AddRazorPagesOptions(ops => { ops.Conventions.Insert(0, new RouteTemplateModelConventionRazorPages()); })
    .AddXDbLocalizerFactory<XLocalizerDbContext, MyMemoryTranslateService>(ops =>
    {
        ops.AutoAddKeys = true;
        ops.AutoTranslate = true;
        ops.UseExpressMemoryCache = false;
    });
}
```` 

### 6- Add a migration and update the database:
````
pm > add-migration -context XLocalizerDbContext XLocalizerStores
pm > update-database -context XLocalizerDbContext
````
_Notice that you need to name the target context `-context XLocalizerDbContext` while adding migration and updating the database_

### See [sample project](https://github.com/LazZiya/XLocalizer.Samples/tree/master/DbLocalizationSample)