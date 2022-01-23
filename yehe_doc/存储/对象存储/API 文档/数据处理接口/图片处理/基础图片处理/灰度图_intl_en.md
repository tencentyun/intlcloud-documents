## Overview
COS uses CI’s **imageMogr2/grayscale** API to set an image to be a grayscale image.

## API Format

```plaintext
download_url?imageMogr2/grayscale/<value>
```

## Parameters

Operation: grayscale

| Parameter | Description |
| --------------------- | ------------------------------------------------------------ |
| download_url | URL of the input image, formatted as `&lt;BucketName-APPID>.cos.&lt;Region>.myqcloud.com/&lt;picture name>`<br>Example: `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg` |
| /grayscale/&lt;value> | Whether to set an image to be a grayscale image.<br>`value` being `0` indicates not to modify the image. <br>`value` being `1` indicates to set the image to be a grayscale image. |
| /ignore-error/1 | If this parameter is carried and the image failed to be processed because it is too large, the input image will be returned with no error reported. |

## Examples

Set an image to be a grayscale image:

```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/grayscale/1
```

Output image:

![img](http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/grayscale/1)
