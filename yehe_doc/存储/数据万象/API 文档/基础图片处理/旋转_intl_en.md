## Feature Overview
This API is used to provide the rotation feature in Tencent Cloud CI, including common rotation and adaptive rotation.

## API Form

```shell
download_url?imageMogr2/rotate/<rotateDegree>
					   /auto-orient
```

> Ignore the preceding spaces and line breaks.


## Parameter Description

| Parameter | Description |
| ------------------------- | ------------------------------------------------------------ |
| download_url | URL that is used to access a file. The URL form is `<BucketName-APPID>.cos.<picture region>.<domain>.com/<picture name>`, <br>for example, `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg`. |
| /rotate/&lt;rotateDegree> | Common rotation, which indicates an image rotates clockwise. Value range: 0 - 360. The default value is not to rotate. |
| /auto-orient | Adaptive rotation, which adaptively rotates an image based on the EXIF information of the original image. |

## Example

This example shows you how to implement **common rotation**.
In the following example, an image is rotated by 90 degrees clockwise:

```
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/rotate/90
```

The final effect is as follows:
![](https://main.qcloudimg.com/raw/2d47c4f47b8f9c8eca85a3590a106e14.jpeg)
