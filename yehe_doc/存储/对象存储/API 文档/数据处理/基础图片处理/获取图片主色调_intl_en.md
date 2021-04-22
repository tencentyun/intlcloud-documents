## Feature

This API **imageAve** from Tencent Cloud CI is used to obtain the average hue information about an image in COS. Currently, supported images are smaller than 20 MB in size and smaller than 9,999 pixels in length and width.

>Image processing is a paid service, the fees of which are charged by Cloud Infinite. For detailed billing instructions, see Cloud Infinite’s [Billing and Pricing](https://intl.cloud.tencent.com/document/product/1045/33431).

## API Form
```plaintext
download_url?imageAve       				
```

## Parameter Description

**Operation name**: imageAve.

| Parameter         | Description                                                         |
| ------------ | ------------------------------------------------------------ |
| download_url | URL that is used to access a file. Format: `<BucketName-APPID>.cos.<picture region>.<domain>.com/<picture name>`, <br>for example, `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg`. |


## Examples

#### Request

```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageAve
```

#### Response
```plaintext
{"RGB": "0x736246"}
```
