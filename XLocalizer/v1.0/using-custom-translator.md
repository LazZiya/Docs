<!-- meta tags details, will be assigned to meta tags inside header by js -->
<div id="meta-info">
<details><summary>meta info</summary>

> * Title: <i id="md-title">Custom Translation Service</i>
> * Keywords: <i id="md-keywords">localization, asp.net-core, translate, custom, service</i>
> * Description: <i id="md-description">Learn how to create custom translation service to use for localizing Asp.Net Core web apps with XLocalizer.</i>
> * Author: <i id="md-author">Ziya Mollamahmut</i>
> * Date: <i id="md-date">08-Aug-2020</i>
> * Image: <i id="md-image">https://github.com/LazZiya/Docs/raw/master/XLocalizer/v1.0/images/xlocalizer-logo.png</i>
> * Image-alt: <i id="md-image-alt">XLocalizer Logo</i>
> * Version: <i id="md-version">v1.0</i>

</details>
</div>

# Custom Translation Service

By [Ziya Mollamahmut](https://github.com/LazZiya)

Any custom translation service that implements [`ITranslator`][1] interface can be used with `XLocalizer`.

### See already implemented translation services

- [GoogleTranslateService][2]
- [YandexTranslateService][3]
- [MyMemoryTranslateService][4]
- [SystranTranslateService][5]
- [IBMWatsonTranslateService][6]

### Sample custom translator
````csharp
using System.Collections.Generic;
using System.Net.Http;
using System.Threading.Tasks;
using Microsoft.Extensions.Configuration;
using Microsoft.Extensions.Logging;
using System;
using Newtonsoft.Json;
using System.Net;

namespace XLocalizer.Translate.GoogleTranslate
{
    /// <summary>
    /// Google translate service
    /// </summary>
    public class GoogleTranslateService : ITranslator
    {
        /// <summary>
        /// Service name
        /// </summary>
        public string ServiceName => "Google Translate";

        private readonly HttpClient _httpClient;
        private readonly ILogger _logger;

        /// <summary>
        /// Initialzie google translate service
        /// </summary>
        /// <param name="httpClient"></param>
        /// <param name="configuration"></param>
        /// <param name="logger"></param>
        public GoogleTranslateService(HttpClient httpClient, IConfiguration configuration, ILogger<GoogleTranslateService> logger)
        {
            _httpClient = httpClient ?? throw new NullReferenceException(nameof(httpClient));

            var _rapidApiKey = configuration["XLocalizer.Translate:RapidApiKey"] ?? throw new NullReferenceException("RapidApi key not found");
            _httpClient.DefaultRequestHeaders.Add("x-rapidapi-key", _rapidApiKey);
            _httpClient.DefaultRequestHeaders.Add("x-rapidapi-host", "google-translate1.p.rapidapi.com");

            _logger = logger;
        }

        /// <summary>
        /// Run async translation task
        /// </summary>
        /// <param name="source">Source language e.g. en</param>
        /// <param name="target">Target language e.g. tr</param>
        /// <param name="text">Text to be translated</param>
        /// <param name="format">Text format: html or text</param>
        /// <returns><see cref="TranslationResult"/></returns>
        public async Task<TranslationResult> TranslateAsync(string source, string target, string text, string format)
        {
            try
            {
                var list = new List<KeyValuePair<string, string>>();
                list.Add(new KeyValuePair<string, string>("format", format));
                list.Add(new KeyValuePair<string, string>("source", source));
                list.Add(new KeyValuePair<string, string>("target", target));
                list.Add(new KeyValuePair<string, string>("q", text));

                var appContent = new FormUrlEncodedContent(list);

                var response = await _httpClient.PostAsync("https://google-translate1.p.rapidapi.com/language/translate/v2", appContent);
                _logger.LogInformation($"Response: {ServiceName} - {response.StatusCode}");
                /*
                 * Sample response content for "Back" translation
                 * {
                 *     "data": { 
                 *         "translations": [ 
                 *                 { "translatedText": "إلغاء" }
                 *             ]
                 *     }
                 * } 
                 * */
                var responseContent = await response.Content.ReadAsStringAsync();

                var responseDto = JsonConvert.DeserializeObject<GoogleTranslateResult>(responseContent);

                return new TranslationResult
                {
                    Text = responseDto.Data.Translations[0].TranslatedText,
                    StatusCode = response.StatusCode,
                    Target = target,
                    Source = source
                };
            }
            catch (Exception e)
            {
                _logger.LogError($"Error {ServiceName} - {e.Message}");
            }

            return new TranslationResult
            {
                StatusCode = System.Net.HttpStatusCode.InternalServerError,
                Text = text,
                Target = target,
                Source = source
            };
        }

        /// <summary>
        /// 
        /// </summary>
        /// <param name="source"></param>
        /// <param name="target"></param>
        /// <param name="text"></param>
        /// <param name="translation"></param>
        /// <returns></returns>
        public bool TryTranslate(string source, string target, string text, out string translation)
        {
            var trans = Task.Run(() => TranslateAsync(source, target, text, "text")).GetAwaiter().GetResult();

            if (trans.StatusCode == HttpStatusCode.OK)
            {
                translation = trans.Text;
                return true;
            }

            translation = text;
            return false;
        }
    }
}
````


[1]:https://github.com/LazZiya/XLocalizer.Translate/blob/master/XLocalizer.Translate/ITranslator.cs
[2]:https://github.com/LazZiya/XLocalizer.Translate.GoogleTranslate/blob/master/XLocalizer.Translate.GoogleTranslate/GoogleTranslateService.cs
[3]:https://github.com/LazZiya/XLocalizer.Translate.YandexTranslate/blob/master/XLocalizer.Translate.YandexTranslate/YandexTranslateService.cs
[4]:https://github.com/LazZiya/XLocalizer.Translate.MyMemoryTranslate/blob/master/XLocalizer.Translate.MyMemoryTranslate/MyMemoryTranslateService.cs
[5]:https://github.com/LazZiya/XLocalizer.Translate.SystranTranslate/blob/master/XLocalizer.Translate.SystranTranslate/SystranTranslateService.cs
[6]:https://github.com/LazZiya/XLocalizer.Translate.IBMWatsonTranslate/blob/master/XLocalizer.Translate.IBMWatsonTranslate/IBMWatsonTranslateService.cs
