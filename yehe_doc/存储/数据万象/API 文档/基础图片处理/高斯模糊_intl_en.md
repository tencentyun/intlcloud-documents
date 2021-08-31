## Overview
This API is used to blur images in Tencent Cloud CI.

## API Form

```shell
download_url?imageMogr2/blur/<radius>x<sigma>		
```

## Parameter Description

Operation name: blur.

| Parameter | Description |
| -------------- | ----------------------------- |
| download_url | URL that is used to access a file. The URL form is `<BucketName-APPID>.cos.<picture region>.<domain>.com/<picture name>`, <br>for example, `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg`. |
| radius&lt;radius> | Blurring radius. Value range: 1 - 50. |
| sigma&lt;sigma> | Standard deviation of normal distribution. The value must be greater than 0. |

> This parameter is not supported when the image format is gif.

## Example

This example shows how to perform Gaussian blurring when the blurring radius is 8 and sigma is 5.

```
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/blur/8x5
```

The effect of the Gaussian blurring is as follows:
![](https://main.qcloudimg.com/raw/d635efeeca1d160e773737361e375801.jpeg)

