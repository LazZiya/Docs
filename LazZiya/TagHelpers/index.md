# LazZiya.TagHelpers

## What is it?
A collection of useful TagHelpers for any ASP.NET Core project.

## Installation :

Install via nuget package manager:
````
Install-Package LazZiya.TagHelpers
````

Then add to _ViewImports.cshtml:
````razor
@addTagHelper *, LazZiya.TagHelpers
````

## Contents
- Paging TagHelper
- Alert TagHelper
- LanguageNav TagHelper
- Localization Validation Scripts TagHelper

### [Paging TagHelper][1]
Create a pagination control _styled with bootstrap 4.x_ using simple html tag.

````html
<paging page-no="Model.PageNo" 
        page-size="Model.PageSize"
        total-records="Model.TotalRecords">
</paging>
````
[![PagingTagHelper default](https://github.com/LazZiya/Docs/raw/master/images/LazZiya.TagHelpers/paging-tag-helper-full.PNG)][1]

### [Alert TagHelper ][2]
Create bootstrap alerts using very simple html tag.

````html
<alert-success>
    My alert text ...
</alert>
````
[![AlertTagHelper - success](https://github.com/LazZiya/Docs/raw/master/images/LazZiya.TagHelpers/alert-taghelper-success.PNG)][2]

### [Language Navigation TagHelper][3]
Create a language dropdown navigation for websites. Supported cultures will be used to create the navigation items.

````html
<language-nav flags="true"></language-nav>
````
[![LanguageNavTagHelper with flags](https://github.com/LazZiya/Docs/raw/master/images/LazZiya.TagHelpers/languagenav-taghelper-with-flags.PNG)][3]

### [Localization Validation Scripts TagHelper][4]
Add all client side scripts that are required for validating localized inputs like decimal numbers, dates, ..etc.
````html
<localization-validation-scripts></localization-validation-scripts>
````
[![Localization number es](https://github.com/LazZiya/Docs/raw/master/images/LazZiya.TagHelpers/localization-validiation-scripts-number-es.PNG)][4]

## Live demos:
http://demo.ziyad.info/en/

[1]:../../LazZiya/TagHelpers/Paging-TagHelper-Basic-Setup.md
[2]:../../LazZiya/TagHelpers/Alerts-TagHelper-Front-end-Alerts.md
[3]:../../LazZiya/TagHelpers/LanguageNav-TagHelper-Setup.md
[4]:../../LazZiya/TagHelpers/LocalizationValidationScripts-TagHelper-Setup.md