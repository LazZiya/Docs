<!-- meta tags details, will be assigned to meta tags inside header by js -->
<div id="meta-info">
<details><summary>meta info</summary>

> * Title: <i id="md-title">LazZiya.ImageResize - Add Image Watermark</i>
> * Keywords: <i id="md-keywords">asp.net-core, image, resize, crop, scale, text watermark, animated, gif</i>
> * Description: <i id="md-description">Image resizing tool for .Net applications to resize images and add text/image watermark, Supports most common image types including animated gif.</i>
> * Author: <i id="md-author">Ziya Mollamahmut</i>
> * Date: <i id="md-date">10-Feb-2021</i>
> * Image: <i id="md-image">https://github.com/LazZiya/Docs/raw/master/LazZiya.ImageResize/v3.0/images/lazziya-imageresize-logo.png</i>
> * Image-alt: <i id="md-image-alt">LazZiya.ImageResize Logo</i>
> * Version: <i id="md-version">v3.0</i>

</details>
</div>

# Add Image Watermark

By [Ziya Mollamahmut](https://github.com/LazZiya)

Easily add an image watermark, change its location and opacity.
````csharp
using(var img = Image.FromFile("wwwroot/images/my-image.jpg"))
{
    img.AddImageWatermark("wwwroot/images/logo-watermark.png")
       .SaveAs("wwwroot/images/new-image.jpg");
}
````

- Watermark image parameter can be a string or an `Image` file.
- `AddImageWatermark` can be overloaded with an additional optional parameter: [`ImageWatermarkOptions`][1]

````csharp
using(var img = Image.FromFile("wwwroot/images/my-image.jpg"))
{
    var wmOps = new ImageWatermarkOptions
                {
                    Location = TargetSpot.BottomRight,
                    Margin = 15 // distance from border
                    Opacity = 35
                }

    img.AddImageWatermark("wwwroot/images/logo-watermark.png", wmOps)
       .SaveAs("wwwroot/images/new-image.jpg");
}
````

- All methods can be combined with resize methods:
````csharp
using(var img = Image.FromFile("wwwroot/images/my-image.jpg"))
{
    img.ScaleByWidth(400)
       .AddImageWatermark("wwwroot/images/logo-watermark.png")
       .SaveAs("wwwroot/images/new-image.jpg");
}
````
## Live demos:
http://demo.ziyad.info/en/

[1]:https://github.com/LazZiya/ImageResize/blob/master/LazZiya.ImageResize/ImageWatermarkOptions.cs