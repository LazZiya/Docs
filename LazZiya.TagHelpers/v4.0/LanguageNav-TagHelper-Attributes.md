<!-- meta tags details, will be assigned to meta tags inside header by js -->
<div id="meta-info">
<details><summary>meta info</summary>

> * Title: <i id="md-title">LanguageNav TagHelper Attributes</i>
> * Keywords: <i id="md-keywords">asp.net-core, taghelpers, language, dropdown, localization</i>
> * Description: <i id="md-description">Attributes of LanguageNav TagHelper.</i>
> * Author: <i id="md-author">Ziya Mollamahmut</i>
> * Date: <i id="md-date">27-Mar-2020</i>
> * Image: <i id="md-image">https://github.com/LazZiya/Docs/raw/master/LazZiya.TagHelpers/v4.0/images/lazziya-tagheleprs-logo.png</i>
> * Image-alt: <i id="md-image-alt">LazZiya.TagHelpers Logo</i>
> * Version: <i id="md-version">v4.0</i>

</details>
</div>

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