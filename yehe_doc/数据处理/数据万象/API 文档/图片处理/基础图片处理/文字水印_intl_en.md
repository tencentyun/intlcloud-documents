## Overview
CI uses the **watermark** API to add text watermarks in real time. An input image cannot be larger than 32 MB, with its width and height not exceeding 30,000 pixels and the total number of pixels not exceeding 250 million. The width and height of the output image cannot exceed 9,999 pixels. For an input animated image, its total number of pixels (Width x Height x Number of frames) cannot exceed 250 million.

## API Format

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

>? Spaces and line breaks above are for readability only and can be ignored.


## Parameters

In the code above, `watermark` is the operation name and the number `2` indicates that the watermark is a text.

| Parameter | Description |
| ------------ | ------------------------------------------------------------ |
| download_url | URL of the input image, formatted as `<BucketName-APPID>.cos.<picture region>.<domain>.com/<picture name>`<br>Example: `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg` |
| /text/  | Watermark text, which must be [Base64 URL-safe encoded](https://intl.cloud.tencent.com/document/product/1045/33430) |
| /font/ | Font of the text, which must be [Base64 URL-safe encoded](https://intl.cloud.tencent.com/document/product/1045/33430). Default font: Tahoma.ttf |
| /fontsize/   | Font size, in pt. Default value: `13`    |
| /fill/ | Font color. The value must be in hexadecimal format, for example, `#FF0000`. For format conversion, please see [RGB Color Codes Chart](https://www.rapidtables.com/web/color/RGB_Color.html). The value must be [URL-safe Base64-encoded](https://intl.cloud.tencent.com/document/product/1045/33430). Default value: `#3D3D3D` (gray) |
| /dissolve/ | Text opacity. Value range: 1−100. Default value: `90` (meaning 90% opacity) |
| /gravity/    | Position of the text watermark, which is a square in a [3x3 grid](#1). Default value: `southeast` |
| /dx/  | Horizontal offset in pixels. Default value: `0` |
| /dy/  | Vertical offset in pixels. Default value: `0` |
| /batch/ | Whether to tile the text watermark. If this parameter is set to `1`, the text watermark will be tiled across the input image. |
| /degree/ | Angle to rotate text watermarks. This parameter is valid only when `/batch/` is set to `1`. Value range: 0−360. Default value: `0`  |
| /ignore-error/1 | If this parameter is carried and the image failed to be processed because it is too large, the input image will be returned with no error reported. |

<span id="1"></span>
## 3x3 Grid Position Diagram

The 3x3 grid position diagram is as follows. Once you specify the `gravity` parameter to position your watermark, the corresponding red dot becomes the reference point of the square, and offsets will be relative to this point.
![](https://main.qcloudimg.com/raw/53a143451229b4fbdd74935afe3832d5.png)

>!
> - If `gravity` is set to `center`, `dx` and `dy` are invalid.
> - If `gravity` is set to `north` or `south`, `dx` is invalid and the watermark will be centered horizontally.
> - If `gravity` is set to `west` or `east`, `dy` is invalid and the watermark will be centered vertically.

## Example
**Adding a text watermark**

```
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?watermark/2/text/6IW-6K6v5LqRwrfkuIfosaHkvJjlm74/fill/IzNEM0QzRA/fontsize/20/dissolve/50/gravity/northeast/dx/20/dy/20/batch/1/degree/45
```

After text watermarks are added:
![](https://main.qcloudimg.com/raw/e2ea173afafb7b50a2a7824b9173edf2.jpeg)

