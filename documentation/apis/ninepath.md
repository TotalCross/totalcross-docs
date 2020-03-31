# Ninepath

## Overview

NinePatch is a class that allows you to create nine custom patches that will be sized the way you define them. It draws an extensible image so you can resize it without losing the edges.

The amount of designs that can be created using this technique is virtually endless, so much so that Android also uses this tool.

To adjust the images and create the guides, keeping in mind that the corners will stay fixed, you need the help of a designer or someone with knowledge in image editing tools as illustrator.

But there are also sites that help to perform this work in a [simpler way as this site](https://romannurik.github.io/AndroidAssetStudio/nine-patches.html#source.type=image&sourceDensity=480&name=multibutton). In it, just upload the desired image and then adjust the guides \(always keeping in mind that the corners are fixed\). That done, just download the .zip file containing the guides!

## Methods

| Type | Name | Description |
| :--- | :--- | :--- |
| **NinePatch** | getInstance\( \) | Returns the instance of the NinePatch |
| **Parts** | load\(Image\) | Return the 9 ninepatch parts from a Image with the guides |
| **Parts** | load\(Image original, int scalableAreaStartWidth, int scalableAreaEndWidth, int scalableAreaStartHeight, int scalableAreaEndHeight\) | Returns the 9 ninepatch parts of the image without the guides but with the values of the points that will cut the image |
| **Parts** | load\(Image original, int scalableAreaWidth, int scalableAreaHeight\) | Returns the 9 parts of the ninepatch of a image without the guides but with the values that are going to be used for the borders rectangles, that are the respective width and height. All border rectangles are equals in this case. |
| **Image** | getNormalInstance\(Parts p, int width, int height, int color, boolean rotate\) | Return the result image built from the given width and height; If the given color is different from -1, it will apply the rgb colors in every pixel from the image. If the given boolean is true, the image will be rotated 180º. |
| **Image** | getNormalInstance\(int type, int width, int height, int color, boolean rotate\) | Return the result image from one of Totalcross standard ninepatchs. If the given color is different from -1, it will apply the rgb colors in every pixel from the image. If the given boolean is true, the image will be rotated 180º. |
| **Image** | getPressedInstance\(Image img, int backColor, int pressColor\) | Return the given image with a pressed effect from the given color |
| **void** | tryDrawImage\(Graphics g, Image npback, int x, int y\) | Draws on the given Graphics the given image on the x and y coordinates. |



