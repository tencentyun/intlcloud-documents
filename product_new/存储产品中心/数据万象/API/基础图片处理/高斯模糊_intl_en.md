## Description
Through the **imageMogr2** API, Tencent Cloud CI allows you to blur an image.

## API Format
```
download_url?imageMogr2/blur/<radius>x<sigma>		
```

## Parameter Description

Operation: blur

| Parameter | Description |
| -------------- | ----------------------------- |
| download_url | The file URL in the format of `<BucketName-APPID>.<picture region>.<domain>.com/<picture name>`, <br>for example, `examplebucket-1250000000.picsh.myqcloud.com/picture.jpeg`. |
| radius&lt;radius> | The blur radius. Value range: 1-50. |
| sigma&lt;sigma> | The standard deviation of normal distribution. The value must be greater than 0. |

> This parameter is not supported if the image format is gif.

## Example

This example shows blurring an image by setting radius to 8 and sigma to 5:

```
http://examples-1251000004.picsh.myqcloud.com/sample.jpeg?imageMogr2/blur/8x5
```

Blurred effect:
![](https://main.qcloudimg.com/raw/d635efeeca1d160e773737361e375801.jpeg)
