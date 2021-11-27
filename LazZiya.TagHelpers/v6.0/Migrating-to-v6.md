<!-- meta tags details, will be assigned to meta tags inside header by js -->
<div id="meta-info">
<details><summary>meta info</summary>

> * Title: <i id="md-title">Migrating to v6.0</i>
> * Keywords: <i id="md-keywords">asp.net-core, taghelpers, paging, alert, language-nav</i>
> * Description: <i id="md-description">Useful taghelpers for every Asp.Net web project.</i>
> * Author: <i id="md-author">Ziya Mollamahmut</i>
> * Date: <i id="md-date">27-Nov-2021</i>
> * Image: <i id="md-image">https://github.com/LazZiya/Docs/raw/master/LazZiya.TagHelpers/v6.0/images/lazziya-tagheleprs-logo.png</i>
> * Image-alt: <i id="md-image-alt">LazZiya.TagHelpers Logo</i>
> * Version: <i id="md-version">v6.0</i>

</details>
</div>

# Migrating to v6.0

By [Ziya Mollamahmut](https://github.com/LazZiya)

`LazZiya.TagHelpers v6.0` provides support for `.net6.0` and `Bootstrap5.x`. If you have any styling issues just add `render-mode="Bootstrap5"` property to the relevant tag helper.

````html
<!-- Paging tag helper -->
<!-- Supported render modes: Bootsrap, Bootstrap5 -->
<paging render-mode="Bootstrap5" 
        page-no=1
        page-size=10
        total-pages=100>
</paging>

<!-- Alert tag helper -->
<!-- Supported render modes: Bootsrap, Bootstrap5 -->
<alert render-mode="Bootstrap5"></alert>

<!-- Language nav tag helper -->
<!-- Supported render modes: Bootsrap, Bootstrap5, Classic, FormControl -->
<language-nav render-mode="Bootstrap5"></language-nav>

````