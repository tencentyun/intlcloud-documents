## Feature Overview
This API is used to scale images in Tencent Cloud CI.

## API Form

```shell
download_url?imageMogr2/thumbnail/<imageSizeAndOffsetGeometry>
```

## Parameter Description

Operation name: thumbnail.

| Parameter | Description |
| ----------------------------- | ------------------------------------------------------------ |
| download_url | URL that is used to access a file. The URL form is `<BucketName-APPID>.cos.<picture region>.<domain>.com/<picture name>`, <br>for example, `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg`. |
| /thumbnail/!&lt;Scale>p | Specifies that the width and height of an image is Scale% of the original image. |
| /thumbnail/!&lt;Scale>px | Specifies that the width of an image is Scale% of the original image while the height keeps unchanged. |
| /thumbnail/!x&lt;Scale>p | Specifies that the height of an image is Scale% of the original image while the width keeps unchanged. |
| /thumbnail/&lt;Width>x | Specifies that the width of the target image is Width and the height is proportionally compressed. |
| /thumbnail/x&lt;Height> | Specifies that the height of the target image is Height and the width is proportionally compressed. |
| /thumbnail/&lt;Width>x&lt;Height> | Limits the maximum width and height of a thumbnail to Width and Height respectively and performs proportional scaling. |
| /thumbnail/!&lt;Width>x&lt;Height>r | Limits the minimum width and height of a thumbnail to Width and Height respectively and performs proportional scaling. |
| /thumbnail/&lt;Width>x&lt;Height> | Ignores the width and height ratio of the original image, specifies the image width to Width and height to Height, and performs forcibly scaling, which may cause deformation of the target image. |
| /thumbnail/&lt;Area>@ | Proportionally scales an image so that the total pixels of the scaled image do not exceed Area. |

## Example

The original image is as follows:
![](https://main.qcloudimg.com/raw/3d4682ff8e622425ebd29913810a5c38.jpeg)

#### Scaling width and height

This example shows you how to scale an image to 50% of the original image’s width and height.
```
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/thumbnail/!50p
```

The final effect is as follows:
![](https://main.qcloudimg.com/raw/2b64595a4a7046dc03f43a2a578764de.jpeg)

#### Scaling width while keeping height unchanged

This example shows you how to scale an image to 50% of the original image’s width while keeping the height unchanged.
```
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/thumbnail/!50px
```

The final effect is as follows:
![](https://main.qcloudimg.com/raw/988ad350c611a662156e34c28aa5f8a2.jpeg)
