<!-- meta tags details, will be assigned to meta tags inside header by js -->
<div id="meta-info">
<details><summary>meta info</summary>

> * Title: <i id="md-title">Localizing Model Binding Errors</i>
> * Keywords: <i id="md-keywords">localization, asp.net-core, model, binding, error, messages</i>
> * Description: <i id="md-description">Learn how to localize model binding error messages with XLocalizer in Asp.Net Core web app.</i>
> * Author: <i id="md-author">Ziya Mollamahmut</i>
> * Date: <i id="md-date">02-Sep-2020</i>
> * Image: <i id="md-image">https://github.com/LazZiya/Docs/raw/master/XLocalizer/v1.0/images/xlocalizer-logo.png</i>
> * Image-alt: <i id="md-image-alt">XLocalizer Logo</i>
> * Version: <i id="md-version">v1.0</i>

</details>
</div>

# Localizing Model Binding Errors

By [Ziya Mollamahmut](https://github.com/LazZiya)

All model binding errors are localized by XLocalizer with the default setup, so no additional steps required to localize data annotations errors. 

When the source translation culture is "en", no additional setup required for localizing model binding error messages, it will be localized automatically by `XLocalizer`. But if the source translation culture is different than "en", then we have to provide the default model binding errors in the relevant default culture, so XLocalizer can use them as source for translation.

#### Customize model binding errors

Model binding errors can be customized by providing a new object of type `XLocalizer.ErrorMessages.ModelBindingErrors` into `XLocalizerOptions` in startup file.

````csharp
services.AddRazorPages()
        .AddXLocalizer<...>(ops =>
        {
            // ...
            ops.ModelBindingErrors = new ModelBindingErrors 
            {
                AttemptedValueIsInvalidAccessor = "The value '{0}' is not valid for {1}.",
                MissingBindRequiredValueAccessor = "A value for the '{0}' parameter or property was not provided.",
                MissingKeyOrValueAccessor = "A value is required.",
                // ...
            };
        });
````

Same way we can provide the default model binding errors in a different culture other than "en".

#### Customize via json
See [Setup XLocalizer via JSON Settings][3].

#
### Next: [Identity errors][1]
#


[1]:identity-errors.md
[2]:https://github.com/LazZiya/XLocalizer/blob/master/XLocalizer/ModelBinding/IModelBindingErrorMessagesProvider.cs
[3]:setup-json.md