## Description
The **watermark** API is used to process text watermarks in real time. Currently, this API is applicable to images with a size no greater than 20 MB and a length and width both less than 9,999 pixels.

## API Format

```
download_url?watermark/2/text/<encodedText>
                        /font/<encodedFont>
                        /fontsize/<fontSize>
                        /fill/<encodedColor>
                        /dissolve/<dissolve>
                        /gravity/<gravity>
                        /dx/<dx>
                        /dy/<dy>
                        /batch/<type>
                        /degree/<degree>
```

> Ignore the preceding spaces and line breaks.




### Parameter description

**Operation**: watermark. 2 indicates that the watermark is a text watermark.

| Parameter | Description |
| ------------ | ------------------------------------------------------------ |
| download_url | The file access URL in the format of `<BucketName-APPID>.<picture region>.<domain>.com/<picture name>`, <br>for example, `examplebucket-1250000000.picsh.myqcloud.com/picture.jpeg`. |
| /text/ | The content of the watermark, which must be URL-safe Base64 encoded. |
| /font/ | The font of the watermark, which must be URL-safe Base64 encoded. The default value is tahoma.ttf. |
| /fontsize/ | The font size of the watermark text in pt. The default value is 13. |
| /fill/ | The font color. The default value is grey. The value must be in hexadecimal RGB format, for example, #FF0000. For more information, see the [RGB Color Codes Chart](https://www.rapidtables.com/web/color/RGB_Color.html). The value of this parameter must be URL-safe Base64 encoded. The default value is #3D3D3D. |
| /dissolve/ | The text transparency value. Value range: 1-100. The default value is 100 (completely opaque). |
| /gravity/ | The position of the text watermark in the Sudoku orientation chart (see the [Sudoku Orientation Chart](#1)). The default value is SouthEast. |
| /dx/ | The horizontal margin in pixels. The default value is 0. |
| /dy/ | The vertical margin in pixels. The default value is 0. |
| /batch/ | The watermark tiling feature. This feature enables a text watermark to be tiled across an entire image. When the value of this parameter is set to 1, the watermark tiling feature is enabled. |
| /degree/ | The rotation degree of the text watermark. Value range: 0-360. The default value is 0. |

<span id="1"></span>
### Sudoku orientation chart

A Sudoku orientation chart can provide a position reference for various operations performed on an image. The red dot indicates the origin of each region (after each region is selected by using the `gravity` parameter, the displacement operation is performed by using the corresponding far point as the reference.)
![](https://main.qcloudimg.com/raw/53a143451229b4fbdd74935afe3832d5.png)


>
- When `gravity` is set to center, the `dx` and `dy` parameters are invalid.
- When `gravity` is set to north or south, the `dx` parameter is invalid (in which case the watermark is centered horizontally).
- When `gravity` is set to west or east, the `dy` parameter is invalid (in which case the watermark is centered vertically).

## Example
**Adding a text watermark**

```
http://examples-1251000004.picsh.myqcloud.com/sample.jpeg?watermark/2/text/6IW-6K6v5LqRwrfkuIfosaHkvJjlm74/fill/IzNEM0QzRA/fontsize/20/dissolve/50/gravity/northeast/dx/20/dy/20/batch/1/degree/45
```

The effect of adding the text watermark is as follows:
![](https://main.qcloudimg.com/raw/7e72e46d082e36dfc5ec319e0ccd1664.jpg)
