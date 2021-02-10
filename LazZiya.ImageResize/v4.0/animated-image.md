<!-- meta tags details, will be assigned to meta tags inside header by js -->
<div id="meta-info">
<details><summary>meta info</summary>

> * Title: <i id="md-title">LazZiya.ImageResize - Animated Gif</i>
> * Keywords: <i id="md-keywords">asp.net-core, image, resize, crop, scale, text watermark, animated, gif</i>
> * Description: <i id="md-description">Image resizing tool for .Net applications to resize images and add text/image watermark, Supports most common image types including animated gif.</i>
> * Author: <i id="md-author">Ziya Mollamahmut</i>
> * Date: <i id="md-date">10-Feb-2021</i>
> * Image: <i id="md-image">https://github.com/LazZiya/Docs/raw/master/LazZiya.ImageResize/v4.0/images/lazziya-imageresize-logo.png</i>
> * Image-alt: <i id="md-image-alt">LazZiya.ImageResize Logo</i>
> * Version: <i id="md-version">v4.0</i>

</details>
</div>

# Animated Images (gif)

By [Ziya Mollamahmut](https://github.com/LazZiya)

All resize methods including adding text/image watermarks are valid for animated images as well. The only change is to use [`AnimatedImage`][2] instead of `Image` as below:

````csharp
using LazZiya.ImageResize.Animated;

using(var img = AnimatedImage.FromFile("wwwroot/images/my-animation.gif"))
{
    img.AddTextWatermark("https://docs.ziyad.info")
       .SaveAs("wwwroot/images/new-animation.gif");
}
````

## Live demos:
http://demo.ziyad.info/en/

[1]:https://github.com/LazZiya/ImageResize/blob/master/LazZiya.ImageResize/TextWatermarkOptions.cs
[2]:https://github.com/LazZiya/ImageResize/blob/vNext/LazZiya.ImageResize/Animated/AnimatedImage.cs