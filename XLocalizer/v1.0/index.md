<!-- meta tags details, will be assigned to meta tags inside header by js -->
<div id="meta-details">
<details><sumary>meta details</summary>

> * Title: <i id="md-title">XLocalizer for Asp.Net Core</i>
> * Keywords: <i id="md-keywords">localization, asp.net-core, xlocalizer</i>
> * Description: <i id="md-description">Learn about localizing Asp.Net Core web apps with XLocalizer powered by auto translate and auto key adding.</i>
> * Author: <i id="md-author">Ziya Mollamahmut</i>
> * Date: <i id="md-date">08-Aug-2020</i>
> * Image: <i id="md-image">https://raw.githubusercontent.com/LazZiya/Docs/master/images/XLocalizer/xlocalizer-logo.PNG</i>
> * Image-alt: <i id="md-image-alt">XLocalizer Logo</i>

</detasil>
</div>

# XLocalizer for Asp.Net Core

By [Ziya Mollamahmut](https://github.com/LazZiya)

Goodbye _"manually creating localization resources"_, welcome **XLocalizer**...! 

#### What is XLocalizer
This is a nuget package that offers localization for Asp.Net Core based on _.resx_, _.xml_, _db_ or any other custom _file/db_ type. Powered by online translation and auto resource creating. XLocalizer has many powerful features and can be extended with custom tools. 

**- Online Translation :** Auto translation of missed localized values.

**- Auto Key Adding :** Auto adding missing keys to the resources files.

**- Multiple Resource Type Support :** Built-in localization support based on _.RESX_, _.XML_, _DB_. Extendable localization support based on any custom file/db type.

**- Export to Resx :** Resources from any source type can be exported to _.RESX_ files via built-in exporters.

**- Do it Fast :** Custom cache support for speeding up the process of getting localized values from sources.

**- Standard interfaces :** Easy to use due to using the standard localization interfaces: `IStringLocalizer`, `IHtmlLocalizer`, `IStringLocalizerFactory` and `IHtmlLocalizerFactory`.

#

#### Disclaimer Third Parties

All product and company names of translation services are trademarks™ or registered® trademarks of their respective holders. Use of them does not imply any affiliation with or endorsement by them.

During the development of `XLocalizer` I've used many online translation services with the freemium plan, but it is up to you to use a priced plan from the respective service.

 Each translation service has its pros and cons. [MyMemory Translate][1] provided the best results for the languages I've been working with _(in terms performans and amount of free translation requests)_. So, in this documentation you will see most samples refering to [MyMemory Translate][1] as the translation service. But you are free to use any other service that fits your needs.
#
### Next: [Xml based localization setup][2]
#


[1]:https://rapidapi.com/translated/api/mymemory-translation-memory
[2]:setup-xml.md
