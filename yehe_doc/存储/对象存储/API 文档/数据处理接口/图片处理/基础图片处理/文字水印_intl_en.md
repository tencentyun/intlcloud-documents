## Overview
COS uses the **watermark** API provided by Cloud Infinite (CI) to overlay a text watermark over an image in real time. The size of an input image cannot be larger than 32 MB, and its width and height cannot exceed 9,999 pixels.

>! Image Processing is charged by CI. For detailed pricing, please see **Basic image processing fee** in [Billing and Pricing](https://intl.cloud.tencent.com/document/product/1045/33431).
>

An image can be processed:

- Upon download
- Upon upload
- In cloud



## API Format

#### 1. Processing upon download

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

> ? Spaces and line breaks above are for readability only and can be ignored.

#### 2. Processing upon upload

```http
PUT /<ObjectKey> HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
Pic-Operations: 
{
  "is_pic_info": 1,
  "rules": [{
      "fileid": "exampleobject",
      "rule": "watermark/2/text/<encodedText>
                        /font/<encodedFont>
                        /fontsize/<fontSize>
                        /fill/<encodedColor>
                        /dissolve/<dissolve>
                        /gravity/<gravity>
                        /dx/<dx>
                        /dy/<dy>
                        /batch/<type>
                        /degree/<degree>"
  }]
}
```

#### 3. Processing in-cloud data

```http
POST /<ObjectKey>?image_process HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Content-length: Size
Authorization: Auth String
Pic-Operations: 
{
  "is_pic_info": 1,
  "rules": [{
      "fileid": "exampleobject",
      "rule": "watermark/2/text/<encodedText>
                        /font/<encodedFont>
                        /fontsize/<fontSize>
                        /fill/<encodedColor>
                        /dissolve/<dissolve>
                        /gravity/<gravity>
                        /dx/<dx>
                        /dy/<dy>
                        /batch/<type>
                        /degree/<degree>"
  }]
}
```

>? **Processing upon download** is used as an example here, which does not store the output image in a bucket. If you need to store the output image, please see [Persistent Image Processing](https://intl.cloud.tencent.com/document/product/1045/33695) and use **Processing upon upload** or **Processing in-cloud data**.


## Parameters

In the code above, `watermark` is the operation name and the number `2` indicates that the watermark is a text.

| Parameter | Description |
| ------------ | ------------------------------------------------------------ |
| download_url | URL of the input image, formatted as `<BucketName-APPID>.cos.<Region>.myqcloud.com/<picture name>`<br>Example: `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg` |
| /text/  | Watermark text, which must be [URL-safe Base64-encoded](https://intl.cloud.tencent.com/document/product/1045/33430) |
| /font/ | Font of the text, which must be [URL-safe Base64-encoded](https://intl.cloud.tencent.com/document/product/1045/33430). Default font: Tahoma.ttf (see [supported fonts](https://intl.cloud.tencent.com/document/product/1045/40681).) |
| /fontsize/   | Font size, in pt. Default value: `13`    |
| /fill/ | Font color. The value must be in hexadecimal format, for example, `#FF0000`. For format conversion, please see [RGB Color Codes Chart](https://www.rapidtables.com/web/color/RGB_Color.html). The value must be [URL-safe Base64-encoded](https://intl.cloud.tencent.com/document/product/1045/33430). Default value: `#3D3D3D` (gray) |
| /dissolve/ | Text opacity. Value range: 1−100. Default value: `90` (meaning 90% opacity) |
| /gravity/    | Position of the text watermark, which is a square in a [3x3 grid](#1). Default value: `southeast` |
| /dx/  | Horizontal offset in pixels. Default value: `0` |
| /dy/  | Vertical offset in pixels. Default value: `0` |
| /batch/ | Whether to tile the text watermark. If this parameter is set to `1`, the text watermark will be tiled across the input image. |
| /degree/ | Angle to rotate text watermarks. This parameter is valid only when `/batch/` is set to `1`. Value range: 0−360. Default value: `0`  |

<span id="1"></span>
## 3x3 Grid Position Diagram

The 3x3 grid position diagram is as follows. Once you specify the `gravity` parameter to position your watermark, the corresponding red dot becomes the reference point of the square, and offsets will be relative to this point.
![](https://main.qcloudimg.com/raw/53a143451229b4fbdd74935afe3832d5.png)

>!
> - If `gravity` is set to `center`, `dx` and `dy` are invalid.
> - If `gravity` is set to `north` or `south`, `dx` is invalid and the watermark will be centered horizontally.
> - If `gravity` is set to `west` or `east`, `dy` is invalid and the watermark will be centered vertically.
> 

## Examples

#### Adding a text watermark

```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?watermark/2/text/6IW-6K6v5LqRwrfkuIfosaHkvJjlm74/fill/IzNEM0QzRA/fontsize/20/dissolve/50/gravity/northeast/dx/20/dy/20/batch/1/degree/45
```

After text watermarks are added:
![](https://main.qcloudimg.com/raw/e2ea173afafb7b50a2a7824b9173edf2.jpeg)

#### Adding a text watermark with a signature carried

This example processes the image in the same way as in the example above except that a signature is added. The signature is joined with other processing parameters using an ampersand (&):

```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?q-sign-algorithm=<signature>&watermark/2/text/6IW-6K6v5LqRwrfkuIfosaHkvJjlm74/fill/IzNEM0QzRA/fontsize/20/dissolve/50/gravity/northeast/dx/20/dy/20/batch/1/degree/45
```

>? You can obtain the value of `<signature>` by referring to [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).
>

