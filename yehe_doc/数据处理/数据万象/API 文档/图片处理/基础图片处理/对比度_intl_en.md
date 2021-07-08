## Overview
CI uses the **imageMogr2** API to adjust an image’s contrast, which is the difference in luminance between the brightest and darkest points in an image (i.e., the contrast in grayscale).

## API Format

```shell
download_url?imageMogr2/contrast/<value>
```

## Parameters

Operation: contrast

| Parameter | Description |
| ---------------- | ------------------------------------------------------------ |
| download_url | URL of the input image, formatted as `<BucketName-APPID>.cos.<picture region>.<domain>.com/<picture name>`<br>Example: `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg` |
| /contrast/<value> | Adjusts the contrast of an image. The value must be an integer in the range of [−100, 100].<br><li>`value` < 0: reduces the contrast.<br><li>`value` = 0: does not adjust the contrast.<br><li>`value` > 0: increases the contrast. |
| /ignore-error/1 | If this parameter is carried and the image failed to be processed because it is too large, the input image will be returned with no error reported. |

## Examples

#### Contrast adjustment

This example reduces the contrast of an image by 50:
```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/contrast/-50
```

Output image:
![](https://main.qcloudimg.com/raw/555a3a42dff976c0f4ef382de70eae79.jpg)
