## Description
The **imageMogr2** API is used to provide the following rotation features: common rotation and adaptive rotation.

## API Format

```
download_url?imageMogr2/rotate/<rotateDegree>
					   /auto-orient
```

> Ignore the preceding spaces and linefeeds.


## Parameter Description

| Parameter | Description |
| ------------------------- | ------------------------------------------------------------ |
| download_url | The file URL in the format of `<BucketName-APPID>.<picture region>.<domain>.com/<picture name>`, <br>for example, `examplebucket-1250000000.picsh.myqcloud.com/picture.jpeg`. |
| /rotate/&lt;rotateDegree> | The common rotation mode. It specifies the degree by which the image is rotated clockwise. Value range: 0-360. The image is not rotated by default. |
| /auto-orient | The adaptive rotation mode. In this mode, the image is adaptively rotated to restore to its original orientation based on the EXIF information of the original image. |

## Example

**Common rotation**
This example rotates an image by 90 degrees clockwise:

```
http://examples-1251000004.picsh.myqcloud.com/sample.jpeg?imageMogr2/rotate/90
```

Final effect:
![](https://main.qcloudimg.com/raw/2d47c4f47b8f9c8eca85a3590a106e14.jpeg)
