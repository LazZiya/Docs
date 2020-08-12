---
title: SelectEnum TagHelper
keywords: asp.net-core, taghelpers, select, enum
description: Creates a select list dropdown from Enum, with ability to set selected value and localization support.
author: Ziya Mollamahmut
date: 08-Aug-2020
versions: 1.x, 2.x, 3.x, 4.x, 5.x
---

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