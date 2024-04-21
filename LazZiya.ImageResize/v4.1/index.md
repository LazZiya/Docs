<!-- meta tags details, will be assigned to meta tags inside header by js -->
<div id="meta-info">
<details><summary>meta info</summary>

> * Title: <i id="md-title">LazZiya.ImageResize</i>
> * Keywords: <i id="md-keywords">asp.net-core, image, resize, crop, scale, rotate, flip, text watermark, animated, gif</i>
> * Description: <i id="md-description">Image resizing tool for .Net applications to resize images and add text/image watermark, Supports most common image types including animated gif.</i>
> * Author: <i id="md-author">Ziya Mollamahmut</i>
> * Date: <i id="md-date">02-Aug-2021</i>
> * Image: <i id="md-image">https://github.com/LazZiya/Docs/raw/master/LazZiya.ImageResize/v4.1/images/lazziya-imageresize-logo.png</i>
> * Image-alt: <i id="md-image-alt">LazZiya.ImageResize Logo</i>
> * Version: <i id="md-version">v4.1</i>

</details>
</div>

# LazZiya.ImageResize

By [Ziya Mollamahmut](https://github.com/LazZiya)

## What is it?
Image resizing tool for .Net applications to resize images and add text/image watermark, Supports most common image types including animated images as gif.

## Contents
- Install
- Basic Usage
- [Image Resizing Methods][2]
- [Image Watermark][3]
- [Text Watermark][4]
- [Image Frame][9]
- [Image Mask][10]
- [Rotate Flip Image][11]
- [Animated Images][5]
- [Animated Text Watermark][6]
- [Animated Image Watermark][7]
- [Conditional Methods][8]

## Install :

Install via nuget package manager:
````
Install-Package LazZiya.ImageResize
````

## Basic Usage
````csharp
using System.Drawing;
using LazZiya.ImageResize;

using(var img = Image.FromFile("wwwroot/images/image-file.jpg"))
{
    img.ScaleByWidth(600)
       .AddTextWatermark("https://docs.ziyad.info")
       .SaveAs("wwwroot/images/resized-image.jpg");
}
````

## Supported OS
`LazZiya.ImageResize` depends on `System.Drawing.Common`, so OS compatibility with the latter may affect the project compatibility.

- Windows: all .net versions.
- Linux: all .net versions prior to .net6 (see [breaking change announcement](https://learn.microsoft.com/en-us/dotnet/core/compatibility/core-libraries/6.0/system-drawing-common-windows-only))

### Notice for Linux Users
This package depends on `System.Drawing.Common` which is a cross platform GDI+ graphic processing package, and in order for it to work on linux/ubuntu systems install below libraries:

````
sudo apt install libc6-dev 
sudo apt install libgdiplus
````

### Live demos (not covering v4.0 yet):
http://demo.ziyad.info/en/

### Disclaimer :
Parts of the animated gif support depends on a customized version of the code provided by [gOODiDEA.NET](https://www.codeproject.com/Articles/11505/NGif-Animated-GIF-Encoder-for-NET) in CodeProject.com.


[2]:image-resizing-methods.md
[3]:image-watermark.md
[4]:text-watermark.md
[5]:animated-image.md
[6]:animated-text-watermark.md
[7]:animated-image-watermark.md
[8]:conditional-methods.md
[9]:image-frame.md
[10]:image-mask.md
[11]:image-rotate-flip.md
