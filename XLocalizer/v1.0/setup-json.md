<!-- meta tags details, will be assigned to meta tags inside header by js -->
<div id="meta-info">
<details><summary>meta info</summary>

> * Title: <i id="md-title">XLocalizer Setup via JSON Settings</i>
> * Keywords: <i id="md-keywords">localization, asp.net-core, setup, startup, json, appsettings, options</i>
> * Description: <i id="md-description">Learn how to setup XLocalizer via json settings.</i>
> * Author: <i id="md-author">Ziya Mollamahmut</i>
> * Date: <i id="md-date">31-Mar-2021</i>
> * Image: <i id="md-image">https://github.com/LazZiya/Docs/raw/master/XLocalizer/v1.0/images/xlocalizer-logo.png</i>
> * Image-alt: <i id="md-image-alt">XLocalizer Logo</i>
> * Version: <i id="md-version">v1.0</i>

</details>
</div>

# XLocalizer Setup via JSON Settings

By [Ziya Mollamahmut](https://github.com/LazZiya)

In some cases you may want to provide all `XLocalizerOptions` in a json file like `appsettings.json`. Simply get the relevant configuration section and bind it to `XLocalizerOptions` as below:

````csharp
services.AddRazorPages()
        .AddXLocalizer<...>(ops => Configuration.GetSection("XLocalizerOptions").Bind(ops));
````

#### Create XLocalizerOptions JSON Settings
All available options are listed under a section named **XLocalizerOptions** in the json settings. These settings provides an easy to configure one place to customize all framework error messages (validation, model binding and identity errors) 

````json
{
  "XLocalizerOptions": {
    "ResourcesPath": "LocalizationResources",
    "UseExpressValidationAttributes": false,
    "AutoAddKeys": false,
    "AutoTranslate": false,
    "UseExpressMemoryCache": true,
    "TranslateFromCulture": "en",
    "ValidationErrors": {
      "CompareAttribute_MustMatch": "'{0}' and '{1}' do not match. They should not be different!",
      "CreditCardAttribute_Invalid": "The {0} field is not a valid credit card number.",
      "CustomValidationAttribute_ValidationError": "{0} is not valid.",
      "DataTypeAttribute_EmptyDataTypeString": "The custom DataType string cannot be null or empty.",
      "EmailAddressAttribute_Invalid": "The {0} field is not a valid e-mail address.",
      "FileExtensionsAttribute_Invalid": "The {0} field only accepts files with the following extensions: {1}",
      "MaxLengthAttribute_ValidationError": "The field {0} must be a string or array type with a maximum length of '{1}'.",
      "MinLengthAttribute_ValidationError": "The field {0} must be a string or array type with a minimum length of '{1}'.",
      "PhoneAttribute_Invalid": "The {0} field is not a valid phone number.",
      "RangeAttribute_ValidationError": "The field {0} must be between {1} and {2}.",
      "RegexAttribute_ValidationError": "The field {0} must match the regular expression '{1}'.",
      "RequiredAttribute_ValidationError": "The {0} field is required. Don't bypass this field!",
      "StringLengthAttribute_ValidationError": "The field {0} must be a string with a maximum length of {1}.",
      "StringLengthAttribute_ValidationErrorIncludingMinimum": "The field {0} must be a string with a minimum length of {2} and a maximum length of {1}.",
      "UrlAttribute_Invalid": "The {0} field is not a valid fully-qualified http, https, or ftp URL.",
      "ValidationAttribute_ValidationError": "The field {0} is invalid."
    },
    "IdentityErrors": {
      "DuplicateEmail": "Email '{0}' is already taken.",
      "DuplicateUserName": "User name '{0}' is already taken. Please try another one.",
      "InvalidEmail": "Email '{0}' is invalid.",
      "DuplicateRoleName": "Role name '{0}' is already taken.",
      "InvalidRoleName": "Role name '{0}' is invalid.",
      "InvalidToken": "Invalid token.",
      "InvalidUserName": "User name '{0}' is invalid, can only contain letters or digits.",
      "LoginAlreadyAssociated": "A user with this login already exists.",
      "PasswordMismatch": "Incorrect password.",
      "PasswordRequiresDigit": "Passwords must have at least one digit ('0'-'9').",
      "PasswordRequiresLower": "Passwords must have at least one lowercase ('a'-'z').",
      "PasswordRequiresNonAlphanumeric": "Passwords must have at least one non alphanumeric character.",
      "PasswordRequiresUniqueChars": "Passwords must use at least {0} different characters.",
      "PasswordRequiresUpper": "Passwords must have at least one uppercase ('A'-'Z').",
      "PasswordTooShort": "Passwords must be at least {0} characters.",
      "UserAlreadyHasPassword": "User already has a password set.",
      "UserAlreadyInRole": "User already in role '{0}'.",
      "UserNotInRole": "User is not in role '{0}'.",
      "UserLockoutNotEnabled": "Lockout is not enabled for this user.",
      "RecoveryCodeRedemptionFailed": "Recovery code redemption failed.",
      "ConcurrencyFailure": "Optimistic concurrency failure, object has been modified.",
      "DefaultError": "An unknown failure has occurred."
    },
    "ModelBindingErrors": {
      "AttemptedValueIsInvalidAccessor": "The value '{0}' is not valid for {1}.",
      "MissingBindRequiredValueAccessor": "A value for the '{0}' parameter or property was not provided.",
      "MissingKeyOrValueAccessor": "A value is required.",
      "MissingRequestBodyRequiredValueAccessor": "A non-empty request body is required.",
      "NonPropertyAttemptedValueIsInvalidAccessor": "The value '{0}' is not valid.",
      "NonPropertyUnknownValueIsInvalidAccessor": "The supplied value is invalid.",
      "NonPropertyValueMustBeANumberAccessor": "The field must be a number.",
      "UnknownValueIsInvalidAccessor": "The supplied value is invalid for {0}.",
      "ValueIsInvalidAccessor": "The value '{0}' is invalid. You entered something weired!",
      "ValueMustBeANumberAccessor": "The field {0} must be a number. Don't use letters or special characters.",
      "ValueMustNotBeNullAccessor": "The value '{0}' is invalid. This can't be null."
    }
  }
}
````