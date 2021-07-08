## Overview
CI uses the **imageMogr2** API to adjust the brightness of an image.

## API Format

```shell
download_url?imageMogr2/bright/<value>
```

## Parameters

Operation: bright

| Parameter | Description |
| ---------------- | ------------------------------------------------------------ |
| download_url | URL of the input image, formatted as `<BucketName-APPID>.cos.<picture region>.<domain>.com/<picture name>`<br>Example: `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg` |
| /bright/<value> | Adjusts the brightness of an image. The value must be an integer in the range of [−100, 100]. <br><LI>`value` < 0: reduces the brightness. <br><LI>`value` = 0: does not adjust the brightness. <br><LI>`value` > 0: increases the brightness. |
| /ignore-error/1 | If this parameter is carried and the image failed to be processed because it is too large, the input image will be returned with no error reported. |

## Examples

#### Brightness adjustment

This example increases the brightness of an image by 70:

```PLAINTEXT 
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/bright/70
```

Output image:

![](https://main.qcloudimg.com/raw/f0fac36084c6d6709ad832c91752ee28.jpg)	
