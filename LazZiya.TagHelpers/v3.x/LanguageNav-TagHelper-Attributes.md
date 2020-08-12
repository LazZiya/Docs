---
title: LanguageNav TagHelper Attributes
keywords: asp.net-core, taghelpers, language, dropdown, localization
description: Attributes of LanguageNav TagHelper.
author: Ziya Mollamahmut
date: 08-Aug-2020
versions: 1.x, 2.x, 3.x, 4.x, 5.x
---

# LanguageNav TagHelper Attributes

By [Ziya Mollamahmut](https://github.com/LazZiya)

> All language navigation taghelper attributes are optional.

| Html attribute | type | default value | description |
|:---|:---|:---|:---|
| `supported-cultures` | `string` |  | Manually specify a list of supported cultures. e.g. "en,tr,ar" |
| `language-label` | [`LanguageLabel`][1] | `LanguageLabel.EnglishName` | The displayed text for each language in the dropdown. Possible values: `Name`, `DisplayName`, `EnglishName`, `NativeName`, `TwoLetterISOLanguageName` |
| `redirect-to-url` | `string` | `{0}` | The url to redirect to on language change. |
| [`cookie-handler-url`][2] | `string` |  | The url to the handler that sets the value of culture cookie. |
| `render-mode` | [`RenderMode`][3] | `RenderMode.Bootstrap` | Render a bootstrap dropdown or a classic `<select>` dropdown. Possible values: `Bootstrap`, `Classic`. |
| `flags` | `bool` | `false` | Show/hide relevant country flags. Works with bootstrap mode only. |
| `flags-squared` | `bool` | `false` | Show flags in squared format. |
| <img width="350" /> | | | |


[1]:https://github.com/LazZiya/TagHelpers/blob/master/LazZiya.TagHelpers/LanguageNavModels.cs#L6
[2]:LanguageNav-TagHelper-Setup.md#set-culture-cookie
[3]:https://github.com/LazZiya/TagHelpers/blob/master/LazZiya.TagHelpers/LanguageNavModels.cs#L60