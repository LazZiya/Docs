<!-- meta tags details, will be assigned to meta tags inside header by js -->
<div id="meta-info">
<details><summary>meta info</summary>

> * Title: <i id="md-title">LazZiya.ImageResize - Add Text Watermark</i>
> * Keywords: <i id="md-keywords">asp.net-core, image, resize, crop, scale, text watermark, animated, gif</i>
> * Description: <i id="md-description">Image resizing tool for .Net applications to resize images and add text/image watermark, Supports most common image types including animated gif.</i>
> * Author: <i id="md-author">Ziya Mollamahmut</i>
> * Date: <i id="md-date">10-Feb-2021</i>
> * Image: <i id="md-image">https://github.com/LazZiya/Docs/raw/master/LazZiya.ImageResize/v4.0/images/lazziya-imageresize-logo.png</i>
> * Image-alt: <i id="md-image-alt">LazZiya.ImageResize Logo</i>
> * Version: <i id="md-version">v4.0</i>

</details>
</div>

# Add Text Watermark

By [Ziya Mollamahmut](https://github.com/LazZiya)

Easily add a text watermark, change its location, opacity, font size, color, ...etc.
````csharp
using(var img = Image.FromFile("wwwroot/images/my-image.jpg"))
{
    img.AddTextWatermark("https://docs.ziyad.info")
       .SaveAs("wwwroot/images/new-image.jpg");
}
````

- `AddTextWatermark` can be overloaded with an additional optional parameter: [`TextWatermarkOptions`][1]

````csharp
using(var img = Image.FromFile("wwwroot/images/my-image.jpg"))
{
    var tmOps = new ImageTextWatermarkOptions
                {
                    Location = TargetSpot.TopLeft,
                    Margin = 15, // distance from border
                    FontSize = 35,
                    FontStyle = FontStyle.Bold,
                    TextColor = Color.FromArgb(255, Color.Whight), // Use alpha channel to change opacity
                    BGColor = Color.FromArgb(100, Color.Red), // set alpha to 0 to remove background
                    OutlineColor = Color.FromArgb(255, Color.Black), // Use alpha channel to change opacity
                    OutlineWidth = 3.5f // draw an outline around the text
                }

    img.AddTextWatermark("https://docs.ziyad.info", tmOps)
       .SaveAs("wwwroot/images/new-image.jpg");
}
````

- All methods can be combined with resize methods:
````csharp
using(var img = Image.FromFile("wwwroot/images/my-image.jpg"))
{
    img.ScaleByWidth(400)
       .AddTextWatermark("https://docs.ziyad.info")
       .SaveAs("wwwroot/images/new-image.jpg");
}
````

## Live demos:
http://demo.ziyad.info/en/

[1]:https://github.com/LazZiya/ImageResize/blob/master/LazZiya.ImageResize/TextWatermarkOptions.cs