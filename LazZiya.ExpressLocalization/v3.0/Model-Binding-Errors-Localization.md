<!-- meta tags details, will be assigned to meta tags inside header by js -->
<div id="meta-info">
<details><summary>meta info</summary>

> * Title: <i id="md-title">Localizing Model Binding Errors</i>
> * Keywords: <i id="md-keywords">localization, asp.net-core, model, binding, error, messages</i>
> * Description: <i id="md-description">Learn how to localize model binding error messages with ExpressLocalization in Asp.Net Core web app.</i>
> * Author: <i id="md-author">Ziya Mollamahmut</i>
> * Date: <i id="md-date">27-Sep-2019</i>
> * Image: <i id="md-image">https://github.com/LazZiya/Docs/raw/master/LazZiya.ExpressLocalization/v3.0/images/lazziya-express-localization-logo.png</i>
> * Image-alt: <i id="md-image-alt">LazZiya.ExpressLocalization Logo</i>
> * Version: <i id="md-version">v3.0</i>

</details>
</div>

# Localizing Model Binding Errors

By [Ziya Mollamahmut](https://github.com/LazZiya)

Model binding error localization setup is done by default with `ExpressLocalization`, you only need to provide the localized versions for the below messages in resx files:

### Default model binding errors

````
A non-empty request body is required.
A value for the '{0}' parameter or property was not provided.
A value is required.
The field {0} must be a number.
The supplied value is invalid for {0}.
The supplied value is invalid.
The value '{0}' is invalid.
The value '{0}' is not valid for {1}.
The value '{0}' is not valid.
````