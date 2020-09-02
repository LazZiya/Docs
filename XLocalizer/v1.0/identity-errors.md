<!-- meta tags details, will be assigned to meta tags inside header by js -->
<div id="meta-info">
<details><summary>meta info</summary>

> * Title: <i id="md-title">Localized Identity Errors</i>
> * Keywords: <i id="md-keywords">localization, asp.net-core, xlocalizer, identity, error, message</i>
> * Description: <i id="md-description">Localization of identity describer error messages in Asp.Net Core with XLocalizer.</i>
> * Author: <i id="md-author">Ziya Mollamahmut</i>
> * Date: <i id="md-date">02-Sep-2020</i>
> * Image: <i id="md-image">https://github.com/LazZiya/Docs/raw/master/XLocalizer/v1.0/images/xlocalizer-logo.png</i>
> * Image-alt: <i id="md-image-alt">XLocalizer Logo</i>
> * Version: <i id="md-version">v1.0</i>

</details>
</div>

# Localized Identity Errors

By [Ziya Mollamahmut](https://github.com/LazZiya)

If the source translation culture is "en", no additional setup required for identity error messages, it will be localized automatically by XLocalizer, you don't even need to add them manually if you have enabled auto translation and auto adding keys.

But if the source translation culture is different than "en", then we have to provide the default identity describer errors in the relevant default culture, so XLocalizer can use them as source for translation.

#### How to customize defatul model binding errors

* Create a new class (e.g.: `CustomIdentityDescriberErrors`) that implements [`IIdentityErrorMessagesProvider`][2] and provide your custom identity describer errors.

````csharp
public class CustomIdentityDescriberErrors : IIdentityErrorMessagesProvider
{
    string IIdentityErrorMessagesProvider.DuplicateEmail => "Email '{0}' is already taken.";

    string IIdentityErrorMessagesProvider.DuplicateUserName => "User name '{0}' is already taken.";

    string IIdentityErrorMessagesProvider.InvalidEmail => "Email '{0}' is invalid.";

    string IIdentityErrorMessagesProvider.DuplicateRoleName => "Role name '{0}' is already taken.";

    string IIdentityErrorMessagesProvider.InvalidRoleName => "Role name '{0}' is invalid.";

    string IIdentityErrorMessagesProvider.InvalidToken => "Invalid token.";

    string IIdentityErrorMessagesProvider.InvalidUserName => "User name '{0}' is invalid, can only contain letters or digits.";

    string IIdentityErrorMessagesProvider.LoginAlreadyAssociated => "A user with this login already exists.";

    string IIdentityErrorMessagesProvider.PasswordMismatch => "Incorrect password.";

    string IIdentityErrorMessagesProvider.PasswordRequiresDigit => "Passwords must have at least one digit ('0'-'9').";

    string IIdentityErrorMessagesProvider.PasswordRequiresLower => "Passwords must have at least one lowercase ('a'-'z').";

    string IIdentityErrorMessagesProvider.PasswordRequiresNonAlphanumeric => "Passwords must have at least one non alphanumeric character.";

    string IIdentityErrorMessagesProvider.PasswordRequiresUniqueChars => "Passwords must use at least {0} different characters.";

    string IIdentityErrorMessagesProvider.PasswordRequiresUpper => "Passwords must have at least one uppercase ('A'-'Z').";

    string IIdentityErrorMessagesProvider.PasswordTooShort => "Passwords must be at least {0} characters.";

    string IIdentityErrorMessagesProvider.UserAlreadyHasPassword => "User already has a password set.";

    string IIdentityErrorMessagesProvider.UserAlreadyInRole => "User already in role '{0}'.";

    string IIdentityErrorMessagesProvider.UserNotInRole => "User is not in role '{0}'.";

    string IIdentityErrorMessagesProvider.UserLockoutNotEnabled => "Lockout is not enabled for this user.";

    string IIdentityErrorMessagesProvider.RecoveryCodeRedemptionFailed => "Recovery code redemption failed.";

    string IIdentityErrorMessagesProvider.ConcurrencyFailure => "Optimistic concurrency failure, object has been modified.";

    string IIdentityErrorMessagesProvider.DefaultError => "An unknown failure has occurred.";
}
````

* Register in startup:
````csharp
services.AddSingleton<IIdentityErrorMessagesProvider, CustomIdentityDescriberErrors>();
````

These errors will override the system default errors for the default culture, so if you have a default culture other that "en" you can provide your localized errors in this class. This way XLocalizer can translate and add them to the resource file.


#
### Next: [Localizing custom backend messages][1]
#


[1]:localizing-custom-backend-messages.md
[2]:https://github.com/LazZiya/XLocalizer/blob/master/XLocalizer/Identity/IIdentityErrorMessagesProvider.cs