<!-- meta tags details, will be assigned to meta tags inside header by js -->
<div id="meta-info">
<details><summary>meta info</summary>

> * Title: <i id="md-title">Paging TagHelper Basic Setup</i>
> * Keywords: <i id="md-keywords">asp.net-core, taghelpers, paging, control, pagination, attributes</i>
> * Description: <i id="md-description">Basic setup of PagingTagHelper for Asp.Net Core.</i>
> * Author: <i id="md-author">Ziya Mollamahmut</i>
> * Date: <i id="md-date">02-Oct-2019</i>
> * Image: <i id="md-image">https://github.com/LazZiya/Docs/raw/master/LazZiya.TagHelpers/v3.0/images/lazziya-tagheleprs-logo.png</i>
> * Image-alt: <i id="md-image-alt">LazZiya.TagHelpers Logo</i>
> * Version: <i id="md-version">v3.0</i>

</details>
</div>

# Paging TagHelper Basic Setup

By [Ziya Mollamahmut](https://github.com/LazZiya)

### Default setup
Paging taghelper requires below parameters to render the paging control:

````html
<paging page-no="Model.PageNo"
        page-size="Model.PageSize"
        total-records="Model.TotalRecords">
</paging>
````

Output:

![PagingTagHelper - default](https://github.com/LazZiya/Docs/raw/master/LazZiya.TagHelpers/v3.0/images/paging-tag-helper-full.PNG)

### Customized setup
PagingTagHelper can be customized using [`html`][1] or [`json`][2] attributes:
![PagingTagHelper - customization](https://github.com/LazZiya/Docs/raw/master/LazZiya.TagHelpers/v3.0/images/paging-tag-helper-samples.PNG)

[1]:Paging-TagHelper-Attributes.md
[2]:Paging-TagHelper-Json-Settings.md
