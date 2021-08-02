<!-- meta tags details, will be assigned to meta tags inside header by js -->
<div id="meta-info">
<details><summary>meta info</summary>

> * Title: <i id="md-title">LazZiya.ImageResize - Add Animated Image Watermark</i>
> * Keywords: <i id="md-keywords">asp.net-core, image, resize, crop, scale, text watermark, animated, gif</i>
> * Description: <i id="md-description">Image resizing tool for .Net applications to resize images and add text/image watermark, Supports most common image types including animated gif.</i>
> * Author: <i id="md-author">Ziya Mollamahmut</i>
> * Date: <i id="md-date">22-Feb-2021</i>
> * Image: <i id="md-image">https://github.com/LazZiya/Docs/raw/master/LazZiya.ImageResize/v4.1/images/lazziya-imageresize-logo.png</i>
> * Image-alt: <i id="md-image-alt">LazZiya.ImageResize Logo</i>
> * Version: <i id="md-version">v4.1</i>

</details>
</div>

# Add Animated Image Watermark

By [Ziya Mollamahmut](https://github.com/LazZiya)

Easily add an animated image watermark, change its location and opacity.

> Animated image watermark can be placed over a static image only

````csharp
// Add animated image watermark over a static image
using(var img = Image.FromFile("wwwroot/images/my-image.jpg"))
{
    img.AddAnimatedImageWatermark("wwwroot/images/logo-watermark.gif")
       .SaveAs("wwwroot/images/new-image.gif"); // Make sure to save as gif
}
````

![Static Image - Animated Watermark](https://github.com/LazZiya/Docs/raw/master/LazZiya.ImageResize/v4.1/images/static-image-animated-image-watermark.gif)

## Live demos:
http://demo.ziyad.info/en/

[1]:https://github.com/LazZiya/ImageResize/blob/master/LazZiya.ImageResize/ImageWatermarkOptions.cs