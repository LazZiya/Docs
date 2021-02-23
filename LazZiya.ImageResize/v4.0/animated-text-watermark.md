<!-- meta tags details, will be assigned to meta tags inside header by js -->
<div id="meta-info">
<details><summary>meta info</summary>

> * Title: <i id="md-title">LazZiya.ImageResize - Add Animated Text Watermark</i>
> * Keywords: <i id="md-keywords">asp.net-core, image, resize, crop, scale, text watermark, animated, gif</i>
> * Description: <i id="md-description">Image resizing tool for .Net applications to resize images and add text/image watermark, Supports most common image types including animated gif.</i>
> * Author: <i id="md-author">Ziya Mollamahmut</i>
> * Date: <i id="md-date">22-Feb-2021</i>
> * Image: <i id="md-image">https://github.com/LazZiya/Docs/raw/master/LazZiya.ImageResize/v4.0/images/lazziya-imageresize-logo.png</i>
> * Image-alt: <i id="md-image-alt">LazZiya.ImageResize Logo</i>
> * Version: <i id="md-version">v4.0</i>

</details>
</div>

# Add Animated Text Watermark

By [Ziya Mollamahmut](https://github.com/LazZiya)

Easily add an animated text watermark, change its location, opacity, font size, color, ...etc.

Animated text watermarks can be added to static images (jpg, png) or animated images (gif). When adding an animated text watermark to a static image it must be saved as ".gif".

### - Animated Text Watermark Over Static Image
````csharp
// Add animated text watermark over a static image
using(var img = Image.FromString("wwwroot/images/my-image.jpg"))
{
    var twmOps = new TextWatermarkOptions 
    {
        FontSize = 15,
        Location = TargetSpot.BottomRight 
    };

    img.ScaleAndCrop(400, 250)
        .AddAnimatedTextWatermark("LazZiya.ImageResize....", twmOps)
        .SaveAs("wwwroot/upload/new-image.gif", 100); // Make sure to save as gif
}
````

![Static Image - Animated Text Watermark](https://github.com/LazZiya/Docs/raw/master/LazZiya.ImageResize/v4.0/images/static-image-animated-text-watermark.gif)


### - Animated Text Watermark Over Animated Image
Just like adding the animated text over a static image, use `AnimatedImage` instead.
````csharp
// Add animated text watermark over an animated image
using(var img = AnimatedImage.FromFile("wwwroot/images/my-image.gif"))
{
    img.AddAnimatedTextWatermark("LazZiya.ImageResize...")
       .SaveAs("wwwroot/upload/new-image.gif", 50); // Make sure to save as gif
}
````
![Animated Image - Animated Text Watermark](https://github.com/LazZiya/Docs/raw/master/LazZiya.ImageResize/v4.0/images/animated-image-animated-text-watermark.gif)

> <small>Animated image obtained from [Giphy](https://giphy.com/gifs/GoTurkey-turkey-tourism-goturkey-Y2z4kPLUEDddnAjXwh)</small>

## Live demos:
http://demo.ziyad.info/en/

[1]:https://github.com/LazZiya/ImageResize/blob/master/LazZiya.ImageResize/TextWatermarkOptions.cs