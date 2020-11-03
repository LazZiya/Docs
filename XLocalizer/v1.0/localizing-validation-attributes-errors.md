<!-- meta tags details, will be assigned to meta tags inside header by js -->
<div id="meta-info">
<details><summary>meta info</summary>

> * Title: <i id="md-title">Localizing Validiation Errors</i>
> * Keywords: <i id="md-keywords">localization, asp.net-core, data-annotations, validation, attributes</i>
> * Description: <i id="md-description">Learn how to localize DataAnnotations error messages with XLocalizer in Asp.Net Core web app.</i>
> * Author: <i id="md-author">Ziya Mollamahmut</i>
> * Date: <i id="md-date">02-Nov-2020</i>
> * Image: <i id="md-image">https://github.com/LazZiya/Docs/raw/master/XLocalizer/v1.0/images/xlocalizer-logo.png</i>
> * Image-alt: <i id="md-image-alt">XLocalizer Logo</i>
> * Version: <i id="md-version">v1.0</i>

</details>
</div>

# Localizing Valdiation Errors

By [Ziya Mollamahmut](https://github.com/LazZiya)

All validation errors are localized by XLocalizer with the default setup, so no additional steps required to localize validation errors. What is more, **there is no need to provide an error message inside valdiation attributes!** All attributes will have an error message assigned and localized by XLocalizer by default.

Below are sample attributes with the default error messages they produce:

````csharp
// "The {0} field is required."
[Required]

// "The field {0} must be a string with a maximum length of {1}."
[StringLength(10)]

// "The field {0} must be a string with a minimum length of {2} and a maximum length of {1}."
[StringLength(10, MinimumLength=3)]

// "The field {0} must be between {1} and {2}."
[Range(3, 10)]

// "The field {0} must be a string or array type with a minimum length of '{1}'."
[MinLength(3)]

// "The field {0} must be a string or array type with a maximum length of '{1}'."
[MaxLength(10)]

// "'{0}' and '{1}' do not match."
[Compare("other_field")]

// "The field {0} must match the regular expression '{1}'."
[RegularExpression("regex_pattern")]

// "The {0} field is not a valid credit card number."
[CreditCard]

// "{0} is not valid."
[CustomValdiation]

// "The {0} field is not a valid e-mail address."
[EmailAddress]

// "The {0} field only accepts files with the following extensions: {1}"
[FileExtensions]

// "The {0} field is not a valid phone number."
[Phone]

// "The {0} field is not a valid fully-qualified http, https, or ftp URL."
[Url]
```` 


#### Customize validation errors

Validation errors can be customized by providing a new object of type `XLocalizer.ErrorMessages.ValidationErrors` into `XLocalizerOptions` in startup file.

````csharp
services.AddRazorPages()
        .AddXLocalizer<...>(ops =>
        {
            // ...
            ops.ValidationErrors = new ValidationErrors 
            {
                RequiredAttribute_ValidationError = "The {0} field is required.",
                CompareAttribute_MustMatch = "'{0}' and '{1}' do not match.",
                StringLengthAttribute_ValidationError = "The field {0} must be a string with a maximum length of {1}.",
                // ...
            };
        });
````

Same way we can provide the default validiation errors in a different culture other than "en".

#### Customize via json
See [Setup XLocalizer via JSON Settings][2].

#
### Next: [Model binding errors][1]
#


[1]:model-binding-errors.md
[2]:setup-json.md