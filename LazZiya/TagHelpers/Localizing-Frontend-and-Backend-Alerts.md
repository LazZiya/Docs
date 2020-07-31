All front-end and back-end alerts can be localized by parsing `IStringLocalizer` instance to the alert tag:

````html
@inject IStringLocalizer _localizer

<alert localizer="_localizer"></alert>
````

Or if hyou are using [`LazZiya.ExpressLocalization`][1] you can pass instance of [`ISharedCultureLocalizer`][2] as well:

````html
@inject ISharedCultureLocalizer _localizer

<alert localizer="_localizer"></alert>
````

---
### Applies to version:
5.0

[1]:../../LazZiya/ExpressLocalization/index.md
[2]:https://github.com/LazZiya/ExpressLocalization/blob/master/LazZiya.ExpressLocalization/ISharedCultureLocalizer.cs