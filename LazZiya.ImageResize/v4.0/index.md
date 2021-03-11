<!-- meta tags details, will be assigned to meta tags inside header by js -->
<div id="meta-info">
<details><summary>meta info</summary>

> * Title: <i id="md-title">LazZiya.ImageResize</i>
> * Keywords: <i id="md-keywords">asp.net-core, image, resize, crop, scale, text watermark, animated, gif</i>
> * Description: <i id="md-description">Image resizing tool for .Net applications to resize images and add text/image watermark, Supports most common image types including animated gif.</i>
> * Author: <i id="md-author">Ziya Mollamahmut</i>
> * Date: <i id="md-date">10-Feb-2021</i>
> * Image: <i id="md-image">https://github.com/LazZiya/Docs/raw/master/LazZiya.ImageResize/v4.0/images/lazziya-imageresize-logo.png</i>
> * Image-alt: <i id="md-image-alt">LazZiya.ImageResize Logo</i>
> * Version: <i id="md-version">v4.0</i>

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
- [Animated Images][5]
- [Animated Text Watermark][6]
- [Animated Image Watermark][7]
- [Conditional Methods][8]

## Install :

Install via nuget package manager:
````
Install-Package LazZiya.ImageResize -Pre
````
> v4.0 still in preview mode, so add -Pre to the command to install latest preview version

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

## Live demos:
http://demo.ziyad.info/en/

[2]:image-resizing-methods.md
[3]:image-watermark.md
[4]:text-watermark.md
[5]:animated-image.md
[6]:animated-text-watermark.md
[7]:animated-image-watermark.md
[8]:conditional-methods.md
[9]:image-frame.md
[10]:image-mask.md