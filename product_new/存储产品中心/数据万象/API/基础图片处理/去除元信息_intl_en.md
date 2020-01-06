## Description

The **imageMogr2** API is used to remove image meta information including EXIF information.

## API Format
```
download_url?imageMogr2/strip
```

## Parameter Description

Operation: strip

| Parameter | Description |
| ------------ | ------------------------------------------------------------ |
| download_url | The file access URL in the format of `<BucketName-APPID>.<picture region>.<domain>.com/<picture name>`, <br>for example, `examplebucket-1250000000.picsh.myqcloud.com/picture.jpeg`. | 

## Example

**Removing image meta information**
```
http://examples-1251000004.picsh.myqcloud.com/sample.jpeg?imageMogr2/strip	