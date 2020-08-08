---
title: Paging TagHelper Number Formats
keywords: asp.net-core, taghelpers, paging, control, pagination, number, formats, attributes
description: Change the number fortmat of PagingTagHelper for Asp.Net Core.
author: Ziya Mollamahmut
date: 08-Aug-2020
versions: 4.x, 5.x
---

# Paging TagHelper Number Formats

By [Ziya Mollamahmut](https://github.com/LazZiya)

### Changing numbers format
Paging taghelper provides a handy feature to display numbers in different formats (Arabic, Hindi, Roman, Hex, ...etc.)

Just provide the relevant format to the taghelper. For example to use `Hex` numbers:
````html
@using LazZiya.TagHelpers.Utilities

<paging page-no="Model.PageNo"
        page-size="Model.PageSize"
        total-records="Model.TotalRecords"
        number-format="@NumberFormats.Hex">
</paging>
````

Sample to use `Roman` numbers:
````html
@using LazZiya.TagHelpers.Utilities

<paging page-no="Model.PageNo"
        page-size="Model.PageSize"
        total-records="Model.TotalRecords"
        number-format="@NumberFormats.Roman">
</paging>
````

![PagingTagHelper - number formats](https://github.com/LazZiya/Docs/raw/master/images/LazZiya.TagHelpers/paging-tag-helper-number-formats.PNG)

### Custom number format
You may specify a custom number format by passing a string list delimited by space char, each char represents a number by order
````html
<paging page-no="Model.PageNo"
        page-size="Model.PageSize"
        total-records="Model.TotalRecords"
        number-format="A B C D E F G H I K">
</paging>
````
So, A=0, B=1, ... K=9

### Built-in number formats
All available number formats with `NumberFormats` class:
````cs
Default     // system default
Hex         // 0 .. 9 A .. F
Roman       //   I II III IV ... C̅M̅ M̅
Arabic      // 0 1 2 3 4 5 6 7 8 9
Hindi       // ٩ ٨ ٧ ٦ ٥ ٤ ٣ ٢ ١ ٠
Brah        // 𑁦 𑁧 𑁨 𑁩 𑁪 𑁫 𑁬 𑁭 𑁮 𑁯
Beng        // ০ ১ ২ ৩ ৪ ৫ ৬ ৭ ৮ ৯
Deva        // ० १ २ ३ ४ ५ ६ ७ ८ ९
Farsi       // ۰ ۱ ۲ ۳ ۴ ۵ ۶ ۷ ۸ ۹
Fullwide    // ０ １ ２ ３ ４ ５ ６ ７ ８ ９
Knda        // ೦ ೧ ೨ ೩ ೪ ೫ ೬ ೭ ೮ ೯
Gujr        // ૦ ૧ ૨ ૩ ૪ ૫ ૬ ૭ ૮ ૯
Guru        // ੦ ੧ ੨ ੩ ੪ ੫ ੬ ੭ ੮ ੯
Hanidec     // 〇 一 二 三 四 五 六 七 八 九
Java        // ꧐ ꧑ ꧒ ꧓ ꧔ ꧕ ꧖ ꧗ ꧘ ꧙
Khmr        // ០ ១ ២ ៣ ៤ ៥ ៦ ៧ ៨ ៩
Laoo        // ໐ ໑ ໒ ໓ ໔ ໕ ໖ ໗ ໘ ໙
Latin       // 0 1 2 3 4 5 6 7 8 9
Mathbold    // 𝟎 𝟏 𝟐 𝟑 𝟒 𝟓 𝟔 𝟕 𝟖 𝟗
Mathborder  // 𝟘 𝟙 𝟚 𝟛 𝟜 𝟝 𝟞 𝟟 𝟠 𝟡
Mathmono    // 𝟶 𝟷 𝟸 𝟹 𝟺 𝟻 𝟼 𝟽 𝟾 𝟿
Mathanb     // 𝟬 𝟭 𝟮 𝟯 𝟰 𝟱 𝟲 𝟳 𝟴 𝟵
Mathsans    // 𝟢 𝟣 𝟤 𝟥 𝟦 𝟧 𝟨 𝟩 𝟪 𝟫
Mlym        // ൦ ൧ ൨ ൩ ൪ ൫ ൬ ൭ ൮ ൯
Mong        // ᠐ ᠑ ᠒ ᠓ ᠔ ᠕ ᠖  ᠗ ᠘ ᠙
Mymr        // ၀ ၁ ၂ ၃ ၄ ၅ ၆ ၇ ၈ ၉
Mymrshan    // ႐ ႑ ႒ ႓ ႔ ႕ ႖ ႗ ႘ ႙
Mymtlng     // ꧰ ꧱ ꧲ ꧳ ꧴ ꧵ ꧶ ꧷ ꧸ ꧹
Nkoo        // ߀ ߁ ߂ ߃ ߄ ߅ ߆ ߇ ߈ ߉
Olck        // ᱐ ᱑ ᱒ ᱓ ᱔ ᱕ ᱖ ᱗ ᱘ ᱙
Orya        // ୦ ୧ ୨ ୩ ୪ ୫ ୬ ୭ ୮ ୯
Osma        // 𐒠 𐒡 𐒢 𐒣 𐒤 𐒥 𐒦 𐒧 𐒨 𐒩
Sinh        // ෦ ෧ ෨ ෩ ෪ ෫ ෬ ෭ ෮ ෯
Talu        // ᧐ ᧑ ᧒ ᧓ ᧔ ᧕ ᧖ ᧗ ᧘ ᧙
Tamldec     // ௦ ௧ ௨ ௩ ௪ ௫ ௬ ௭ ௮ ௯
Telu        // ౦ ౧ ౨ ౩ ౪ ౫ ౬ ౭ ౮ ౯
Thai        // ๐ ๑ ๒ ๓ ๔ ๕ ๖ ๗ ๘ ๙
Tibt        // ༠ ༡ ༢ ༣ ༤ ༥ ༦ ༧ ༨ ༩
Vaii        // ꘠ ꘡ ꘢ ꘣ ꘤ ꘥ ꘦ ꘧ ꘨ ꘩
````