## Feature
This API **imageMogr2** from Tencent Cloud CI is used to scale images in COS.

>Image processing is a paid service, the fees of which are charged by Cloud Infinite. For detailed billing instructions, see Cloud Infinite’s [Billing and Pricing](https://intl.cloud.tencent.com/document/product/1045/33431).

## API Form

```plaintext
download_url?imageMogr2/thumbnail/<imageSizeAndOffsetGeometry>
```

## Parameter Description

Operation name: thumbnail.

| Parameter                         | Description                                                         |
| ----------------------------- | ------------------------------------------------------------ |
| download_url | URL that is used to access a file. Format: `<BucketName-APPID>.cos.<picture region>.<domain>.com/<picture name>`, <br>for example, `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg`. |
| /thumbnail/!&lt;Scale>p | Specifies that the width and height of an image is Scale% of the original image. |
| /thumbnail/!&lt;Scale>px | Specifies that the width of an image is Scale% of the original image while the height keeps unchanged. |
| /thumbnail/!x&lt;Scale>p | Specifies that the height of the an image is Scale% of the original image while the width keeps unchanged. |
| /thumbnail/&lt;Width>x | Specifies the target image width, with the height proportionally scaled down. |
| /thumbnail/x&lt;Height> | Specifies the target image height, with the width proportionally scaled down. |
| /thumbnail/&lt;Width>x&lt;Height> | Specifies the maximum width and height of a thumbnail for proportional scaling |
| /thumbnail/!&lt;Width>x&lt;Height>r | Specifies the minimum width and height of a thumbnail for proportional scaling |
| /thumbnail/&lt;Width>x&lt;Height> | Forces image scaling with the specified Width and Height, which may cause deformation of the target image |
| /thumbnail/&lt;Area>@ | Proportionally scales an image so that its total pixels does not exceed the value of `Area` |

## Examples

Take the image below as an example:
![](https://main.qcloudimg.com/raw/3d4682ff8e622425ebd29913810a5c38.jpeg)

#### Example 1: scaling width and height

This example shows you how to scale an image to 50% of its original width and height.
```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/thumbnail/!50p
```

Final image:
![](https://main.qcloudimg.com/raw/2b64595a4a7046dc03f43a2a578764de.jpeg)

#### Example 2: scaling width while keeping height unchanged

This example shows you how to scale an image to 50% of its original width while keeping the height unchanged.
```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/thumbnail/!50px
```

Final image:
![](https://main.qcloudimg.com/raw/988ad350c611a662156e34c28aa5f8a2.jpeg)
