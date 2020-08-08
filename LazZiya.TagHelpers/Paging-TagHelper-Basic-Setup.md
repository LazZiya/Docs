---
title: Paging TagHelper Basic Setup
keywords: asp.net-core, taghelpers, paging, control, pagination, attributes
description: Basic setup of PagingTagHelper for Asp.Net Core.
author: Ziya Mollamahmut
date: 08-Aug-2020
versions: 1.x, 2.x, 3.x, 4.x, 5.x
---

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

![PagingTagHelper - default](https://github.com/LazZiya/Docs/raw/master/images/LazZiya.TagHelpers/paging-tag-helper-full.PNG)

### Customized setup
PagingTagHelper can be customized using [`html`][1] or [`json`][2] attributes:
![PagingTagHelper - customization](https://github.com/LazZiya/Docs/raw/master/images/LazZiya.TagHelpers/paging-tag-helper-samples.PNG)

[1]:../LazZiya.TagHelpers/Paging-TagHelper-Attributes.md
[2]:../LazZiya.TagHelpers/Paging-TagHelper-Json-Settings.md
