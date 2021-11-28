<!-- meta tags details, will be assigned to meta tags inside header by js -->
<div id="meta-info">
<details><summary>meta info</summary>

> * Title: <i id="md-title">Asp.Net Core - Use Multiple DbContexts</i>
> * Keywords: <i id="md-keywords">asp.net,core,dbcontext</i>
> * Description: <i id="md-description">How to use multiple dbcontexts in one Asp.Net Core app.</i>
> * Author: <i id="md-author">Ziya Mollamahmut</i>
> * Date: <i id="md-date">28-Nov-2021</i>
> * Image: <i id="md-image">https://github.com/LazZiya/Docs/raw/master/Miscellaneous/v1.0/images/ziya-logo.png</i>
> * Image-alt: <i id="md-image-alt">Miscellaneous Logo</i>
> * Version: <i id="md-version">v1.0</i>

</details>
</div>


# How to use multiple DbContext in one Asp.Net Core App
By [Ziya Mollamahmut](https://github.com/LazZiya)

1. Create DB contexts
````csharp
public class DBContext_A : DbContext
{
    public DBContext_A(DbContextOptions<DBContext_A> options) : base(options)
    {
    }
}

public class DBContext_B : DbContext
{
    public DBContext_B(DbContextOptions<DBContext_B> options) : base(options)
    {
    }
}

public class DBContext_C : DbContext
{
    public DBContext_C(DbContextOptions<DBContext_C> options) : base(options)
    {
    }
}
````

2. Define a connection string for each DBContext:
````json
{
  "ConnectionStrings": {
    "Connection_A": "Server=(localdb)\\mssqllocaldb;Database=DB_A;Trusted_Connection=True;...",
    "Connection_B": "Server=(localdb)\\mssqllocaldb;Database=DB_B;Trusted_Connection=True;...",
    "Connection_C": "Server=(localdb)\\mssqllocaldb;Database=DB_C;Trusted_Connection=True;...",
  }
}
````

3. Register in startup:
````csharp
services.AddDbContext<DBContext_A>(ops =>
{
    ops.UseSqlServer(Configuration.GetConnectionString($"Connection_A"));
});

services.AddDbContext<DBContext_B>(ops =>
{
    ops.UseSqlServer(Configuration.GetConnectionString($"Connection_B"));
});

services.AddDbContext<DBContext_C>(ops =>
{
    ops.UseSqlServer(Configuration.GetConnectionString($"Connection_C"));
});

````

4. Inject into controller:
````csharp
public FooController : Controller
{
    private readonly DBContext_A _context_A;
    private readonly DBContext_B _context_B;
    private readonly DBContext_C _context_C;

    public FooController(
            DBContext_A context_A, 
            DBContext_B context_B, 
            DBContext_C context_C)
    {
        _context_A = context_A;
        _context_B = context_B;
        _context_C = context_C;
    }
}
````

### Additional best-practice for Code First approach:
Create a class library for each context, so when you apply migrations each context will have its own migrations folder in its own project.

* Solution
  - MainProject
    - startup.cs
  - ClassLibrary_A
    - DbContext_A.cs
    - Migrations // folder
  - ClassLibrary_B
    - DbContext_B.cs
    - Migrations // folder
  - ClassLibrary_C
    - DbContext_C.cs
    - Migrations // folder

While applying migrations in a multi context solution;
- From solution explorer, Set the main project (with startup.cs) as "Startup project"
- Set the relevant ClassLibrary_A or B or C from the package manager console as "Default project"
- Add the target context to each cmd as below:
````
PM > add-migration Init -Context DBContext_A
PM > update-database -Context DBContext_A

PM > add-migration Init -Context DBContext_B
PM > update-database -Context DBContext_B

PM > add-migration Init -Context DBContext_C
PM > update-database -Context DBContext_C
````

Alternatively, you may use the full PM cmd as below:
````
PM > add-migration Init -Context DBContext_A -Project ClassLibrary_A -StartupProject MainProject
PM > update-database -Context DBContext_A -Project ClassLibrary_A -StartupProject MainProject

PM > add-migration Init -Context DBContext_B -Project ClassLibrary_B -StartupProject MainProject
PM > update-database -Context DBContext_B -Project ClassLibrary_B -StartupProject MainProject

PM > add-migration Init -Context DBContext_C -Project ClassLibrary_C -StartupProject MainProject
PM > update-database -Context DBContext_C -Project ClassLibrary_C -StartupProject MainProject
````
