<!-- meta tags details, will be assigned to meta tags inside header by js -->
<div id="meta-info">
<details><summary>meta info</summary>

> * Title: <i id="md-title">Create Paging Control Easily with PagingTagHelper</i>
> * Keywords: <i id="md-keywords">asp.net-core, taghelpers, paging, control, pagination</i>
> * Description: <i id="md-description">Easily create a paging control for large amount of records with PagingTagHelper for Asp.Net Core.</i>
> * Author: <i id="md-author">Ziya Mollamahmut</i>
> * Date: <i id="md-date">04-May-2022</i>
> * Image: <i id="md-image">https://github.com/LazZiya/Docs/raw/master/LazZiya.TagHelpers/v6.0/images/lazziya-tagheleprs-logo.png</i>
> * Image-alt: <i id="md-image-alt">LazZiya.TagHelpers Logo</i>
> * Version: <i id="md-version">v6.0</i>

</details>
</div>

# Easily Create Paging Control for Asp.Net Core

By [Ziya Mollamahmut](https://github.com/LazZiya)

* Install package
````
PM > Install-Package LazZiya.TagHelpers
````

* Add to _VÝewImports.cshtml:
````html
@addTagHelper *, LazZiya.TagHelpers
````

### Create a pagination control

Only few parameters are required to fire up the pagination control

````html
<paging total-records="Model.TotalRecords"
            page-no="Model.PageNo"
            query-string-value="@(Request.QueryString.Value)"
            show-prev-next="true">
</paging>
````
Query string value is necessary if there is multiple search filters in the url.

Full options of pagination control :
````html
    <paging total-records="Model.TotalRecords"
            page-no="Model.PageNo"
            page-size="Model.PageSize"
            show-prev-next="true"
            show-total-pages="true"
            show-total-records="true"
            show-page-size-nav="true"
            show-first-numbered-page="true"
            show-last-numbered-page="true"
            gap-size="2"
            max-displayed-pages="3"
            query-string-key-page-no="p"
            query-string-key-page-size="s"
            query-string-value="@@(Request.QueryString.Value)"
            page-size-nav-block-size="10"
            page-size-nav-max-items="3"
            page-size-nav-on-change="get"
            page-size-nav-form-method="this.form.submit();"
            class="row"
            class-paging-control-div="col"
            class-info-div="col"
            class-page-size-div="col"
            class-paging-control="pagination"
            class-active-page="disabled"
            class-disabled-jumping-button="disabled"
            class-total-pages="badge badge-secondary"
            class-total-records="badge badge-info"
            text-page-size="Items per page:"
            text-total-pages="pages"
            text-total-records="records"
            text-first="&laquo;"
            text-last="&raquo;"
            text-previous="&lsaquo;"
            text-next="&rsaquo;"
            sr-text-first="First"
            sr-text-last="Last"
            sr-text-previous="Previous"
            sr-text-next="Next">
    </paging>
````


### Json Friendly
Keep your html code clean by moving all optional settings to appSettings.json, and create different instances for different use cases:

appSettings.json:
````json
{
    "lazziya": {
        "pagingTagHelper": {
            "basic": {
            "show-first-last": true,
            "max-displayed-pages": 7,
            "class-active-aage": "disabled"
          },
          "custom": {
            "show-first-last": true,
            "show-prev-next": true,
            "max-displayed-pages": 2,
            "text-first": "go first",
            "text-last": "go last",
            "text-previous": "one step back",
            "text-next": "one step forward",
            "class-paging-control": "pagination pagination-lg"
          },
          "full": {
            "max-displayed-pages": 10,
            "gap-size": 3,
            "show-first-last": true,
            "show-prev-next": true,
            "show-page-size-nav": true,
            "show-total-pages": true,
            "show-total-records": true,
            "show-first-numbered-page": true,
            "show-last-numbered-page": true
          }
        }
    }
}
````
HTML Code:
````html
    <!-- custom settings -->
    <paging total-records="Model.TotalRecords" 
            page-no="Model.PageNo" 
            page-size="Model.PageSize" 
            settings-json="custom">
    </paging>

    <!-- basic settings -->
    <paging total-records="Model.TotalRecords" 
            page-no="Model.PageNo" 
            page-size="Model.PageSize" 
            settings-json="basic">
    </paging>

    <!-- full settings -->
    <paging total-records="Model.TotalRecords" 
            page-no="Model.PageNo" 
            page-size="Model.PageSize" 
            settings-json="full">
    </paging>
````
Documentation : http://www.ziyad.info/en/articles/21-Paging_TagHelper_for_ASP_NET_Core

Live demo : http://demo.ziyad.info/en/paging