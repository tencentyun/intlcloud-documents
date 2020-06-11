## Feature

This API **imageMogr2** from Tencent Cloud CI is used to remove image metadata, such as EXIF data, in COS.

>Image processing is a paid service, the fees of which are charged by Cloud Infinite. For detailed billing instructions, see Cloud Infinite’s [Billing and Pricing](https://intl.cloud.tencent.com/document/product/1045/33431).

## API Form
```plaintext
download_url?imageMogr2/strip
```

## Parameter Description

Operation name: strip.

| Parameter         | Description                                                         |
| ------------ | ------------------------------------------------------------ |
| download_url | URL that is used to access a file. Format: `<BucketName-APPID>.cos.<picture region>.<domain>.com/<picture name>`, <br>for example, `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg`. |

## Examples

**Removing metadata**:
```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/strip	
```
