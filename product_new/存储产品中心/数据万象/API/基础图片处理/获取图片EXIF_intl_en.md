## Description
An exchangeable image file (EXIF) can record the shooting parameters, thumbnail, and other properties of a digital image. The **exif** API is used to obtain EXIF information. Currently, this API is applicable for images with a size no greater than 20 MB and a length and width both less than 9,999 pixels.


> If an image has no EXIF information, `{"error" : "no exif data"}` is returned.

## API Format

```
download_url?exif
```

### Parameter description

**Operation**: exif

| Parameter | Description |
| ------------ | ------------------------------------------------------------ |
| download_url | The file access URL in the format of `<BucketName-APPID>.<picture region>.<domain>.com/<picture name>`, <br>for example, `examplebucket-1250000000.picsh.myqcloud.com/picture.jpeg`. |


## Example
```
http://examples-1251000004.picsh.myqcloud.com/sample.jpeg?exif
```
