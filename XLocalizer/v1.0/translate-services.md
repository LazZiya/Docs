<!-- meta tags details, will be assigned to meta tags inside header by js -->
<div id="meta-info">
<details><summary>meta info</summary>

> * Title: <i id="md-title">Use Online Translation Services For Localization</i>
> * Keywords: <i id="md-keywords">localization, asp.net-core, translate, online, service</i>
> * Description: <i id="md-description">Learn how to use online translation services for localization of Asp.Net Core web apps with XLocalizer.Translate.</i>
> * Author: <i id="md-author">Ziya Mollamahmut</i>
> * Date: <i id="md-date">23-Oct-2020</i>
> * Image: <i id="md-image">https://github.com/LazZiya/Docs/raw/master/XLocalizer/v1.0/images/xlocalizer-logo.png</i>
> * Image-alt: <i id="md-image-alt">XLocalizer Logo</i>
> * Version: <i id="md-version">v1.0</i>

</details>
</div>

# Use Online Translation Services For Localization

By [Ziya Mollamahmut](https://github.com/LazZiya)

Provides translation support to web applications. Can be used with `XLocalizer` or as standalsone services.

### Table of contents
- [Available translation services](#available-translation-services)
- [Use with XLocalizer](#use-with-xlocalizer)
- [Use as standalone service](#use-as-standalone-service)
- [Register multiple translation services](#register-multiple-translation-services)

#### Available translation services
Below services are already available as nugets and ready to install. 

- [XLocalizer.Translate.MyMemoryTranslate][5]
- [XLocalizer.Translate.GoogleTranslate][3]
- [XLocalizer.Translate.MicrosoftTranslate][8]
- [XLocalizer.Translate.YandexTranslate][4]
- [XLocalizer.Translate.SystranTranslate][6]
- [XLocalizer.Translate.IBMWatsonTranslate][7]

> Click on each service for more details about how to install.


Any service that implements [`ITranslator`][1] interface can be used for automatic translation with `XLocalizer` or as standalone translation services as well.


#### Use with XLocalizer
````csharp
// Register a translation service
services.AddHttpClient<ITranslator, MyMemoryTranslateService>();

// Configure XLocalizer to use the translation service 
// and enable online translation
services.AddRazorPages()
        .AddXLocalizer<LocSource, MyMemoryTranslateService>(ops =>
        {
            // ...
            ops.AutoTranslate = true;
            ops.TranslateFrom = "en";
        });
````
> Recommended read [IHttpClientFactory](https://docs.microsoft.com/en-us/dotnet/architecture/microservices/implement-resilient-applications/use-httpclientfactory-to-implement-resilient-http-requests)

If `TranslateFrom` is not defined, then `DefaultRequestCulture` will be considered as the source culture for translation.

#### Use as standalone service
````csharp
using XLocalizer.Translate;

public class IndexModel : PageModel
{
    private readonly ITranslator _translator;

    public IndexModel(ITranslator translator)
    {
        _translator = translator ?? throw new NotImplementedException(nameof(translator));
    }

    public void OnGet()
    {
        var success = _translator.TryTranslate("en", "tr", "Welcome", out string translation);
    }
}
````

Or you can use the async method of [`ITranslator`][1] interface:
````csharp
public async Task OnGetAsync()
{
    var translation = await _translator.TranslateAsync("en", "tr", "Welcome", "text");
}
````

#### Register multiple translation services
It is possible to register multiple tranlsation services then retrive specific service for translation using [`ITranslatorFactory`][2] interface.

Register multiple translation services:
````csharp
services.AddHttpClient<ITranslator, MyMemoryTranslateService>();
services.AddHttpClient<ITranslator, GoogleTranslateService>();
services.AddHttpClient<ITranslator, MicrosoftTranslateService>();
services.AddSingleton<ITranslator, IBMWatsonTranslateService>();
services.AddHttpClient<ITranslator, SystranTranslateService>();
services.AddHttpClient<ITranslator, YandexTranslateService>();
````

Retrive specific service:
````csharp
using XLocalizer.Translate;

public class IndexModel : PageModel
{
    private readonly ITranslator _translator;

    public IndexModel(ITranslatorFactory factory)
    {
        // e.g: retrive an instance of MyMemoryTranslateService
        _translator = factory.Create<MyMemoryTranslateService>();

        // or retrive an instance based on string service name
        _translator = factory.Create("MyMemory Translate");
    }
}
````

[`ITranslatorFactory`][2] is already registered by `XLocalizer`. If you are not using `XLocalizer` you need to register it in startup as below:

````csharp
using XLocalizer.Translate;
using XLocalizer.Translate.MyMemoryTranslate;

services.AddSingleton<ITranslatorFactory, TranslatorFactory<MyMemoryTranslateService>();
````


[1]:https://github.com/LazZiya/XLocalizer.Translate/blob/master/XLocalizer.Translate/ITranslator.cs
[2]:https://github.com/LazZiya/XLocalizer.Translate/blob/master/XLocalizer.Translate/ITranslatorFactory.cs
[3]:translate-services-google.md
[4]:translate-services-yandex.md
[5]:translate-services-mymemory.md
[6]:translate-services-systran.md
[7]:translate-services-ibm.md
[8]:translate-services-microsoft.md