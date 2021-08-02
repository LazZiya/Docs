<!-- meta tags details, will be assigned to meta tags inside header by js -->
<div id="meta-info">
<details><summary>meta info</summary>

> * Title: <i id="md-title">LazZiya.ImageResize - Conditional Methods</i>
> * Keywords: <i id="md-keywords">asp.net-core, image, resize, crop, scale, text watermark, animated, gif, conditional</i>
> * Description: <i id="md-description">Image resizing tool for .Net applications to resize images and add text/image watermark, Supports most common image types including animated gif.</i>
> * Author: <i id="md-author">Ziya Mollamahmut</i>
> * Date: <i id="md-date">09-Mar-2021</i>
> * Image: <i id="md-image">https://github.com/LazZiya/Docs/raw/master/LazZiya.ImageResize/v4.1/images/lazziya-imageresize-logo.png</i>
> * Image-alt: <i id="md-image-alt">LazZiya.ImageResize Logo</i>
> * Version: <i id="md-version">v4.1</i>

</details>
</div>

By [Ziya Mollamahmut](https://github.com/LazZiya)

# Conditional Methods

Just like all methods, with additional condition boolean parameter. If the parameter is true the resize will done, otherwise it will return the same image.

## Why Conditional Methods?
In some cases we may need to resize an image depending on a dynamic parameter in our project. 

#### The old way of doing it:
````csharp
using(var img = Image.FromFile("my-image-file.jpg")
{
    if(doResize == true)
    {
        img.Scale(800, 600)
           .SaveAs("new-image.jpg");
    }
    else
    {
        img.SaveAs("new-image.jpg");
    }
}
````

#### The new way:
````csharp
using(var img = Image.FromFile("my-image-file.jpg")
{
    img.ScaleIf(doResize, 800, 600)
       .SaveAs("new-image.jpg");
}
````

## Chain Methods
Conditional reaize can be applied to all resizing methods, and all can be chained together:
````csharp
// doResize, addTextWM and addImgWM are boolean values
using(var img = Image.FromFile("my-image-file.jpg")
{
    img.ScaleIf(doResize, 800, 600)
       .AddTextWatermarkIf(addTextWM, "https://docs.ziyad.info")
       .AddImageWatermarkIf(addImagWm, "logo.png")
       .SaveAs("new-image.jpg");
}
````

All methods are available with the conditional `If` variation.