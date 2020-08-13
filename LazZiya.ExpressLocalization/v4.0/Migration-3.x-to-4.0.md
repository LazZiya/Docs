---
title: Migrating from 3.x to 4.x
keywords: localization, asp.net-core, migrating
description: Migrate from ExpressLocalization 3.x to 4.x.
author: Ziya Mollamahmut
date: 08-Aug-2020
versions: 1.0
---

# Migrating from 3.x to 4.x

By [Ziya Mollamahmut](https://github.com/LazZiya)

Use this manual to upgrade from `LazZiya.ExpressLocalization v3.x` to `v4.0`.


### LocalizeTagHelper
Open __ViewImports.cshtml_ remove old reference and add new reference to localize tag helper as below:
````
@* remove this line *@
@addTagHelper *, LazZiya.TagHelpers.Localization

@* add new taghelpers *@
@addTagHelper *, LazZiya.ExpressLocalizaion
````

### SharedCultureLocalizer
If you where using `SharedCultureLocalizer` to localize backend messages or views, just replace it with `ISharedCultureLocalizer`.

````csharp
// Replace all SharedCultureLocalizer instances 
// with ISharedCultureLocalizer
public class IndexModel : PageModel
{
    // remove this line
    // private readonly SharedCultureLocalizer _loc;

    // add IShared... instead
    private readonly ISharedCultureLocalizer _loc;

    public IndexModel(ISharedCultureLocalizer loc)
    {
        _loc = loc;
    }
}
````

### LocalizationValdiationScripts TagHelper Component
Previously the taghelper component for localization valdiation scripts taghlper;

 ````html
<localization-validation-scripts></localization-validation-scripts>
````
 where automtically registered with `ExpressLocalization`. Starting from v4.0 it will require manually registration in startup:

````csharp
services.AddTransient<ITagHelperComponent, LocalizationValidationScriptsTagHelperComponent>();
````
Read more about [Validating localized input][3]

### Validation Attributes
Previously all valdiation attributes where requiring an error message as below:
````csharp
[Required(ErrorMessage = "The field {0} is required"]

// or

[Required(ErrorMessage = DataAnnotationsErrorMessages.RequiredAttribute_ValidationError)]
````

Starting from v4.0 a new express attributes can be used. Express attributes produces localized error message by default, no need to manually provide an error message inside the attribute tags.

````csharp
// remove the reference to the error messages namespace
using LazZiya.ExpressLocalization.Messages;

// add reference to express data annotations
using LazZiya.ExpressLocalization.DataAnnotations

// Use express validation attributes by adding Ex... prefix to the attribute name
[ExRequired]
````

See all [express valdiation attributes][1] and [default attributes][2] for more details.

[1]:DataAnnotations-Localization-Using-Express-Attributes.md
[2]:DataAnnotations-Localization-Using-Default-Attributes.md
[3]:Validating-Localized-Input.md