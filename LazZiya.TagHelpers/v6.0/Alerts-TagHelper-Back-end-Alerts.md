<!-- meta tags details, will be assigned to meta tags inside header by js -->
<div id="meta-info">
<details><summary>meta info</summary>

> * Title: <i id="md-title">AlertTagHelper - Backend Alerts</i>
> * Keywords: <i id="md-keywords">asp.net-core, taghelpers, alerts, backend</i>
> * Description: <i id="md-description">Create bootstrap alerts from backend with LazZiya.TagHelpers.</i>
> * Author: <i id="md-author">Ziya Mollamahmut</i>
> * Date: <i id="md-date">27-Nov-2021</i>
> * Image: <i id="md-image">https://github.com/LazZiya/Docs/raw/master/LazZiya.TagHelpers/v6.0/images/lazziya-tagheleprs-logo.png</i>
> * Image-alt: <i id="md-image-alt">LazZiya.TagHelpers Logo</i>
> * Version: <i id="md-version">v6.0</i>

</details>
</div>

# AlertTagHelper - Backend Alerts

By [Ziya Mollamahmut](https://github.com/LazZiya)

* Install package
````
PM > Install-Package LazZiya.TagHelpers
````

* Add to _VÝewImports.cshtml:
````html
@addTagHelper *, LazZiya.TagHelpers
````

### TempData Extensions
In the backend add reference to `LazZiya.TagHelpers.Alerts` namespace, then use the alert extensions of `TempData` to send alerts from the backend to the UI.

````cs
using LazZiya.TagHelpers.Alerts;

public IndexModel : PageModel
{
    public void OnGet()
    {
        TempData.Success("A success message from the backend");
    }
}
````

On the front end, just add the alert tag where you want to show it:
````html
<alert></alert>
````

The alert tag will not render if there is no alerts in the `TempData`. Backend alerts will be styled with reference to their types (primary, success, warning, ...etc.). Once the alert is displayed it will be removed from the `TempData` and will not render in the next request.

### Attributes
All [front end alerts][1] attributes can be used from the backend as well. Additionally, it is possible to send multiple alerts from the backend, The `<alert></alert>` html tag will render all of them in order.  

Below two alert are sent from the backend:
````cs
TempData.Success("This is success alert message from c# backend!");
TempData.Warning("This is a warning alert message", "Alert Header", false);
````

### Slide alerts
When sending multiple alerts from the backend, you can group them in a slider in the fromt end.
````html
<alert slide-alerts="true"></alert>
````

### Alert Icons
Optional, show icons in the alerts
````html
<alert show-icons="true"></alert>
````


### Bootstrap5.x and .net6 support
If you are using bootstrap5.0 or .net6.0 you can use `render-mode` to specify `Bootstrap5`
````html
<alert render-mode="Bootstrap5"></alert>
````

By default the icons source is `FontAwesome`, other sources: `Bootstrap` and `Bootstrap5`.

### All backend alerts
````cs
TempData.Primary
TempData.Secondary
TempData.Success
TempData.Info
TempData.Warning
TempData.Danger
TempData.Light
TempData.Dark
````

[1]:Alerts-TagHelper-front-end-Alerts.md
