## Feature
This API is used to provide real-time text watermarking in Tencent Cloud CI. Currently, images smaller than 20 MB in size and smaller than 9,999 pixels in length and width are supported.

## API Form

```http
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

> Please ignore the preceding spaces and line breaks.


## Parameter Description

**Operation name**: watermark. The number 2 indicates the watermark type is text watermark.

| Parameter | Description |
| ------------ | ------------------------------------------------------------ |
| download_url | URL that is used to access a file. The URL form is `<BucketName-APPID>.cos.<picture region>.<domain>.com/<picture name>`, <br>for example, `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg`. |
| /text/ | Watermark content, which is encoded with Base64 that is safe to the URL. |
| /font/ | Watermark font, which is [encoded with Base64 that is safe to the URL](https://intl.cloud.tencent.com/document/product/1045/33430#.E4.BB.80.E4.B9.88.E6.98.AF-url-.E5.AE.89.E5.85.A8.E7.9A.84-base64-.E7.BC.96.E7.A0.81.EF.BC.9F). The default value is tahoma.ttf. |
| /fontsize/ | Watermark text fontsize in pounds. The default value is 13. |
| /fill/ | Watermark font color, which must be set to the hexadecimal RGB format (such as #FF0000). The default value is gray. For more information, see [RGB Code Table](https://www.rapidtables.com/web/color/RGB_Color.html). The value must be [encoded with Base64 that is safe to the URL](https://intl.cloud.tencent.com/document/product/1045/33430#.E4.BB.80.E4.B9.88.E6.98.AF-url-.E5.AE.89.E5.85.A8.E7.9A.84-base64-.E7.BC.96.E7.A0.81.EF.BC.9F). The default value is #3D3D3D. |
| /dissolve/ | Text transparency. Value range: 1 - 100. The default value is 90, which indicates total non-transparency. |
| /gravity/ | Text watermark position, which is a 3x3 grid position ([See the 3x3 grid position diagram](#1)). The default value is SouthEast. |
| /dx/ | Horizontal margin in pixels. The default value is 0. |
| /dy/ | Vertical margin in pixels. The default value is 0. |
| /batch/ | Tiled watermarking, which can tile the text watermark to the entire image. If you set batch to 1, tiled watermarking is enabled. |
| /degree/ | Rotation angle of the text watermark. Value range: 0 - 360. The default value is 0. |

<span id="1"></span>
## 3x3 Grid Position Diagram

A 3x3 grid position diagram provides position reference for multiple image operations. Red dots show the origin points of each region. After you use the gravity parameter to select a region, displacement must be based on the corresponding origin point.
![](https://main.qcloudimg.com/raw/53a143451229b4fbdd74935afe3832d5.png)

>
- When the gravity parameter is set to center, the dx and dy parameters are invalid.
- When the gravity parameter is set to north or south, the dx parameter is invalid, and the watermark is centered horizontally.
- When the gravity parameter is set to west or east, the dy parameter is invalid, and the watermark is centered vertically.

## Example
This example shows you how to **add a text watermark**.

```
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?watermark/2/text/6IW-6K6v5LqRwrfkuIfosaHkvJjlm74/fill/IzNEM0QzRA/fontsize/20/dissolve/50/gravity/northeast/dx/20/dy/20/batch/1/degree/45
```

After the text watermark is added, the effect is as follows:
![](https://main.qcloudimg.com/raw/7e72e46d082e36dfc5ec319e0ccd1664.jpg)

