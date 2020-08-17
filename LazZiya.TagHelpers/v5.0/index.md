<!-- meta tags details, will be assigned to meta tags inside header by js -->
<div id="meta-info">
<details><summary>meta info</summary>

> * Title: <i id="md-title">LazZiya.TagHelpers</i>
> * Keywords: <i id="md-keywords">asp.net-core, taghelpers, paging, alerts, language, dropdown, localization, valdiation, scripts</i>
> * Description: <i id="md-description">A collection of usefull tag helpers for every Asp.Net Core web app.</i>
> * Author: <i id="md-author">Ziya Mollamahmut</i>
> * Date: <i id="md-date">08-Aug-2020</i>
> * Image: <i id="md-image">https://github.com/LazZiya/Docs/raw/master/LazZiya.TagHelpers/v5.0/images/lazziya-tagheleprs-logo.png</i>
> * Image-alt: <i id="md-image-alt">LazZiya.TagHelpers Logo</i>
> * Version: <i id="md-version">v5.0</i>

</details>
</div>

# LazZiya.TagHelpers

By [Ziya Mollamahmut](https://github.com/LazZiya)

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
[![PagingTagHelper default](https://github.com/LazZiya/Docs/raw/master/LazZiya.TagHelpers/v5.0/images/paging-tag-helper-full.PNG)][1]

### [Alert TagHelper ][2]
Create bootstrap alerts using very simple html tag.

````html
<alert-success>
    My alert text ...
</alert>
````
[![AlertTagHelper - success](https://github.com/LazZiya/Docs/raw/master/LazZiya.TagHelpers/v5.0/images/alert-taghelper-success.PNG)][2]

### [Language Navigation TagHelper][3]
Create a language dropdown navigation for websites. Supported cultures will be used to create the navigation items.

````html
<language-nav flags="true"></language-nav>
````
[![LanguageNavTagHelper with flags](https://github.com/LazZiya/Docs/raw/master/LazZiya.TagHelpers/v5.0/images/languagenav-taghelper-with-flags.PNG)][3]

### [Localization Validation Scripts TagHelper][4]
Add all client side scripts that are required for validating localized inputs like decimal numbers, dates, ..etc.
````html
<localization-validation-scripts></localization-validation-scripts>
````
[![Localization number es](https://github.com/LazZiya/Docs/raw/master/LazZiya.TagHelpers/v5.0/images/localization-validiation-scripts-number-es.PNG)][4]

## Live demos:
http://demo.ziyad.info/en/

[1]:Paging-TagHelper-Basic-Setup.md
[2]:Alerts-TagHelper-Front-end-Alerts.md
[3]:LanguageNav-TagHelper-Setup.md
[4]:LocalizationValidationScripts-TagHelper-Setup.md
