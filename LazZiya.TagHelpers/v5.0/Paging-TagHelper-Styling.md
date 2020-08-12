---
title: Paging TagHelper Styling
keywords: asp.net-core, taghelpers, paging, control, pagination, styling
description: Change the look of PagingTagHelper via bootstrap styling.
author: Ziya Mollamahmut
date: 10-Aug-2020
versions: 5.x
---

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

#### Applies to versions:
5.x

[0]:Paging-TagHelper-Attributes.md#styling-attributes
[1]:https://github.com/LazZiya/Docs/raw/master/images/LazZiya.TagHelpers/paging-tag-helper-default.PNG
[2]:https://github.com/LazZiya/Docs/raw/master/images/LazZiya.TagHelpers/paging-tag-helper-dark.PNG
[3]:https://github.com/LazZiya/Docs/raw/master/images/LazZiya.TagHelpers/paging-tag-helper-gray.PNG