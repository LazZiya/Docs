---
title: Client Side Validation
keywords: localization, asp.net-core, xlocalizer, client, side, validation
description: setup client side validation in Asp.Net Core web application.
author: Ziya Mollamahmut
date: 08-Aug-2020
versions: 1.0
---

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
