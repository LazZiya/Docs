<!-- meta tags details, will be assigned to meta tags inside header by js -->
<div id="meta-info">
<details><summary>meta info</summary>

> * Title: <i id="md-title">LazZiya.ImageResize - Resizing Methods</i>
> * Keywords: <i id="md-keywords">asp.net-core, image, resize, crop, scale, text watermark, animated, gif</i>
> * Description: <i id="md-description">Image resizing tool for .Net applications to resize images and add text/image watermark, Supports most common image types including animated gif.</i>
> * Author: <i id="md-author">Ziya Mollamahmut</i>
> * Date: <i id="md-date">10-Feb-2021</i>
> * Image: <i id="md-image">https://github.com/LazZiya/Docs/raw/master/LazZiya.ImageResize/v4.1/images/lazziya-imageresize-logo.png</i>
> * Image-alt: <i id="md-image-alt">LazZiya.ImageResize Logo</i>
> * Version: <i id="md-version">v4.1</i>

</details>
</div>

# Image Resizing Methods

By [Ziya Mollamahmut](https://github.com/LazZiya)

**- Scale :**
Auto scales image by width or height till both borders are fitted, and keeps aspect ratio same as the original image
````csharp 
using(var img = Image.FromFile("my-image.jpg"))
{
    img.Scale(800, 600)
       .SaveAs("resized-image.jpg");
}
````

**- Scale by width :**
Scales image by provided width value, auto adjusts new height according to aspect ratio.
````csharp
img.ScaleByWidth(800);
````

**- Scale by height :**
Scales image by provided height value, auto adjusts new width according to aspect ratio.
````csharp
img.ScaleByHeight(600);
````

**- Scale and crop :**
Scalesthe image to fit new width or new height (which fits first), then crops out the rest of the image.
````csharp
img.ScaleAndCrop(800, 600);

// or
img.ScaleAndCrop(800, 600, TargetSpot.Center);
````

**- Crop :**
Directly crop a specified spot of the image, without scaling.
````csharp 
img.Crop(800, 600);

// or
img.Crop(800, 600, TargetSpot.Center);
````


- All resizing methods will return a `System.Drawing.Image` file that can be saved in any supported image format (JPG, PNG, etc.)
- All methods can be overloaded with an optional parameter: [`GraphicOptions`][1].
- [`TargtSpot`][2] can be used to quickly select a predefined region of the image.

## Live demos:
http://demo.ziyad.info/en/

[1]:https://github.com/LazZiya/ImageResize/blob/master/LazZiya.ImageResize/GraphicOptions.cs
[2]:https://github.com/LazZiya/ImageResize/blob/master/LazZiya.ImageResize/TargetSpot.cs