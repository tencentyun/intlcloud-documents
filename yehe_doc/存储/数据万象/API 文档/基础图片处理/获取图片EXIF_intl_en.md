## Feature Overview
Exchangeable Image File (EXIF) can record the shooting parameters, thumbnails, and other attributes of digital pictures. This API is used to obtain EXIF information in Tencent Cloud CI. Currently, images smaller than 20 MB in size and smaller than 9,999 pixels in length and width are supported.


> If an image has no exif information, `{"error" : "no exif data"}` will be returned.

## API Form

```
download_url?exif
```

## Parameter Description

**Operation name**: exif.

| Parameter | Description |
| ------------ | ------------------------------------------------------------ |
| download_url | URL that is used to access a file. The URL form is `<BucketName-APPID>.cos.<picture region>.<domain>.com/<picture name>`, <br>for example, `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg`. |


## Example
```
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?exif
```

