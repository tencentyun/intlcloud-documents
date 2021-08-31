## Feature

This API is used to remove image metadata such as exif information in Tencent Cloud CI.

## API Form
```
download_url?imageMogr2/strip
```

## Parameter Description

Operation name: strip.

| Parameter | Description |
| ------------ | ------------------------------------------------------------ |
| download_url | URL that is used to access a file. The URL form is `<BucketName-APPID>.cos.<picture region>.<domain>.com/<picture name>`, <br>for example, `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg`. |

## Example

This example shows you how to **remove metadata**.
```
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/strip	
```
