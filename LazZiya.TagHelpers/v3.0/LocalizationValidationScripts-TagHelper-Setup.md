<!-- meta tags details, will be assigned to meta tags inside header by js -->
<div id="meta-info">
<details><summary>meta info</summary>

> * Title: <i id="md-title">Valdiating Localized Input in Asp.Net Core</i>
> * Keywords: <i id="md-keywords">asp.net-core, taghelpers, language, localizatin, valdiating, input</i>
> * Description: <i id="md-description">Valdiating localized input in Asp.Net Core like decimals.</i>
> * Author: <i id="md-author">Ziya Mollamahmut</i>
> * Date: <i id="md-date">02-Oct-2019</i>
> * Image: <i id="md-image">https://github.com/LazZiya/Docs/raw/master/LazZiya.TagHelpers/v3.0/images/lazziya-tagheleprs-logo.png</i>
> * Image-alt: <i id="md-image-alt">LazZiya.TagHelpers Logo</i>
> * Version: <i id="md-version">v3.0</i>

</details>
</div>

# Valdiating Localized Input in Asp.Net Core

By [Ziya Mollamahmut](https://github.com/LazZiya)

### Introduction
Some input fields need to be localized (decimal numbers, dates, ...etc.). But without client side localizing libraries this could make problems with different cultures (e.g. decimal numbers 1.23 and 1,23).

![ES number input validiation](https://github.com/LazZiya/Docs/raw/master/LazZiya.TagHelpers/v3.0/images/localization-validiation-scripts-number-es.PNG)

Validating localized input requires a couple of additional scripts _for each culture_ to be included under the form. For more details see [How to install client side validation scripts article manually][1].

If you had a look at that article you must noticed that there is a lot of work to do! Luckily I've developed another useful tag helper that simplified the issue to single html tag :)

### Setup
- Install `LazZiya.TagHelpers` from nuget:
````
PM > Install-Package LazZiya.TagHelpers
````

- Add to __ViewImports.cshtml_:
````html
@addTagHelper *, LazZiya.TagHelpers
````

- Register in startup _only for v4.0 and newer, earlier versions doesn't require this step_
````cs
@using LazZiya.TagHelpers

services.AddTransient<ITagHelperComponent, LocalizationValidationScriptsTagHelperComponent>();
````

- Insert the html tag inside `Scripts` section just after validation scripts partial:
````html
@section Scripts {
    <partial name="_ValidationScriptsPartial" />
    <localization-validation-scripts></localization-validation-scripts>
}
````

That's all we have to do to get fully localized client side input validation. 

The output of this tag helper is **culture aware** validation scripts, that's mean; depending on the current culture the relevant scripts will be loaded by the tag helper. 

----
### Sample output
Below code provided just for info. You don't have to write it manually, it will be produced automatically by using [`localization-validation-scripts`] tag helper.

````html
<!-- cldr scripts (needed for globalize) -->
<script src="/lib/cldr/dist/cldr.min.js"></script>
<script src="/lib/cldr/dist/cldr/event.min.js"></script>
<script src="/lib/cldr/dist/cldr/supplemental.min.js"></script>

<!-- globalize scripts -->
<script src="/lib/globalize/dist/globalize.min.js"></script>
<script src="/lib/globalize/dist/globalize/number.min.js"></script>
<script src="/lib/globalize/dist/globalize/date.min.js"></script>
<script src="/lib/globalize/dist/globalize/currency.min.js"></script>

<!-- jquery valdiation globalize -->
<script src="https://cdn.jsdelivr.net/gh/johnnyreilly/jquery-validation-globalize@1.0.0/jquery.validate.globalize.min.js"></script>

<script type="text/javascript">
    $.when(
        $.get("/lib/cldr-data/supplemental/likelySubtags.json"),
        $.get("/lib/cldr-data/main/{culture}/numbers.json"),
        $.get("/lib/cldr-data/main/{culture}/currencies.json"),
        $.get("/lib/cldr-data/supplemental/numberingSystems.json"),
        $.get("/lib/cldr-data/main/{culture}/ca-gregorian.json"),
        $.get("/lib/cldr-data/main/{culture}/timeZoneNames.json"),
        $.get("/lib/cldr-data/supplemental/timeData.json"),
        $.get("/lib/cldr-data/supplemental/weekData.json"),
    ).then(function () {
        // Normalize $.get results, we only need the JSON, not the request statuses.
        return [].slice.apply(arguments, [0]).map(function (result) {
            return result[0];
        });
    }).then(Globalize.load).then(function () {
        Globalize.locale("{culture}");
    });
</script>
````

[1]:http://www.ziyad.info/en/articles/35-How_to_install_client_side_validation_scripts