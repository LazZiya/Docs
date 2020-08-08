---
title: XLocalizer for Asp.Net Core
keywords: localization, asp.net-core, xlocalizer
description: Goodbye _"manually creating localization resources"_, welcome XLocalizer...!
author: Ziya Mollamahmut
date: 08/08/2020
versions: 1.0
---

# XLocalizer for Asp.Net Core

By [Ziya Mollamahmut][0]

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

[0]:https://github.com/LazZiya
[1]:https://rapidapi.com/translated/api/mymemory-translation-memory
[2]:../XLocalizer/setup-xml.md