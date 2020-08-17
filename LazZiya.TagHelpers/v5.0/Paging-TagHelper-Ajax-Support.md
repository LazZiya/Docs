<!-- meta tags details, will be assigned to meta tags inside header by js -->
<div id="meta-info">
<details><summary>meta info</summary>

> * Title: <i id="md-title">Paging Control with Ajax Support for Asp.Net Core</i>
> * Keywords: <i id="md-keywords">asp.net-core, taghelpers, paging, control, pagination, ajax</i>
> * Description: <i id="md-description">Easily create a paging control with ajax support for large amount of records with PagingTagHelper for Asp.Net Core.</i>
> * Author: <i id="md-author">Ziya Mollamahmut</i>
> * Date: <i id="md-date">08-Aug-2020</i>
> * Image: <i id="md-image">https://github.com/LazZiya/Docs/raw/master/LazZiya.TagHelpers/v5.0/images/lazziya-tagheleprs-logo.png</i>
> * Image-alt: <i id="md-image-alt">LazZiya.TagHelpers Logo</i>
> * Version: <i id="md-version">v5.0</i>

</details>
</div>

# Paging Control with Ajax Support for Asp.Net Core

By [Ziya Mollamahmut](https://github.com/LazZiya)

* Install package
````
PM > Install-Package LazZiya.TagHelpers
````

* Add to _VÝewImports.cshtml:
````html
@addTagHelper *, LazZiya.TagHelpers
````

## Quick navigation
- [Required attributes](#required-attributes)
- [Optional attributes](#optional-attributes)
- [Ajax Requirements](#requirements)
- [Basic sample](#basic-sample)

### Required attributes
| Html attribute name | Json attribute | Value type | Default value | Description |
|:---|:---|:---|:---|:---|
| `ajax` | - | `bool` | `false` | Enable/disable ajax support |
| `ajax-update` | - | `string` |   | The ID of the DOM element to update by using the response from the server. |
| `ajax-url` | - | `string` |   | The URL to make the request to. |
| | | | | [Goto top](#quick-navigation) |

### Optional attributes
| Html attribute name | Json attribute | Value type | Default value | Description |
|:---|:---|:---|:---|:---|
| `ajax-loading` | - | `string` | `#loading-spinner` | The id attribute of an HTML element that is displayed while the Ajax function is loading. `PagingTagHelper` will create one by default. |
| `ajax-loading-duration` | - | `int` | `0` | A value, in milliseconds, that controls the duration of the animation when showing or hiding the loading element. |
| `ajax-mode` | - | `string` | `replace` | The mode that specifies how to insert the response into the target DOM element. Valid values are `before`, `after` and `replace`. Currently only `replace` mode provides the best functionality. |
| `ajax-confirm` | - | `string` |   | The message to display in a confirmation window before a request is submitted. |
| `ajax-begin` | - | `string` |   | The name of the JavaScript function to call immediately before the page is updated. |
| `ajax-complete` | - | `string` |   | The JavaScript function to call when response data has been instantiated but before 
| `ajax-success` | - | `string` |   | The JavaScript function to call after the page is successfully updated. |
| `ajax-failure` | - | `string` |   | The JavaScript function to call if the page update fails. |
| <img width="450" /> | | | | [Goto top](#quick-navigation) |


### Ajax Requirements

In order to have a paging control with ajax support, we must provide:
- A partial view for the items including the paging control
- A handler to process ajax call
- A div with specified id in and reference to ajax scripts in the main page 

### Basic sample

Before we add ajax attributes to the paging control, we have to do some infrastructure setup to add ajax support to the page.

1- Create the handler that will process the ajax request in `Index.cshtml.cs`

````cs
public IndexModel : PageModel
{
    // Page number
    [BindPropery(SupportsGet = true)]
    public int P { get; set; } = 1;

    // Page size
    [BindPropery(SupportsGet = true)]
    public int S { get; set; } = 10;

    // Total records
    public int TotalRecords { get; set; } = 0;

    public ICollection<Item> Items { get; set; }

    private readonly AppContext _context;
    public IndexModel(AppContext context)
    {
        _context = context;
    }

    public void OnGet()
    {
        (TotalRecords, Items) = GetData();
    }

    public IActionResult OnGetItemsList()
    {
        (TotalRecords, Items) = GetData();

        return new PartialViewResult()
        {
            ViewName = "_itemsListPartial",
            ViewData = this.ViewData
        };
    }

    public (int total, int items) GetData()
    {
        total = _context.Set<Item>().AsNoTracking().Count();

        items = _context.Set<Item>().AsNoTracking()
                        .OrderBy(x => x.Name)
                        .Skip((P-1)*S)
                        .Take(S)
                        .ToList();

        return (total, items);
    }
}
````

2- Create a partial view to render the items list with the paging control. For example `_itemsList.cshtml`

````razor
<!-- _itemsListPartial.cshtml -->

@model IndexModel

<table class="table table-stripped>
    <thead>
        <tr>
            <th>ID</th>
            <th>Name</th>
        </tr>
    </thead>

    <tbody>
        @if(Model.TotalRecords == 0)
        {
            <td colspan="2">No records!</td>    
        }
        else
        {
            foreach(var item in Model.Items)
            {
                <td>@item.ID</td>
                <td>@item.Name</td>
            }
        }
    </tbody>

    <tfoot>
        <tr>
            <td colspan="2">
                <!-- paging control -->
                <paging page-no="Model.P"
                        page-size="Model.S"
                        total-records="Model.TotalRecords"
                        ajax="true"
                        ajax-update="#items"
                        ajax-url="?handler=ItemsList">
                </paging>
            </td>
        </tr>
    </tfoot>
</table>
````

3- Add the target div to be updated to the page e.g. `Index.cshtml`, and put the partial view inside it _required for the initial request_:

````html
<!-- Index.cshtml -->

<div id="items">
    <partial name="_itemsListPartial.cshtml" />
</div>
````

Then add ajax scripts

````html
@section Scripts
{
    <script src="https://cdn.jsdelivr.net/npm/jquery-ajax-unobtrusive@3.2.6/dist/jquery.unobtrusive-ajax.min.js"></script>
}
````

See [sample repository](https://github.com/LazZiya/PagingSampleProject) in GitHub.