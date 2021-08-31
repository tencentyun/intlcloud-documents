## Overview
This API is used to query the basic information of an image, including the format, length, and width of the image in Tencent Cloud CI. Currently, images smaller than 20 MB in size and smaller than 9,999 pixels in length and width are supported.

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
