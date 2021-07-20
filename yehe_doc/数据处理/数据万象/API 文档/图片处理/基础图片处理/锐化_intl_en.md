## Overview
CI uses the **imageMogr2** API to sharpen an image.

## API Format

```shell
download_url?imageMogr2/sharpen/<value>
```

## Parameters

Operation: sharpen

| Parameter | Description |
| ---------------- | ------------------------------------------------------------ |
| download_url | URL of the input image, formatted as `<BucketName-APPID>.cos.<picture region>.<domain>.com/<picture name>`<br>Example: `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg` |
| /sharpen/&lt;value> | Sharpens an image, where `value` controls the strength of the sharpening effect. The greater the value, the more obvious the sharpening. Value range: an integer in the range of 10 to 300 (70 is recommended.) |
| /ignore-error/1 | If this parameter is carried and the image failed to be processed because it is too large, the input image will be returned with no error reported. |

## Examples

#### Sharpening

This example sharpens an image with the sharpening value of `70`:
```
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/sharpen/70
```

Output image:
![](https://main.qcloudimg.com/raw/b599b8cc198d9682d2f6316aa0e44a9d.jpeg)

#### Sharpening an image with a signature carried

This example processes the image in the same way as in the example above except that a signature is carried. The signature is joined with other processing parameters using an ampersand (&):

```
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?q-sign-algorithm=<signature>&imageMogr2/sharpen/70
```

>? You can obtain the value of `<signature>` by referring to [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).
>
