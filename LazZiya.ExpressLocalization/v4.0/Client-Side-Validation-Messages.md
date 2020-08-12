---
title: Localization of Client Side Validation Messages
keywords: localization, asp.net-core, express-localization, client, side, validation
description: Learn about localizing client side valdiation error messages with ExpressLocalization in Asp.Net Core.
author: Ziya Mollamahmut
date: 08-Aug-2020
versions: 1.x, 2.x, 3.x, 4.x
---

# Localization of Client Side Validation Messages

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