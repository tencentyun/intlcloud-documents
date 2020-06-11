## Feature
This API **watermark** from Tencent Cloud CI is used to provide real-time text watermarking in COS. Currently, supported images are smaller than 20 MB in size and smaller than 9,999 pixels in length and width.

>Image processing is a paid service, the fees of which are charged by Cloud Infinite. For detailed billing instructions, see Cloud Infinite’s [Billing and Pricing](https://intl.cloud.tencent.com/document/product/1045/33431).

## API Form

```plaintext
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

>Please ignore the preceding spaces and line breaks.


## Parameter Description

**Operation name**: watermark. The number 2 indicates the watermark type is text watermark.

| Parameter         | Description                                                         |
| ------------ | ------------------------------------------------------------ |
| download_url | URL that is used to access a file. Format: `<BucketName-APPID>.cos.<picture region>.<domain>.com/<picture name>`, <br>for example, `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg`. |
| /text/       | Watermark content, which must be [URL Safe Base64 encoded](https://intl.cloud.tencent.com/document/product/1045/33430)                    |
| /font/       | Watermark font, which must be [URL Safe Base64 encoded](https://intl.cloud.tencent.com/document/product/1045/33430). Default: tahoma.ttf. For the list of watermark fonts, see [Fonts List](https://cloud.tencent.com/document/product/460/19568). |
| /fontsize/ | Watermark text font size in pounds. The default value is 13. |
| /fill/       | Watermark font color, which must be set to the hexadecimal RGB format (such as #FF0000), and URL Safe Base64 encoded. The default value is gray #3D3D3D. For more information, see [RGB Color Codes Chart](https://www.rapidtables.com/web/color/RGB_Color.html). |
| /dissolve/ | Text transparency. Value range: 1 - 100. The default value is 90, which indicates total non-transparency. |
| /gravity/ | Text watermark position, which is shown in a 3 x 3 grid ([See 3 x 3 Positioning Grid](#1)). The default value is SouthEast. |
| /dx/ | Horizontal margin in pixels. The default value is 0. |
| /dy/ | Vertical margin in pixels. The default value is 0. |
| /batch/ | Tiled watermarking, which can tile the text watermark to the entire image. If you set batch to 1, tiled watermarking is enabled. |
| /degree/ | Rotation angle of the text watermark. Value range: 0 - 360. The default value is 0. |

<span id="1"></span>
## 3 x 3 Positioning Grid

A 3 x 3 positioning grid provides position reference for multiple image operations. Red dots show the origin points of each region. After you use the `gravity` parameter to select a region, displacement must take place based on the corresponding farthest point.
![](https://main.qcloudimg.com/raw/53a143451229b4fbdd74935afe3832d5.png)

>
- When `gravity` is set to center, the `dx` and `dy` parameters are invalid.
- When `gravity` is set to north or south, the `dx` parameter is invalid (in which case the watermark is centered horizontally).
- When `gravity` is set to west or east, the `dy` parameter is invalid (in which case the watermark is centered vertically).

## Examples

This example shows you how to **add text watermark**.

```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?watermark/2/text/6IW-6K6v5LqRwrfkuIfosaHkvJjlm74/fill/IzNEM0QzRA/fontsize/20/dissolve/50/gravity/northeast/dx/20/dy/20/batch/1/degree/45
```

Final image:
![](https://main.qcloudimg.com/raw/e2ea173afafb7b50a2a7824b9173edf2.jpeg)

