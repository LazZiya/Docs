<!-- meta tags details, will be assigned to meta tags inside header by js -->
<div id="meta-info">
<details><summary>meta info</summary>

> * Title: <i id="md-title">Localizing Identity Errors</i>
> * Keywords: <i id="md-keywords">localization, asp.net-core, express-localization, identity, errors</i>
> * Description: <i id="md-description">Localization of identity errors in Asp.Net Core with ExpressLocalization.</i>
> * Author: <i id="md-author">Ziya Mollamahmut</i>
> * Date: <i id="md-date">27-Sep-2019</i>
> * Image: <i id="md-image">https://github.com/LazZiya/Docs/raw/master/LazZiya.ExpressLocalization/v3.0/images/lazziya-express-localization-logo.png</i>
> * Image-alt: <i id="md-image-alt">LazZiya.ExpressLocalization Logo</i>
> * Version: <i id="md-version">v3.0</i>

</details>
</div>

# Localizing Identity Errors

By [Ziya Mollamahmut](https://github.com/LazZiya)

Identity errors localization setup is done by default with `ExpressLocalization`, you only need to provide the localized versions for the below messages in resx files:

### Default identity describer errors
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