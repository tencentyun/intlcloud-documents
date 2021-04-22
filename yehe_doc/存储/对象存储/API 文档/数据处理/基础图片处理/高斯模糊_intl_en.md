## Feature
This API **imageMogr2** from Tencent Cloud CI is used to blur images in COS.

>Image processing is a paid service, the fees of which are charged by Cloud Infinite. For detailed billing instructions, see Cloud Infinite’s [Billing and Pricing](https://intl.cloud.tencent.com/document/product/1045/33431).

## API Form

```plaintext
download_url?imageMogr2/blur/<radius>x<sigma>		
```

## Parameter Description

Operation name: blur.

| Parameter | Description |
| -------------- | ----------------------------- |
| download_url | URL that is used to access a file. Format: `<BucketName-APPID>.cos.<picture region>.<domain>.com/<picture name>`,<br>such as `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg` |
| radius&lt;radius> | Blurring radius. Value range: 1 - 50. |
| sigma&lt;sigma> | Standard deviation of normal distribution. The value must be greater than 0. |

> This parameter is not supported when the image format is gif.

## Examples

This example shows you how to perform Gaussian blur when the blurring radium is 8 and sigma is 5.

```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/blur/8x5
```

The effect of the Gaussian blur is as follows:
![](https://main.qcloudimg.com/raw/d635efeeca1d160e773737361e375801.jpeg)

