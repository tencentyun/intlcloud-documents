## Description
Through the **imageMogr2** API, Tencent Cloud CI allows you to perform the following cropping operations: cut (regular cropping), crop (scaling and cropping), iradius (inscribed circle cropping), rradius (rounded corner cropping), and scrop (smart cropping).

## API Format

```
download_url?imageMogr2/cut/<width>x<height>x<dx>x<dy>
					   /crop/<imageSizeAndOffsetGeometry>
					   /iradius/<radius>
                       /rradius/<radius>
					   /scrop/<Width>x<Height>
```

> Ignore the spaces and line breaks above.


## Parameter Description

| Parameter | Description |
| ------------ | ------------------------------------------------------------ |
| download_url | The file URL in the format of `<BucketName-APPID>.<picture region>.<domain>.com/<picture name>`, <br>for example, `examplebucket-1250000000.picsh.myqcloud.com/picture.jpeg`. |

#### Parameters for the cut operation

Operation: cut

| Parameter | Description |
| ----------- | ----------------------------------- |
| &lt;width> | Specify the width of the target image. |
| &lt;height> | Specify the height of the target image. |
| &lt;dx> | Specify the horizontal offset (dx) to the right relative to the top-left vertex of the image. |
| &lt;dy> | Specify the vertical downward offset (dy). |


> The parameter value should be greater than 0 and less than the width or height of the original image.


#### Parameters for the crop operation

Operation: crop

| Parameter | Description |
| ---------------------------- | ------------------------------------------------------------ |
| /crop/&lt;Width>x | Specify the width of the target image, and leave the height unchanged. The value of Width should be greater than 0 and less than the width of the original image. |
| /crop/x&lt;Height> | Specify the height of the target image, and leave the width unchanged. The value of Height should be greater than 0 and less than the height of the original image. |
| /crop/&lt;Width>x&lt;Height> | Specify the width and height of the target image. The values of Width or Height should both be greater than 0 and respectively less than the width and the height of the original image. |

During the crop operation, you can also use the `gravity` parameter to specify the location of the start point. For more information, see the [example of the scaling and cropping](#Crop).

<span id="1"></span>

#### Parameters for the iradius operation

Operation: iradius

| Parameter | Description |
| -------------------- | ------------------------------------------------------------ |
| /iradius/&lt;radius> | This parameter refers to the inscribed circle cropping function, where radius specifies the radius of the inscribed circle. The value of radius is an integer that is greater than 0 and less than half the length of the shorter side of the original image. The center of the inscribed circle is the center of the original image. This parameter is not supported if the image format is gif. |

#### Parameters for the rradius operation

Operation name: rradius

| Parameter | Description |
| -------------------- | ------------------------------------------------------------ |
| /rradius/&lt;radius&gt; | This parameter refers to the rounded corner cropping function, where radius specifies the radius of the rounded corner of the image. The value of radius is an integer that is greater than 0 and less than half the length of the shorter side of the original image. The rounded corner is tangent to the edge of the original image. This parameter is not supported if the image format is gif. |



#### Parameters for the scrop operation

Operation: scrop

| Parameter | Description |
| ----------------------------- | ------------------------------------------------------------ |
| /scrop/&lt;Width>x&lt;Height> | This parameter refers to performing zooming and cropping based on the location of the human face in the image. Width and Height respectively specify the width and the height of the target image. |

## Nine-Part Grid

A nine-part grid can provide a location reference for various operations performed on an image. The red dot is the origin of each region (after each region is selected by using the `gravity` parameter, the displacement operation is performed by taking the corresponding far point as the reference.) 
![](https://main.qcloudimg.com/raw/53a143451229b4fbdd74935afe3832d5.png)

> !
- When `gravity` is set to center, the `dx` and `dy` parameters are invalid.
- When `gravity` is set to north or south, the `dx` parameter is invalid (in which case the watermark is horizontally centered).
- When `gravity` is set to west or east, the `dy` parameter is invalid (in which case the watermark is vertically centered).



## Examples
**Cut**
This example shows how to translate by 100 pixels horizontally to the right and 10 pixels vertically to the bottom relative to the top-left vertex of the image. It also shows how to cut the image according to the specified target image resolution of 600 × 600 pixels:

```
http://examples-1251000004.picsh.myqcloud.com/sample.jpeg?imageMogr2/cut/600x600x100x10
```

Original image:
![](https://main.qcloudimg.com/raw/becc02d71fb703c2e87ad15e19808bb1.jpeg)

Final effect:
![](https://main.qcloudimg.com/raw/e28696af6be355cc678284b621a7c97b.jpeg)

<span id="Crop"></span>
**Crop**
Assuming that the center point (center) is used as the reference point, this example shows how to crop the image to the specified resolution of 300 × 400 pixels:

```
http://examples-1251000004.picsh.myqcloud.com/sample.jpeg?imageMogr2/crop/300x400/gravity/center 
```

Final effect:
![](https://main.qcloudimg.com/raw/b9adeff300df483c22765b7d746d6690.jpeg)

**iradius**
This example shows how to perform the inscribed circle cropping operation according to the specified radius of 300:

```
http://examples-1251000004.picsh.myqcloud.com/sample.jpeg?imageMogr2/iradius/300
```

Final effect:
![](https://main.qcloudimg.com/raw/f38ead869790236879a229f2d5f1bafc.jpeg)

**rradius**
This example shows how to perform the rounded corner cropping operation according to the specified radius of 100:
```
http://examples-1251000004.picsh.myqcloud.com/sample.jpeg?imageMogr2/rradius/100 
```

Final effect:
![](https://main.qcloudimg.com/raw/795e0a3254137a5815b9f9f23cecbb91.jpeg)


**Scrop**
This example shows how to crop the image to the specified resolution of 100 × 600 pixels based on the location of the human face in the image:

```
http://examples-1251000004.picsh.myqcloud.com/sample.jpeg?imageMogr2/scrop/100x600
```

> If no human face is recognized in the image, the original image is restored.
