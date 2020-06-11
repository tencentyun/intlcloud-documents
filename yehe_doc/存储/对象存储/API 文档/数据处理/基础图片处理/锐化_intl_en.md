## Feature
This API **imageMogr2** from Tencent Cloud CI is used to sharpen images in COS.

>Image processing is a paid service, the fees of which are charged by Cloud Infinite. For detailed billing instructions, see Cloud Infinite’s [Billing and Pricing](https://intl.cloud.tencent.com/document/product/1045/33431).

## API Form

```plaintext
download_url?imageMogr2/sharpen/<value>
```

## Parameter Description

Operation name: sharpen.

| Parameter                         | Description                                                         |
| ---------------- | ------------------------------------------------------------ |
| download_url | URL that is used to access a file. Format: `<BucketName-APPID>.cos.<picture region>.<domain>.com/<picture name>`, <br>for example, `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg`. |
| /sharpen/&lt;value> | Image sharpening. `value` indicates the value of the `sharpen` parameter, and is an integer from 10 to 300. The greater the value, the highly an image is sharpened. We recommend that you set the parameter to 70. |

## Examples

#### Sharpening

This example shows you how to sharpen an image with `sharpen` value set to 70.
```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/sharpen/70
```

The final effect is as follows:
![](https://main.qcloudimg.com/raw/b599b8cc198d9682d2f6316aa0e44a9d.jpeg)
