<!-- meta tags details, will be assigned to meta tags inside header by js -->
<div id="meta-info">
<details><summary>meta info</summary>

> * Title: <i id="md-title">LazZiya.ImageResize - Add Image Watermark</i>
> * Keywords: <i id="md-keywords">asp.net-core, image, resize, crop, scale, text watermark, animated, gif</i>
> * Description: <i id="md-description">Image resizing tool for .Net applications to resize images and add text/image watermark, Supports most common image types including animated gif.</i>
> * Author: <i id="md-author">Ziya Mollamahmut</i>
> * Date: <i id="md-date">10-Feb-2021</i>
> * Image: <i id="md-image">https://github.com/LazZiya/Docs/raw/master/LazZiya.ImageResize/v4.0/images/lazziya-imageresize-logo.png</i>
> * Image-alt: <i id="md-image-alt">LazZiya.ImageResize Logo</i>
> * Version: <i id="md-version">v4.0</i>

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
- All methods can be combined with resize methods:
````csharp
using (var img = Image.FromStream(stream))
{
    var imOps = new ImageWatermarkOptions 
    {
        Opacity = 35,
        Location = TargetSpot.Center
    };

    img.ScaleAndCrop(600, 300)
        .AddImageWatermark("wwwroot/images/icon.png", imOps)
        .SaveAs("wwwroot/upload/new-image.jpg");
}
````

![Static Image - Static Image Watermark](https://github.com/LazZiya/Docs/raw/master/LazZiya.ImageResize/v4.0/images/static-image-static-image-watermark.jpg)

#### See also [Animated Image Watermark](animated-image-watermark.md)

[1]:https://github.com/LazZiya/ImageResize/blob/master/LazZiya.ImageResize/ImageWatermarkOptions.cs