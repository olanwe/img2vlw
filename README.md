# img2vlw
Simple image to VLW converter for e-ink displays being used with [OpenEPaperLink](https://openepaperlink.de/).

Everything is included in the [img2vlw.html](img2vlw.html) itself. Download it for offline usage or [run it online](http://htmlpreview.github.io/?https://github.com/olanwe/img2vlw/blob/main/img2vlw.html)!

## Usage
It is suggested to prepare the image file for conversion first (e.g. by removing unsupported colors, dithering, resizing and cropping the image before feeding it into the converter).

1. Open an image file by clicking on the browse button.
2. Select the third color of the display (either red, yellow or none).
3. Enter a width and/or height of the target image or leave both fields empty to use the original size. If you enter either width or height, the image will be scaled proportionally to that size. Entering both values will resize the image to the given dimensions.
4. Change the luminance offset value as required. Sometimes it is necessary to change that value to get better results with color separation.
5. Click the download-button to download the VLW-file. It will be saved to the download directory.
6. Upload the VLW-file to the "fonts"-directory on your OpenEPaperLink access point. (Open ``http://<AP-IP-address>/edit`` to access the file browser of the access point.)

To display the image in JSON, create a text using the generated font and write character "0" for the black image. If you have selected a third color then write character "1" on top of the first text (at the same position).

Example (for a three-color image):
```
[
{ "text": [5, 5, "0", "image.vlw", 1] },
{ "text": [5, 5, "1", "image.vlw", 2] }
]
```
