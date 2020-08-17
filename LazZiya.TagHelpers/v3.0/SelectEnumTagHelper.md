<!-- meta tags details, will be assigned to meta tags inside header by js -->
<div id="meta-info">
<details><summary>meta info</summary>

> * Title: <i id="md-title">SelectEnum TagHelper</i>
> * Keywords: <i id="md-keywords">asp.net-core, taghelpers, select, enum</i>
> * Description: <i id="md-description">Creates a select list dropdown from Enum, with ability to set selected value and localization support.</i>
> * Author: <i id="md-author">Ziya Mollamahmut</i>
> * Date: <i id="md-date">02-Oct-2019</i>
> * Image: <i id="md-image">https://github.com/LazZiya/Docs/raw/master/LazZiya.TagHelpers/v3.0/images/lazziya-tagheleprs-logo.png</i>
> * Image-alt: <i id="md-image-alt">LazZiya.TagHelpers Logo</i>
> * Version: <i id="md-version">v3.0</i>

</details>
</div>

# SelectEnum TagHelper

By [Ziya Mollamahmut](https://github.com/LazZiya)

# What is it?
Creates a select list dropdown from Enum, with ability to set selected value and localization support.

## Live demo : 
http://demo.ziyad.info/en/SelectEnum

## Sample usage:
If we have an enum for weekdays as below : 

`public enum WeekDays { MON, TUS, WED, THU, FRI, SAT, SUN }`

**create a select list dropdown :**

````razor
<select-enum 
    enum-type="typeof(WeekDays)" 
    name="weekDay">
</select-enum>
````

**create a select list dropdown with selected value:**

````razor
<select-enum 
    enum-type="typeof(WeekDays)" 
    selected-value="(int)WeekDays.Friday" 
    name="weekDay">
</select-enum>
````

**create a select list dropdown with selected value and localized display names:**
IViewLocalizer must be injected to the view in advance:

````razor
@using Microsoft.AspNetCore.Mvc.Localization`

@inject IViewLocalizer Localizer`

<select-enum
    enum-type="typeof(WeekDays)"
    selected-value="(int)WeekDays.Friday" 
    text-localizer-delegate="delegate(string s) { return Localizer[s].Value; }"
    name="weekDay">
</select-enum>
````


**DisplayAttribute** 
SelectEnumTagHelper can read Name value of DisplayAttribute and use it for localization or display.

Documentation : [http://ziyad.info/en/articles/28-Select_Enum_TagHelper](http://ziyad.info/en/articles/28-Select_Enum_TagHelper)
Live demo : http://demo.ziyad.info/en/SelectEnum