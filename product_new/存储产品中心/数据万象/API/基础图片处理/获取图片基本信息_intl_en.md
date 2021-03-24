## Overview
This API is used to query the basic information of an image, including the format, length, and width of the image in Tencent Cloud CI. The size of the input image to be processed cannot exceed 20 MB, its width and height cannot exceed 30,000 pixels respectively, and its total pixels cannot exceed 250 million. The width and height of the output image cannot exceed 9,999 pixels respectively. For animated images, the input image's Width x Height x Number of frames cannot exceed 250 million pixels.

## API Form

```
download_url?imageInfo
```

## Parameter Description

**Operation name**: imageInfo

| Parameter | Description |
| ------------ | ------------------------------------------------------------ |
| download_url | URL that is used to access a file. The URL form is `<BucketName-APPID>.cos.<picture region>.<domain>.com/<picture name>`, <br>for example, `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg`. |

## Example

**Request**
```
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageInfo
```


**Response**
```
{"format": "jpeg", "width": "960", "height": "540", "size": "158421", "md5": "77a16fa70e2eba652fb42e8a639c52f2", "photo_rgb": "0x736246"}
```
