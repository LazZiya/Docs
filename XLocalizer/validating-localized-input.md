## Validating Localized Input

Some input fields need to be localized (decimal numbers, dates, ...etc.). But without client side localizing libraries this could make problems with different cultures (e.g. decimal numbers 1.23 and 1,23).

To have client side validation full compatibility with all cultures see [`LocalizationValdiationScripts`][1] taghelper from [`LazZiya.TagHelpers`][2]

[1]:../LazZiya/TagHelpers/LocalizationValidationScripts-TagHelper-Setup.md
[2]:https://github.com/LazZiya/TagHelpers