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

[1]:../../LazZiya/TagHelpers/Paging-TagHelper-Attributes.md
[2]:../../LazZiya/TagHelpers/Paging-TagHelper-Json-Settings.md