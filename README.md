# img2vlw

Simple image to VLW converter for e-ink displays being used with [OpenEPaperLink](https://openepaperlink.de/).

Everything is included in the [img2vlw.html](img2vlw.html) itself. Download it for offline usage or [run it online](http://htmlpreview.github.io/?https://github.com/olanwe/img2vlw/blob/main/img2vlw.html)!  

*New:* img2vlw will crop the color bitmaps separately to the actually used area to save space. (For example, if you have a large black, white, and red image with only a small red dot on it, img2vlw will only save the area of the dot and store its coordinates in the glyph definition. The displayed image itself, however, will not appear to be cropped at all.)

## Usage

It is suggested to prepare the image file for conversion first (e.g. by removing unsupported colors, dithering, resizing and cropping the image before feeding it into the converter).

1. Open an image file by clicking on the browse button.
2. Select the third color of the display (either red, yellow or none).
3. Enter a width and/or height of the target image or leave both fields empty to use the original size. If you enter either width or height, the image will be scaled proportionally to that size. Entering both values will resize the image to the given dimensions.
4. Change the luminance offset value as required. Sometimes it is necessary to change that value to get better results with color separation.
5. If you are creating a multi-color image and need to place it at x-position 0 (which should be avoided - see [Known issues](#known-issues) below), then enable the "x-pos 0 patch".
6. Click the download-button to download the VLW-file. It will be saved to the download directory.
7. Upload the VLW-file to the "fonts"-directory on your OpenEPaperLink access point. (Open ``http://<AP-IP-address>/edit`` to access the file browser of the access point.)

To display the image in JSON, create a text using the generated font and write character "0" for the black image. If you have selected a third color then write character "1" on top of the first text (at the same position).

Example (for a three-color image):

```json
[
{ "text": [5, 5, "0", "image.vlw", 1] },
{ "text": [5, 5, "1", "image.vlw", 2] }
]
```

## Known issues

If the image is placed on the far left of the display (x-pos = 0), the font renderer will remove all white space on the left side of the character. This can break multicolor images because both color planes are shifted to the left individually (see [Issue #1](https://github.com/olanwe/img2vlw/issues/1)).
To avoid this situation, you can simply position the image at x ≥ 1 instead of x = 0. If this is not possible, then the "x-pos 0 patch" must be activated. This will create an additional pixel on the shifted color plane so that both color planes start at the same x-position. In this case it is important to print the colors in the order given by the converter. For example, if the patch is applied to the color plane, it must be printed first. In this case, the patched pixel will be overwritten by the pixel on the other color plane, so it will not be visible. Keep in mind that the whitespace removal will still shift the image to the left, removing all blank space, and that the patch will result in larger VLW-files.
