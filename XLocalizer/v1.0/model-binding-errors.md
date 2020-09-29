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

If the source translation culture is "en", no additional setup required for model binding error messages, it will be localized automatically by `XLocalizer`, you don't even need to add them manually to the resource file if you have enabled auto translation and auto adding keys.

But if the source translation culture is different than "en", then we have to provide the default model binding errors in the relevant default culture, so XLocalizer can use them as source for translation.

#### How to customize default model binding errors

* Create a new class (e.g.: `CustomModelBindingErrors`) that implements [`IModelBindingErroeMessagesProvider`][2] and provide your custom model binding errors.
* Register your class in startup.

````csharp
public class CustomModelBindingErrors : IModelBindingErrorMessagesProvider
{
    string IModelBindingErrorMessagesProvider.AttemptedValueIsInvalidAccessor => "The value '{0}' is not valid for {1}.";

    string IModelBindingErrorMessagesProvider.MissingBindRequiredValueAccessor => "A value for the '{0}' parameter or property was not provided.";

    string IModelBindingErrorMessagesProvider.MissingKeyOrValueAccessor => "A value is required.";

    string IModelBindingErrorMessagesProvider.MissingRequestBodyRequiredValueAccessor => "A non-empty request body is required.";

    string IModelBindingErrorMessagesProvider.NonPropertyAttemptedValueIsInvalidAccessor => "The value '{0}' is not valid.";

    string IModelBindingErrorMessagesProvider.NonPropertyUnknownValueIsInvalidAccessor => "The supplied value is invalid.";

    string IModelBindingErrorMessagesProvider.NonPropertyValueMustBeANumberAccessor => "The field must be a number.";

    string IModelBindingErrorMessagesProvider.UnknownValueIsInvalidAccessor => "The supplied value is invalid for {0}.";

    string IModelBindingErrorMessagesProvider.ValueIsInvalidAccessor => "The value '{0}' is invalid.";

    string IModelBindingErrorMessagesProvider.ValueMustBeANumberAccessor => "The field {0} must be a number.";

    string IModelBindingErrorMessagesProvider.ValueMustNotBeNullAccessor => "The value '{0}' is invalid.";
}
````

* Register in startup:
````csharp
services.AddSingleton<IModelBindingErrorMessagesProvider, CustomModelBindingErrors>();
````

These errors will override the system default errors for the default culture, so if you have a default culture other that "en" you can provide your localized errors in this class. This way XLocalizer can translate and add them to the resource file.


#
### Next: [Identity errors][1]
#


[1]:identity-errors.md
[2]:https://github.com/LazZiya/XLocalizer/blob/master/XLocalizer/ModelBinding/IModelBindingErrorMessagesProvider.cs
