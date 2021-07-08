## Overview
CI uses the **imageMogr2** API to rotate an image by a specified angle or automatically.

## API Format

```shell
download_url?imageMogr2/rotate/<rotateDegree>
					   /auto-orient
```

>! Spaces and line breaks above are for readability only and can be ignored.
>


## Parameters

| Parameter | Description |
| ------------------------- | ------------------------------------------------------------ |
| download_url | URL of the input image, formatted as `<BucketName-APPID>.cos.<picture region>.<domain>.com/<picture name>`<br>Example: `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg` |
| /rotate/<rotateDegree> | Rotates an image clockwise by a specified angle. Value range: 0−360. By default, the image is not rotated. |
| /auto-orient | Auto-rotates an image based on its EXIF orientation tag. |
| /flip/&lt;flip&gt; | Flips an image. Valid values: `vertical`, `horizontal` |
| /ignore-error/1 | If this parameter is carried and the image failed to be processed because it is too large, the input image will be returned with no error reported. |

## Examples

**Common rotation**
This example rotates an image by 90 degrees clockwise:

```
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/rotate/90
```

Output image:
![](https://main.qcloudimg.com/raw/2d47c4f47b8f9c8eca85a3590a106e14.jpeg)

