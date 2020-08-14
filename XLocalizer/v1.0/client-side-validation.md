<!-- meta tags details, will be assigned to meta tags inside header by js -->
<div id="meta-info">
<details><summary>meta info</summary>

> * Title: <i id="md-title">Client Side Validation</i>
> * Keywords: <i id="md-keywords">localization, asp.net-core, xlocalizer, client, side, validation</i>
> * Description: <i id="md-description">Setup client side validation in Asp.Net Core web application.</i>
> * Author: <i id="md-author">Ziya Mollamahmut</i>
> * Date: <i id="md-date">08-Aug-2020</i>
> * Image: <i id="md-image">https://github.com/LazZiya/Docs/raw/master/XLocalizer/v1.0/images/xlocalizer-logo.png</i>
> * Image-alt: <i id="md-image-alt">XLocalizer Logo</i>
> * Version: <i id="md-version">v1.0</i>

</details>
</div>

## Client Side Validation

By [Ziya Mollamahmut](https://github.com/LazZiya)

Client side validation is done during filling the form before the submit button is clicked. It requires adding validation span as below:

````html
<form method="post>
    <label asp-for="Name" />
    <input as-for="Name" />
    <span asp-validation-for="Name" />
    <button type="submit">Submit</button>
</form>
````

In order to see localized client side validation messages, just add the validation scripts to the `Scripts` section of the page. The relevant partial is already provided in the default project template:

````html
@section Scripts {
    <partial name="_ValidationScriptsPartial" />
}
````

You can add the relevant scripts manually as well:

````html
<script src="~/lib/jquery/dist/jquery.js"></script>
<script src="~/lib/jquery-validation/dist/jquery.validate.js"></script>
<script src="~/lib/jquery-validation-unobtrusive/jquery.validate.unobtrusive.js"></script>
````

#
### Next: [Validating localized input][1]
#


[1]:validating-localized-input.md
