<!-- meta tags details, will be assigned to meta tags inside header by js -->
<div id="meta-info">
<details><summary>meta info</summary>

> * Title: <i id="md-title">Paging TagHelper Styling</i>
> * Keywords: <i id="md-keywords">asp.net-core, taghelpers, paging, control, pagination, styling</i>
> * Description: <i id="md-description">Change the look of PagingTagHelper via bootstrap styling.</i>
> * Author: <i id="md-author">Ziya Mollamahmut</i>
> * Date: <i id="md-date">08-Aug-2020</i>
> * Image: <i id="md-image">https://github.com/LazZiya/Docs/raw/master/LazZiya.TagHelpers/v6.0/images/lazziya-tagheleprs-logo.png</i>
> * Image-alt: <i id="md-image-alt">LazZiya.TagHelpers Logo</i>
> * Version: <i id="md-version">v6.0</i>

</details>
</div>

# Paging TagHelper Styling

By [Ziya Mollamahmut](https://github.com/LazZiya)

Paging taghelper has class-* attributes to change the styling, so you can build a themed control (dark, light, etc.)

See all available styling attributes [here][0].

#### Default style

![PagingTagHelper Default Theme][1]

````html
<paging page-no="1"
        page-size="10"
        total-records="30">
</paging>
````

#### Dark style

![PagingTagHelper Dark Theme][2]

````html
<paging page-no="1"
        page-size="10"
        total-records="30"
        class-page-link="bg-dark text-warning border-secondary"
        class-disabled-jumping-button="bg-dark text-secondary border-secondary"
        class-active-page="bg-warning text-dark">
</paging>
````

#### Gray style

![PagingTagHelper Gray Theme][3]

````html
<paging page-no="1"
        page-size="10"
        total-records="30"
        class-page-link="bg-secondary text-light border-dark"
        class-disabled-jumping-button="bg-secondary text-dark border-dark"
        class-active-page="bg-light">
</paging>
````

---

[0]:Paging-TagHelper-Attributes.md#styling-attributes
[1]:https://github.com/LazZiya/Docs/raw/master/LazZiya.TagHelpers/v6.0/images/paging-tag-helper-default.PNG
[2]:https://github.com/LazZiya/Docs/raw/master/LazZiya.TagHelpers/v6.0/images/paging-tag-helper-dark.PNG
[3]:https://github.com/LazZiya/Docs/raw/master/LazZiya.TagHelpers/v6.0/images/paging-tag-helper-gray.PNG
