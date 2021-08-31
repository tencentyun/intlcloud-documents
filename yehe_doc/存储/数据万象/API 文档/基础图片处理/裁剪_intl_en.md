## Overview
This API is used to perform cropping, including regular cropping, scaling and cropping, inscribed circle cropping, rounded corner cropping, and smart cropping in Tencent Cloud CI.

## API Form

```shell
download_url?imageMogr2/cut/<width>x<height>x<dx>x<dy>
                       /crop/<imageSizeAndOffsetGeometry>
                       /iradius/<radius>
                       /rradius/<radius>
                       /scrop/<Width>x<Height>
```

> Ignore the preceding spaces and line breaks.


## Parameter Description

| Parameter | Description |
| ------------ | ------------------------------------------------------------ |
| download_url | URL that is used to access a file. The URL form is `<BucketName-APPID>.cos.<picture region>.<domain>.com/<picture name>`, <br>for example, `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg`. |

#### Regular cropping

Operation name: cut.

| Parameter | Description |
| ----------- | ----------------------------------- |
| &lt;width> | Specifies the width of the target image to Width. |
| &lt;height> | Specifies the height of the target image to Height. |
| &lt;dx> | Horizontally moves rightward relative to the upper-left vertex of the image by dx. |
| &lt;dy> | Vertically moves downward by dy. |


> The value range is greater than 0 and smaller than the width and height of the original image.


#### Scaling and cropping

Operation name: crop.

| Parameter | Description |
| ---------------------------- | ------------------------------------------------------------ |
| /crop/&lt;Width>x | Specifies the width of the target image to Width while keeping the height unchanged. The value range of Width is greater than 0 and smaller than the width of the original image. |
| /crop/x&lt;Height> | Specifies the height of the target image to Height while keeping the width unchanged. The value range of Height is greater than 0 and smaller than the width of the original image. |
| /crop/&lt;Width>x&lt;Height> | Specifies the width of the target image to Width and the height to Height. The value ranges of Width and Height are greater than 0 and smaller than the width of the original image. |

When performing scaling and cropping, you can also use the gravity parameter to specify the start position of the operation. For more information, see [Example of scaling and cropping](#Scaling and cropping).

<span id="1"></span>

#### Inscribed circle cropping

Operation name: iradius.

| Parameter | Description |
| -------------------- | ------------------------------------------------------------ |
| /iradius/&lt;radius> | Inscribed circle cropping. radius indicates the radius of the inscribed circle. The value is an integer that is greater than 0 and smaller than half of the smallest edge of the original image. The center of the inscribed circle is the center of the image. This parameter is not supported when the image format is gif. |

#### Rounded corner cropping

Operation name: rradius.

| Parameter | Description |
| -------------------- | ------------------------------------------------------------ |
|/rradius/&lt;radius&gt;| Rounded corner cropping. radius indicates the rounded corner edge radius of the image. The value is an integer that is greater than 0 and smaller than half of the smallest edge of the original image. The rounded corner is tangent to the edge of the original image. This parameter is not supported when the image format is gif. |



#### Smart cropping

Operation name: scrop.

| Parameter | Description |
| ----------------------------- | ------------------------------------------------------------ |
| /scrop/&lt;Width>x&lt;Height> | Scales and crops an image based on the face position in the image. The width and height of the target image are Width and Height. |

## 3x3 Grid Position Diagram

A 3x3 grid position diagram provides position reference for multiple image operations. Red dots show the origin points of each region. After you use the gravity parameter to select a region, displacement must be based on the corresponding origin point. 
![](https://main.qcloudimg.com/raw/53a143451229b4fbdd74935afe3832d5.png)

>
- When the gravity parameter is set to center, the dx and dy parameters are invalid.
- When the gravity parameter is set to north or south, the dx parameter is invalid, and the watermark is centered horizontally.
- When the gravity parameter is set to west or east, the dy parameter is invalid, and the watermark is centered vertically.



## Example

#### Regular cropping

This example shows you how to horizontally move rightward by 100 pixels and vertically move downward by 10 pixels relative to the upper-left vertex of the image and specify the size of the target image as 600x600 for cropping.

```
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/cut/600x600x100x10
```

The original image is as follows:
![](https://main.qcloudimg.com/raw/becc02d71fb703c2e87ad15e19808bb1.jpeg)

The final effect is as follows:
![](https://main.qcloudimg.com/raw/e28696af6be355cc678284b621a7c97b.jpeg)


<span id="scaling and cropping"></span>

#### Scaling and cropping

This example shows you how to scale and crop an image to 300x400 by using the center as the reference point.

```
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/crop/300x400/gravity/center 
```

The final effect is as follows:
![](https://main.qcloudimg.com/raw/b9adeff300df483c22765b7d746d6690.jpeg)

#### Inscribed circle cropping
This example shows you how to perform inscribed circle cropping when the radius is 300.

```
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/iradius/300
```

The final effect is as follows:
![](https://main.qcloudimg.com/raw/f38ead869790236879a229f2d5f1bafc.jpeg)

#### Rounded corner cropping
This example shows you how to perform rounded corner cropping when the radius is 100.
```
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/rradius/100 
```

The final effect is as follows:
![](https://main.qcloudimg.com/raw/795e0a3254137a5815b9f9f23cecbb91.jpeg)


#### Smart cropping
This example shows you how to scale and crop an image to 100x600 based on the position of the face in the image.

```
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/scrop/100x600
```

> If no face is recognized in the image, the original image is returned.
