## Feature Overview

This API is used to obtain the average hue information of an image in Tencent Cloud CI. Currently, images smaller than 20 MB in size and smaller than 9,999 pixels in length and width are supported.


## API Form
```
download_url?imageAve       				
```

## Parameter Description

**Operation name**: imageAve.

| Parameter | Description |
| ------------ | ------------------------------------------------------------ |
| download_url | URL that is used to access a file. The URL form is `<BucketName-APPID>.cos.<picture region>.<domain>.com/<picture name>`, <br>for example, `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg`. |


## Example

#### Request

```
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageAve
```

#### Response
```
{"RGB": "0x736246"}
```
