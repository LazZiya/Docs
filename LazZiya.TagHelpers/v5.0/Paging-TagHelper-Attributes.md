<!-- meta tags details, will be assigned to meta tags inside header by js -->
<div id="meta-info">
<details><summary>meta info</summary>

> * Title: <i id="md-title">Paging TagHelper Attributes</i>
> * Keywords: <i id="md-keywords">asp.net-core, taghelpers, paging, control, pagination, attributes</i>
> * Description: <i id="md-description">Attributes of PagingTagHelper for Asp.Net Core.</i>
> * Author: <i id="md-author">Ziya Mollamahmut</i>
> * Date: <i id="md-date">08-Aug-2020</i>
> * Image: <i id="md-image">https://github.com/LazZiya/Docs/raw/master/LazZiya.TagHelpers/v5.0/images/lazziya-tagheleprs-logo.png</i>
> * Image-alt: <i id="md-image-alt">LazZiya.TagHelpers Logo</i>
> * Version: <i id="md-version">v5.0</i>

</details>
</div>

# Paging TagHelper Attributes

By [Ziya Mollamahmut](https://github.com/LazZiya)

## Quick navigation
- [Required attributes](#required-attributes)
- [Optional attributes](#optional-attributes)
  - [General settings attributes](#general-settings-attributes)
  - [Query string attributes](#query-string-attributes)
  - [Display attributes](#display-attributes)
  - [Text attributes](#text-attributes)
  - [Texts for screen readers](#texts-for-screen-readers)
  - [Styling attributes](#styling-attributes)

## Required attributes

| Html attribute name | Json attribute | Value type | Default value | Description |
|:---|:---|:---|:---|:---|
| `page-no` | - | `int` | `1` | Current page number |
| `page-size` | - | `int` | `10` | How many items to display in one page |
| `total-records` | - | `int` | `0` | Total count of all records |
| | | | | [Goto top](#quick-navigation) |

## Optional attributes

#### General settings attributes

| Html attribute name | Json attribute | Value type | Default value | Description |
|:---|:---|:---|:---|:---|
| `max-displayed-pages` | yes | `int` | `10` | Total amount of displayed page numbers |
| `page-size-dropdown-items` | yes | `string` | `10-25-50` | Numbers to display in the dropdown for selecting page size |
| `settings-json` | - | `string` | `default` | Default name of json settings group name |
|<img width="430"/>|<img width="150"/>|<img width="150"/>|<img width="200"/>| [Goto top](#quick-navigation) |

#### Query string attributes
Attributes to set the query string key names for page number and page size parameters.

| Html attribute name | Json attribute | Value type | Default value | Description |
|:---|:---|:---|:---|:---|
| `query-string-key-page-no` | yes | `string` | `P` | Query string key name of page number |
| `query-string-key-page-size` | yes | `string` | `S` | Query string key name of page size |
|<img width="250"/>|<img width="50"/>|<img width="50"/>|<img width="50"/>| [Goto top](#quick-navigation) |

#### Display attributes
Attributes to show/hide specific controls of the paging taghelper.

| Html attribute name | Json attribute | Value type | Default value | Description |
|:---|:---|:---|:---|:---|
| `show-page-size-nav` | yes | `bool` | `true` | show/hide page size dropdown list |
| `show-first-last` | yes | `bool` | `true` | show/hide "goto first/last record" navigation buttons  |
| `show-prev-next` | yes | `bool` | `true` | show/hide "goto previous/next record" navigation buttons  |
| `show-total-pages` | yes | `bool` | `true` | show/hide total pages count badge |
| `show-total-records` | yes | `bool` | `true` | show/hide total records count badge |
| `show-gap` | yes | `bool` | `true` | Show a three dots after first page or before last page when there is a gap in pages at the beginning or end. e.g. 1 ... 12 13 14 [15] 16 17 18 ... 100 |
|<img width="350"/>|<img width="50"/>|<img width="50"/>|<img width="50"/>| [Goto top](#quick-navigation) |

#### Text attributes
Attributes to set the texts of the buttons and labels.

| Html attribute name | Json attribute | Value type | Default value | Description |
|:---|:---|:---|:---|:---|
| `text-page-size` | yes | `string` |  | The text to display on the page size label. It will display current page size when no text is provided |
| `text-first` | yes | `string` | `&laquo;` | Text for goto first record button |
| `text-last` | yes | `string` | `&raquo;` | Text for goto last record button |
| `text-previous` | yes | `string` | `&lsaquo;` | Text for goto previous record button |
| `text-next` | yes | `string` | `&rsaquo;` | Text for goto next record button |
| `text-total-pages` | yes | `string` | `pages` | Text for total pages badge e.g. 100 pages |
| `text-total-records` | yes | `string` | `records` | Text for total records badge e.g. 1000 records |
| [`number-format`][1] | yes | `string` | `default` | See [Number format][1] for more details. |
|<img width="300"/>|<img width="50"/>|<img width="50"/>|<img width="50"/>| [Goto top](#quick-navigation) |

#### Texts for screen readers
Attributes for screen readers.

| Html attribute name | Json attribute | Value type | Default value | Description |
|:---|:---|:---|:---|:---|
| `sr-text-first` | yes | `string` | `First` | Screen reader text for goto first record button |
| `sr-text-last` | yes | `string` | `Last` | Screen reader text for goto last record button |
| `sr-text-previous` | yes | `string` | `Previous` | Screen reader text for goto previous record button |
| `sr-text-next` | yes | `string` | `Next` | Screen reader text for goto next record button |
|<img width="200"/>|<img width="50"/>|<img width="50"/>|<img width="50"/>| [Goto top](#quick-navigation) |

#### Styling attributes
Attributes to set class names for the html parts of the paging controls.

| Html attribute name | Json attribute | Value type | Default value | Description |
|:---|:---|:---|:---|:---|
| `class` | yes | `string` | `row` | Class name of the main div |
| `class-paging-control-div` | yes | `string` | `col` | Class name for the paging control div |
| `class-info-div` | yes | `string` | `col-2` | Class name for the info div |
| `class-page-size-div` | yes | `string` | `col-1` | Class name for the page size div |
| `class-paging-control` | yes | `string` | `pagination` | Class name for the paging control |
| `class-active-page` | yes | `string` | `active` | Class name for the currently active page |
| `class-total-pages` | yes | `string` | `badge badge-light` | Class name for the total pages info badge |
| `class-total-records` | yes | `string` | `badge badge-dark` | Class name for the total records info badge |
| `class-disabled-jumping-buttons` | yes | `string` | `disabled` | Class name for the navigation buttons e.g. goto first/last/prev/next buttons while they are disabled. |
| `class-page-link` | yes | `string` | null | Class name for the page link item. This value will be added next to the fixed class `page-link`. |
|<img width="450"/>|<img width="50"/>|<img width="50"/>|<img width="350"/>| [Goto top](#quick-navigation) |

`PagingTagHelper` will render a bootstrap styled paging control. By default it is like below:

````html
<!-- main div -->
<div class="row>
    <!-- paging control div -->
    <div class="col">
        <!-- page numbers unordered list -->
        <ul class="pagination">
        </ul>
    </div>

    <!-- page size div (dropdown nav) -->
    <div class="col-1">
    </div>

    <!-- info div (total pages/records) -->
    <div class="col-2">
    </div>
</div>
````

[1]:Paging-TagHelper-Number-Formats.md
