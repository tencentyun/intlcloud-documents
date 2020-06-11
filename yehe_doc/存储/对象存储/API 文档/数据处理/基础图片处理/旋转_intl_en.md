## Feature
This API **imageMogr2** from Tencent Cloud CI is used to rotate images in COS, including common rotation and adaptive rotation.

>Image processing is a paid service, the fees of which are charged by Cloud Infinite. For detailed billing instructions, see Cloud Infinite’s [Billing and Pricing](https://intl.cloud.tencent.com/document/product/1045/33431).
## API Form

```plaintext
download_url?imageMogr2/rotate/<rotateDegree>
					   /auto-orient
```

>Please ignore the preceding spaces and line breaks.


## Parameter Description

| Parameter                         | Description                                                         |
| ------------------------- | ------------------------------------------------------------ |
| download_url | URL that is used to access a file. Format: `<BucketName-APPID>.cos.<picture region>.<domain>.com/<picture name>`, <br>for example, `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg`. |
| /rotate/&lt;rotateDegree> | Common rotation, which indicates an image rotates clockwise. Value range: 0 - 360. Default: none. |
| /auto-orient | Adaptive rotation, which adaptively rotates an image based on the EXIF data of the original image. |

## Examples

**Common rotation**

The example below shows how to rotate an image 90 degrees clockwise.

```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/rotate/90
```

The final effect is as follows:
![](https://main.qcloudimg.com/raw/2d47c4f47b8f9c8eca85a3590a106e14.jpeg)
