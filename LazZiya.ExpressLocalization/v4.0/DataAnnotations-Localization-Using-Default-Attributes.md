<!-- meta tags details, will be assigned to meta tags inside header by js -->
<div id="meta-info">
<details><summary>meta info</summary>

> * Title: <i id="md-title">Localizing Default Data Annotations</i>
> * Keywords: <i id="md-keywords">localization, asp.net-core, express-localization, data, annotations</i>
> * Description: <i id="md-description">Learn how use a localize default data annotations in Asp.Net Core.</i>
> * Author: <i id="md-author">Ziya Mollamahmut</i>
> * Date: <i id="md-date">08-Aug-2020</i>
> * Image: <i id="md-image">https://github.com/LazZiya/Docs/raw/master/LazZiya.ExpressLocalization/v4.0/images/lazziya-express-localization-logo.png</i>
> * Image-alt: <i id="md-image-alt">LazZiya.ExpressLocalization Logo</i>
> * Version: <i id="md-version">v4.0</i>

</details>
</div>

# Localizing Default Data Annotations

By [Ziya Mollamahmut](https://github.com/LazZiya)

DataAnnotations localization setup is already done during the express setup in `startup.cs` file for [razor pages][1] or [MVC][2].

All we have to do is just provide an error message to the relevant attribute or a `Name` value for `Display` attribute:

````csharp
[Required(ErrorMessage = "The {0} field is required.")]
[Display(Name = "Full name")]
public string Name { get; set; }
````

### Default Error Messages
For easy implementation, all default framework error messages of data annotations, model binding and identity errors are predefined under [`LazZiya.ExpressLocalization.Messages`][3] namespace.

So we can use the already defined messages as below:

````csharp
using LazZiya.ExpressLocalization.Messages

[Required(ErrorMessage = DataAnnotationsErrorMessages.RequiredAttribute_ValidationError)]
[Display(Name = "Full name")]
public string Name { get; set; }
````

See all [`DataAnnotationsErrorMessages`][4]

### Customizing Error Messages
You are still able to provide custom validation messages as below:
````csharp
[Required(ErrorMessage = "Ooops! The {0} field is necessary to continue...")]
[Display(Name = "Full name")]
public string Name { get; set; }
````

> Notice : depending on `ExpressLocalization` setup, the error messages must be defined in the relevant resource file for DataAnnotations. For more details see [Creating Resources][5].

[1]:Setup-for-Razor-Pages.md
[2]:Setup-for-mvc.md
[3]:https://github.com/LazZiya/ExpressLocalization/tree/master/LazZiya.ExpressLocalization/Messages
[4]:https://github.com/LazZiya/ExpressLocalization/blob/master/LazZiya.ExpressLocalization/Messages/DataAnnotationsErrorMessages.cs
[5]:Creating-Resources.md

### Applies to ExpressLocalization versions:
 4.0, 3.2, 3.1, 3.0, 2.0, 1.1, 1.0