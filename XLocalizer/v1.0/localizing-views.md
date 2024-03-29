<!-- meta tags details, will be assigned to meta tags inside header by js -->
<div id="meta-info">
<details><summary>meta info</summary>

> * Title: <i id="md-title">Localizing Views</i>
> * Keywords: <i id="md-keywords">localization, asp.net-core, views, razor, pages, mvc, taghelpers</i>
> * Description: <i id="md-description">Learn how to localize views with XLocalizer.TagHelpers in Asp.Net Core web app.</i>
> * Author: <i id="md-author">Ziya Mollamahmut</i>
> * Date: <i id="md-date">08-Aug-2020</i>
> * Image: <i id="md-image">https://github.com/LazZiya/Docs/raw/master/XLocalizer/v1.0/images/xlocalizer-logo.png</i>
> * Image-alt: <i id="md-image-alt">XLocalizer Logo</i>
> * Version: <i id="md-version">v1.0</i>

</details>
</div>

# Localizing Views

By [Ziya Mollamahmut](https://github.com/LazZiya)

XLocalizer has a handy extension pack; [XLocalizer.TagHelpers][3] for localizing views using a simple html tag.

### Table of contents
- [Install](#install)
- [Setup](#setup)
- [Localize texts](#localize-texts)
- [Localize HTML](#localize-html)
- [Localize Select Items](#localize-select-items)
- [Localize attributes](#localize-attributes)
- [Specify culture](#specify-culture)
- [Provide arguments for localized contents](#provide-arguments-for-localized-contents)
- [Specify resource source](#specify-resource-source)
- [Traditional localization for views](#traditional-localization-for-views)
- [Demo][1]
- [Next: Localizing data annotations][2]

#### Install
Install from nuget
````
PM > Install-Package XLocalizer.TagHelpers
````

#### Setup
Localize views using `LocalizeTagHelper`, first it must be added to `_ViewImports.cshtml_
````
@addTagHelper *, XLocalizer.TagHelpers
````

#### Localize texts
Localize texts/html contents using `localize-content` attribute with any html tag
````html
<h1 localize-content>Sample header</h1>

<p localize-content>
    sample content...
</p>
````

#### Localize Html
Use `<localize>` html tag or to localize all its contents
````html
<localize>
    <h1>Sample title</h1>
    <p>sample contents...</p>
<localize>
````

#### Localize Select Items
Use `<localize-select>` html tag to localize select items texts.
````html
<localize-select asp-items="Model.MyItems"></localize-select>
````

> Requires `XLocalizer.TagHelpers v1.1.0` or later.

#### Localize attributes
Localize attributes like `title` inside `<img` tag using `localize-att-*`
````html
<img src="/images/picture.jpg" localize-att-title="Picture title"/>
````

#### Provide arguments for localized contents
Localize a string that contains arguments by providing the arguments using `localize-args`
````html
@{
    var args = new object[] { "http://demo.ziyad.info/en/localize", 8, "Asp.Net Core" }
}

<p localize-args="args">
    Visit <a href="{0}">demos website</a> to see a collection of {1} demos about "{2}".
</p>
````
> Localized output sample: Visit [demos website][1] to see a collection of 8 demos about "Asp.Net Core".

#### Specify culture
Force specific culture regardless the request culture
````html
<p localize-culture="tr">
    This content will always be localized with TR culture
</p>
````

#### Specify resource source
Specify localization resource type using `localize-source`
````html
<p localize-source="typeof(MyResourceType)">
    This content will be localized from a specific shared resource.
</p>
````

See [demo page][1].

## Traditional localization for views
Default localization interfaces can be used to localize view contents:

````html
@inject IStringLocalizer _localizer

<h1>@_localizer["Welcome"]</h1>
````

#
### Next: [Localizing DataAnnotations][2]
#


[1]:http://demo.ziyad.info/en/localize
[2]:localizing-validation-attributes-errors.md
[3]:https://github.com/LazZiya/XLocalizer.TagHelpers