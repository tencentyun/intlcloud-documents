## Description
The **imageMogr2** API is used to scale an image.

## API Format
```
download_url?imageMogr2/thumbnail/<imageSizeAndOffsetGeometry>
```

## Parameter Description

Operation: thumbnail

| Parameter | Description |
| ----------------------------- | ------------------------------------------------------------ |
| download_url | The file URL in the format of `<BucketName-APPID>.<picture region>.<domain>.com/<picture name>`, <br>for example, `examplebucket-1250000000.picsh.myqcloud.com/picture.jpeg`. |
| /thumbnail/!&lt;Scale>p | Specifies the scaled percentage of the width and height of the target image relative to those of the original image. |
| /thumbnail/!&lt;Scale>px | Specifies the scaled percentage of the width of the target image relative to that of the original image, where the height remains unchanged. |
| /thumbnail/!x&lt;Scale>p | Specifies the scaled percentage of the height of the target image relative to that of the original image, where the width remains unchanged. |
| /thumbnail/&lt;Width>x | Specifies the width of the target image, where the height is scaled proportionally. |
| /thumbnail/x&lt;Height> | Specifies the height of the target image, where the width is scaled proportionally. |
| /thumbnail/&lt;Width>x&lt;Height> | Specifies the maximum width and height of the thumbnail for proportional scaling. |
| /thumbnail/!&lt;Width>x&lt;Height>r | Specifies the minimum width and height of the thumbnail for proportional scaling. |
| /thumbnail/&lt;Width>x&lt;Height>  | Specifies the width and height of the target image without considering the aspect ratio of the original image. This forcibly scales the image and may distort the target image. |
| /thumbnail/&lt;Area>@ | Specifies the maximum number of pixels of the proportionally scaled target image. |

## Example

Original image:
![](https://main.qcloudimg.com/raw/3d4682ff8e622425ebd29913810a5c38.jpeg)

**Scaling the width and height**
This example scales down the original image by 50% in width and height:
```
http://examples-1251000004.picsh.myqcloud.com/sample.jpeg?imageMogr2/thumbnail/!50p
```

Final effect:
![](https://main.qcloudimg.com/raw/2b64595a4a7046dc03f43a2a578764de.jpeg)

**Scaling the width and keeping the height unchanged**
This example scales down the target image by 50% in width while keeping the height unchanged:
```
http://examples-1251000004.picsh.myqcloud.com/sample.jpeg?imageMogr2/thumbnail/!50px
```

Final effect:
![](https://main.qcloudimg.com/raw/988ad350c611a662156e34c28aa5f8a2.jpeg)