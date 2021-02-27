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
- [Image Resizing Methods][1]
- [Image Watermark][2]
- [Text Watermrk][3]
- [Animated Images][4]
- [Animated Text Watermark][5]
- [Animated Image Watermark][6]

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

[1]:image-resizing-methods.md
[2]:image-watermark.md
[3]:text-watermark.md
[4]:animated-image.md
[5]:animated-text-watermark.md
[6]:animated-image-watermark.md