---
title: Validating Localized Input
keywords: localization, asp.net-core, validatin, locailzed, input, decimal
description: Learn how to valdiate locaized input like decimal numbers in Asp.Net Core web apps with XLocalizer.
author: Ziya Mollamahmut
date: 08-Aug-2020
versions: 1.0
---

# Validating Localized Input

By [Ziya Mollamahmut](https://github.com/LazZiya)

Some input fields need to be localized (decimal numbers, dates, ...etc.). But without client side localizing libraries this could make problems with different cultures (e.g. decimal numbers 1.23 and 1,23).

To have client side validation full compatibility with all cultures see [`LocalizationValdiationScripts`][1] taghelper from [`LazZiya.TagHelpers`][2]


[1]:../../LazZiya.TagHelpers/v5.0/LocalizationValidationScripts-TagHelper-Setup.md
[2]:https://github.com/LazZiya/TagHelpers