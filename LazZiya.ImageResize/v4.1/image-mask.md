<!-- meta tags details, will be assigned to meta tags inside header by js -->
<div id="meta-info">
<details><summary>meta info</summary>

> * Title: <i id="md-title">LazZiya.ImageResize - Image Mask</i>
> * Keywords: <i id="md-keywords">asp.net-core, image, resize, crop, scale, text watermark, animated, gif, conditional, frame, border, fill, mask</i>
> * Description: <i id="md-description">Image resizing tool for .Net applications to resize images and add text/image watermark, Supports most common image types including animated gif.</i>
> * Author: <i id="md-author">Ziya Mollamahmut</i>
> * Date: <i id="md-date">11-Mar-2021</i>
> * Image: <i id="md-image">https://github.com/LazZiya/Docs/raw/master/LazZiya.ImageResize/v4.1/images/lazziya-imageresize-logo.png</i>
> * Image-alt: <i id="md-image-alt">LazZiya.ImageResize Logo</i>
> * Version: <i id="md-version">v4.1</i>

</details>
</div>

By [Ziya Mollamahmut](https://github.com/LazZiya)

# Image Mask

Simply apply a mask over the image.

````csharp
// make ellipse frame
using(var img = Image.FromFile("my-image-file.jpg")
{
    img.Mask(new Rectangle(0, 0, 300, 300), ImageFrameShape.Ellipse)
       .SaveAs("wwwroot/upload/new-image.png");
}
````

Original image: 

![Original image](https://github.com/LazZiya/Docs/raw/master/LazZiya.ImageResize/v4.1/images/sample-flower.png)

Result:

![Resized with frame](https://github.com/LazZiya/Docs/raw/master/LazZiya.ImageResize/v4.1/images/masked-flower.png)

All methods are available with the conditional `If` variation.