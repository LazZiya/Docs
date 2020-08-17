<!-- meta tags details, will be assigned to meta tags inside header by js -->
<div id="meta-info">
<details><summary>meta info</summary>

> * Title: <i id="md-title">Localized Identity Errors</i>
> * Keywords: <i id="md-keywords">localization, asp.net-core, xlocalizer, identity, error, message</i>
> * Description: <i id="md-description">Localization of identity describer error messages in Asp.Net Core with XLocalizer.</i>
> * Author: <i id="md-author">Ziya Mollamahmut</i>
> * Date: <i id="md-date">08-Aug-2020</i>
> * Image: <i id="md-image">https://github.com/LazZiya/Docs/raw/master/XLocalizer/v1.0/images/xlocalizer-logo.png</i>
> * Image-alt: <i id="md-image-alt">XLocalizer Logo</i>
> * Version: <i id="md-version">v1.0</i>

</details>
</div>

# Localized Identity Errors

By [Ziya Mollamahmut](https://github.com/LazZiya)

No additional setup required for identity error messages, it will be localized automatically by XLocalizer, you don't even need to add them manually if you have enabled auto translation and auto adding keys.

Just in case you want to manually add the model binding messages see them below:

````
A user with this login already exists.
An unknown failure has occurred.
Email '{0}' is already taken.
Email '{0}' is invalid.
Incorrect password.
Invalid token.
Lockout is not enabled for this user.
Optimistic concurrency failure, object has been modified.
Passwords must be at least {0} characters.
Passwords must have at least one digit ('0'-'9').
Passwords must have at least one lowercase ('a'-'z').
Passwords must have at least one non alphanumeric character.
Passwords must have at least one uppercase ('A'-'Z').
Passwords must use at least {0} different characters.
Recovery code redemption failed.
Role name '{0}' is already taken.
Role name '{0}' is invalid.
User already has a password set.
User already in role '{0}'.
User is not in role '{0}'.
User name '{0}' is already taken.
User name '{0}' is invalid, can only contain letters or digits.
````

#
### Next: [Localizing custom backend messages][1]
#


[1]:localizing-custom-backend-messages.md
