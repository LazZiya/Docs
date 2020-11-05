<!-- meta tags details, will be assigned to meta tags inside header by js -->
<div id="meta-info">
<details><summary>meta info</summary>

> * Title: <i id="md-title">Localizing Identity Errors</i>
> * Keywords: <i id="md-keywords">localization, asp.net-core, xlocalizer, identity, error, message</i>
> * Description: <i id="md-description">Localization of identity describer error messages in Asp.Net Core with XLocalizer.</i>
> * Author: <i id="md-author">Ziya Mollamahmut</i>
> * Date: <i id="md-date">02-Nov-2020</i>
> * Image: <i id="md-image">https://github.com/LazZiya/Docs/raw/master/XLocalizer/v1.0/images/xlocalizer-logo.png</i>
> * Image-alt: <i id="md-image-alt">XLocalizer Logo</i>
> * Version: <i id="md-version">v1.0</i>

</details>
</div>

# Localized Identity Errors

By [Ziya Mollamahmut](https://github.com/LazZiya)

All identity errors are localized by XLocalizer with the default setup, so no additional steps required to localize identity errors.

When the source translation culture is "en", no additional setup required for localizing identity error messages, it will be localized automatically by `XLocalizer`. But if the source translation culture is different than "en", then we have to provide the default identity errors in the relevant default culture, so XLocalizer can use them as source for translation.

#### Customize identity errors

Model binding errors can be customized by providing a new object of type `XLocalizer.ErrorMessages.IdentityErrors` into `XLocalizerOptions` in startup file.

````csharp
services.AddRazorPages()
        .AddXLocalizer<...>(ops =>
        {
            // ...
            ops.IdentityErrors = new IdentityErrors 
            {
                DuplicateEmail = "Email '{0}' is already taken.",
                DuplicateUserName = "User name '{0}' is already taken.",
                InvalidEmail = "Email '{0}' is invalid.",
                // ...
            };
        });
````

Same way we can provide the default model binding errors in a different culture other than "en".

#### Customize via json
See [Setup XLocalizer via JSON Settings][3].

#
### Next: [Localizing custom backend messages][1]
#


[1]:localizing-custom-backend-messages.md
[2]:https://github.com/LazZiya/XLocalizer/blob/master/XLocalizer/Identity/IIdentityErrorMessagesProvider.cs
[3]:setup-json.md