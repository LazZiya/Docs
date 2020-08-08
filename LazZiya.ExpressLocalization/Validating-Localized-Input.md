---
title: Validating Localized Input
keywords: localization, asp.net-core, mvc
description: Validating localized input with ExpressLocalization for Asp.Net Core.
author: Ziya Mollamahmut
date: 08-Aug-2020
versions: 1.x, 2.x, 3.x, 4.x
---

# Validating Localized Input

By [Ziya Mollamahmut](https://github.com/LazZiya)

Some input fields need to be localized (decimal numbers, dates, ...etc.). But without client side localizing libraries this could make problems with different cultures (e.g. decimal numbers 1.23 and 1,23).

To have client side validation full compatibility with all cultures see [`LocalizationValdiationScripts`][1] taghelper from [`LazZiya.TagHelpers`][2]

[1]:../LazZiya.TagHelpers/LocalizationValidationScripts-TagHelper-Setup.md
[2]:..//LazZiya.TagHelpers/index.md

