## Feature Overview

This API is used to obtain the average hue information of an image in Tencent Cloud CI. The size of the input image to be processed cannot exceed 20 MB, its width and height cannot exceed 30,000 pixels respectively, and its total pixels cannot exceed 250 million. The width and height of the output image cannot exceed 9,999 pixels respectively. For animated images, the input image's Width x Height x Number of frames cannot exceed 250 million pixels.

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
