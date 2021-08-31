## Overview
This API is used to sharpen images in Tencent Cloud CI.

## API Form

```shell
download_url?imageMogr2/sharpen/<value>
```

## Parameter Description

Operation name: sharpen.

| Parameter | Description |
| ---------------- | ------------------------------------------------------------ |
| download_url | URL that is used to access a file. The URL form is `<BucketName-APPID>.cos.<picture region>.<domain>.com/<picture name>`, <br>for example, `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg`. |
| /sharpen/&lt;value> | Image sharpening. value indicates the value of the sharpen parameter. The value is an integer from 10 to 300. The greater the value, the more significant of the sharpening effect. We recommend that you set the parameter to 70. |

## Example

#### Sharpening

This example shows you how to sharpen an image when the sharpen parameter is set to 70.
```
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/sharpen/70
```

The final effect is as follows:
![](https://main.qcloudimg.com/raw/b599b8cc198d9682d2f6316aa0e44a9d.jpeg)
