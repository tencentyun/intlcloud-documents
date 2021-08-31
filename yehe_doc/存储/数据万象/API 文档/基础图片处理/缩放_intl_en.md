## Overview
The **imageMogr2** API is used to scale an image.

>?The image to be processed should not be larger than 20 MB, with the width and height not exceeding 30,000 pixels and the total number of pixels not exceeding 250 million. The width and height of the output image should not exceed 9,999 pixels.


## API Format

```shell
download_url?imageMogr2/thumbnail/<imageSizeAndOffsetGeometry>
```

## Parameter Description

Operation name: thumbnail

| Parameter | Description |
| ----------------------------- | ------------------------------------------------------------ |
| download_url | Access URL of the file, formatted as `<BucketName-APPID>.cos.<picture region>.<domain>.com/<picture name>`<br>Example: `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg` |
| /thumbnail/!&lt;Scale>p | Specifies the percentage to scale the width and height of the input image. |
| /thumbnail/!&lt;Scale>px | Specifies the percentage to scale the width of the input image, without changing the height. |
| /thumbnail/!x&lt;Scale>p | Specifies the percentage to scale the height of the input image, without changing the width. |
| /thumbnail/&lt;Width>x | Specifies the width of the output image, with the height scaled automatically. |
| /thumbnail/x&lt;Height> | Specifies the height of the output image, with the width scaled automatically. |
| /thumbnail/&lt;Width>x&lt;Height> | Specifies the maximum width and height of the thumbnail for scaling. |
| /thumbnail/&lt;Width>x&lt;Height>> | Specifies the maximum width and height of the thumbnail to scale down the image. The smaller value between the width scale ratio and height scale ratio will be used as the scale ratio. If both the output width and height are greater than the input width and height, the image will not be scaled. |
|  /thumbnail/&lt;Width>x&lt;Height>< | Specifies the maximum width and height of the thumbnail to scale up the image. The smaller value between the width scale ratio and height scale ratio will be used as the scale ratio. If both the output width and height are smaller than the input width and height, the image will not be scaled. |
| /thumbnail/!&lt;Width>x&lt;Height>r | Specifies the minimum width and height of the thumbnail for scaling. |
| /thumbnail/&lt;Width>x&lt;Height>! | Specifies the output width and height with the aspect ratio of the input image ignored. Note that the output image may be distorted. |
| /thumbnail/&lt;Area>@ | Specifies the maximum number of pixels of the output image. |
| /pad/ | Scales the input image as large as possible in a rectangle with the specified width and height. The color specified in `color` will be used to pad the blank area, with the image centered. Valid values: `0` (disables padding mode), `1` (enables padding mode) |
| /color/ | Padding color. Defaults to `3D3D3D` (gray). The value must be in hexadecimal format, for example, `#FF0000`. For format conversion, please see [RGB Color Codes Chart](https://www.rapidtables.com/web/color/RGB_Color.html). The value must be [URL-safe Base64-encoded](https://intl.cloud.tencent.com/document/product/1045/33430). |

## Examples

Input image:
![](https://main.qcloudimg.com/raw/3d4682ff8e622425ebd29913810a5c38.jpeg)

#### Scaling the width and height

This example scales down the input image by 50% in width and height:
```
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/thumbnail/!50p
```

Final effect:
![](https://main.qcloudimg.com/raw/2b64595a4a7046dc03f43a2a578764de.jpeg)

#### Scaling the width without changing the height

This example scales down the width of the input image by 50% without changing the height:
```
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/thumbnail/!50px
```

Final effect:
![](https://main.qcloudimg.com/raw/988ad350c611a662156e34c28aa5f8a2.jpeg)

#### Scaling in padding mode

This example scales the input image as large as possible in a 600 x 600 rectangle and pads the blank area with a specified color:
```
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/thumbnail/600x600/pad/1/color/IzNEM0QzRA
```

Final effect:
![](https://main.qcloudimg.com/raw/5f1d9423eaa73e2115fa969667738dee.jpg)

