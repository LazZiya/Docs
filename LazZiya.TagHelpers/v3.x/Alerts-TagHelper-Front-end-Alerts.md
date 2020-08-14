<!-- meta tags details, will be assigned to meta tags inside header by js -->
<div id="meta-info">
<details><summary>meta info</summary>

> * Title: <i id="md-title">AlertTagHelper - Frontend Alerts</i>
> * Keywords: <i id="md-keywords">asp.net-core, taghelpers, alerts, backend</i>
> * Description: <i id="md-description">Create bootstrap alerts from frontend with LazZiya.TagHelpers.</i>
> * Author: <i id="md-author">Ziya Mollamahmut</i>
> * Date: <i id="md-date">02-Oct-2019</i>
> * Image: <i id="md-image">https://github.com/LazZiya/Docs/raw/master/LazZiya.TagHelpers/v3.0/images/lazziya-tagheleprs-logo.png</i>
> * Image-alt: <i id="md-image-alt">LazZiya.TagHelpers Logo</i>
> * Version: <i id="md-version">v3.0</i>

</details>
</div>

# AlertTagHelper - Frontend Alerts

By [Ziya Mollamahmut](https://github.com/LazZiya)

### Setup
Install nuget package
````
Install-Package LazZiya.TagHelpers
````

Add taghelpers in __ViewImports.cshtml_
````razor
@addTagHelper *, LazZiya.TagHelpers
````
### Basic usage
Create bootstrap 4.x themed alerts with simple html tag.

````html
<alert-primary>
 This is a primary alert from the front end.
</alert-primary>
````

![Primary alert front end](https://github.com/LazZiya/Docs/raw/master/LazZiya.TagHelpers/v3.0/images/alert-taghelper-primary-front-end.PNG)

### Un-dismissable alert
Use `dismissable` attribute to remove the alert closing button. 
````html
<alert-info dismissable="false">
 This an alert that can't be dismissed!
</alert-info>
```` 

![Alert no dismiss](https://github.com/LazZiya/Docs/raw/master/LazZiya.TagHelpers/v3.0/images/alert-taghelper-no-dismiss.PNG)

### Alert header
Add alert header using `alert-heading` attribute
````html
<alert-warning alert-heading="Warning!">
 This is a warning alert with header.
</alert-warning>
````

![Alert with header](https://github.com/LazZiya/Docs/raw/master/LazZiya.TagHelpers/v3.0/images/alert-taghelper-with-header.PNG)

### Html content
It is possible to use html content inside the alert body.
````html
<alert-danger>
 <h3>Danger alert</h3>
 <p>This is a danger alert with html content.</p>
 <hr />
 <p class="text-dark">Use your creativity to style the content as you wish.</p>
</alert-danger>
````

![Alert with HTML content](https://github.com/LazZiya/Docs/raw/master/LazZiya.TagHelpers/v3.0/images/alert-taghelper-html-content.PNG)

### All alerts
````html
<alert-primary>
<alert-secondary>
<alert-success>
<alert-info>
<alert-warning>
<alert-danger>
<alert-light>
<alert-dark>
````

![All alerts](https://github.com/LazZiya/Docs/raw/master/LazZiya.TagHelpers/v3.0/images/alert-taghelper-all-front-end.PNG)

See samples in the [demo page][1].

[1]:http://demo.ziyad.info/en/alerts