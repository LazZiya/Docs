### Json Settings

All settings of `PagingTagHelper` can be done via `appSettings.json`. This settings can be applied to all paging controls or specific ones. This provides a flexibility in controlling the paging controls and offers a clean html on the other hand.

Sample Json settings for `PagingTagHelper`
````json
{
    "lazziya": {
        "pagingTagHelper": {
            "default": {
                "show-first-last": true,
                "show-prev-next": true,
                "show-page-size-nav": true,
                "show-total-pages": true,
                "show-total-records": true,
            }
        }
    }
}
````
### Default Setting Group

If the name of the settings group is `default` it will be applied to all paging controls unless a different settings name is specified in the paging control.

For example, below paging controls both will use the `default` settings from json:
````cs
<paging page-no="Model.PageNo"
        page-size="Model.PageSize"
        total-records="Model.TotalRecords">
</paging>

<paging page-no="Model.PageNo"
        page-size="Model.PageSize"
        total-records="Model.TotalRecords"
        json-settings="default">
</paging>
````

### Multiple Setting Groups

It is possible to specify different settings groups for different paging controls. For example below we defined two settings `basic` and `custom`:
````json
{
    "lazziya": {
        "pagingTagHelper": {
            "basic": {
                "show-first-last": true,
                "max-displayed-pages": 7,
                "class-active-page": "disabled"
            },
            "custom": {
                "show-first-last": true,
                "show-prev-next": true,
                "show-gap": true,
                "max-displayed-pages": 2,
                "text-first": "go first",
                "text-last": "go last",
                "text-previous": "one step back",
                "text-next": "one step forward",
                "class-paging-control": "pagination pagination-lg"
            }
        }
    }
}
````

And the relevant paging controls:
````html
<!-- basic settings -->
<paging page-no="Model.PageNo"
        page-size="Model.PageSize"
        total-records="Model.TotalRecords"  
        settings-json="basic">
</paging>

<!-- custom settings -->
<paging page-no="Model.PageNo"
        page-size="Model.PageSize"
        total-records="Model.TotalRecords"  
        settings-json="custom">
</paging>
````

### All Default Settings

> Notice: Paging control is configured to use the default settings even if it not defined in `appSettings.json`, so it is not necessary to use json for the default settings.

All json settings with default values in one shot:
````json
{
    "lazziya": {
        "pagingTagHelper": {
            "default": {
                "number-system": "default",
                "max-displayed-pages": 10,
                "page-size-dropdown-items": "10-25-50",
                "query-string-key-page-no": "p",
                "query-string-key-page-size": "s",
                "show-gap": true,
                "show-first-last": true,
                "show-prev-next": true,
                "show-page-size-nav": true,
                "show-total-pages": true,
                "show-total-records": true,
                "text-page-size": "",
                "text-first": "«",
                "text-last": "»",
                "text-previous": "‹",
                "text-next": "›",
                "text-total-pages": "pages",
                "text-total-records": "records",
                "sr-text-first": "First",
                "sr-text-last": "Last",
                "sr-text-previous": "Previous",
                "sr-text-next": "Next",
                "class": "row",
                "class-info-div": "col-1",
                "class-page-size-div": "col-1",
                "class-paging-control-div": "col-10",
                "class-paging-control": "pagination",
                "class-active-page": "active",
                "class-disabled-jumping-button": "disabled",
                "class-total-pages": "badge badge-light",
                "class-total-records": "badge badge-dark"
            }
        }
    }
}
````