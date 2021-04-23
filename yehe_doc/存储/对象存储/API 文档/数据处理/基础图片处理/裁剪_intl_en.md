## Feature
This API **imageMogr2** from Tencent Cloud CI is used to offer a cropping feature in COS, including regular cropping, scaling and cropping, inscribed circle cropping, rounded corner cropping, and smart cropping.

>Image processing is a paid service, the fees of which are charged by Cloud Infinite. For detailed billing instructions, see Cloud Infinite’s [Billing and Pricing](https://intl.cloud.tencent.com/document/product/1045/33431).

## API Form

```plaintext
download_url?imageMogr2/cut/<width>x<height>x<dx>x<dy>
                       /crop/<imageSizeAndOffsetGeometry>
                       /iradius/<radius>
                       /rradius/<radius>
                       /scrop/<Width>x<Height>
```

>Please ignore the preceding spaces and line breaks.


## Parameter Description

| Parameter         | Description                                                         |
| ------------ | ------------------------------------------------------------ |
| download_url | URL that is used to access a file. Format: `<BucketName-APPID>.cos.<picture region>.<domain>.com/<picture name>`, <br>for example, `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg`. |

#### Regular cropping

Operation name: cut.

| Parameter | Description |
| ----------- | ----------------------------------- |
| &lt;width> | Specifies the target width of the image |
| &lt;height> | Specifies the target height of the image |
| &lt;dx> | Rightward offset (dx) relative to the upper-left vertex of the image |
| &lt;dy> | Downward offset (dy) |


>A valid value is greater than 0, and smaller than the width and height of the original image.


#### Scaling and cropping

Operation name: crop.

| Parameter                         | Description                                                         |
| ---------------------------- | ------------------------------------------------------------ |
| /crop/&lt;Width>x | Specifies the target width of the image while keeping the height unchanged. A valid value is greater than 0 and smaller than the original width. |
| /crop/x&lt;Height> | Specifies the target height of the image while keeping the width unchanged. A valid value is greater than 0 and smaller than the original width. |
| /crop/&lt;Width>x&lt;Height> | Specifies the target width and height of the image. Both valid values are greater than 0 and smaller than the original width. |

With scaling and cropping, you can also use the gravity parameter to specify the start position of the operation. For more information, see the [example of scaling and cropping](#Scaling and cropping).

<span id="1"></span>

#### Inscribed circle cropping

Operation name: iradius.

| Parameter                         | Description                                                         |
| -------------------- | ------------------------------------------------------------ |
| /iradius/&lt;radius> | Inscribed circle cropping. radius indicates the radius of the inscribed circle. The value is an integer that is greater than 0 and smaller than half of the smallest edge of the original image. The center of the inscribed circle is the center of the image. This parameter is not supported when the image format is gif. |

#### Rounded corner cropping

Operation name: rradius.

| Parameter                         | Description                                                         |
| -------------------- | ------------------------------------------------------------ |
|/rradius/&lt;radius&gt;| Rounded corner cropping. `radius` indicates the corner radius of the image. The value is an integer that is greater than 0 and smaller than half of the smallest edge of the original image. The rounded corner is tangent to the edge of the original image. This parameter is not supported when the image format is gif. |



#### Smart cropping

Operation name: scrop.

| Parameter                         | Description                                                         |
| ----------------------------- | ------------------------------------------------------------ |
| /scrop/&lt;Width>x&lt;Height> | Scales and crops an image based on the face position in the image, and with target width and height |

## 3 x 3 Positioning Grid

A 3 x 3 positioning grid provides position reference for multiple image operations. Red dots show the origin points of each region. After you use the gravity parameter to select a region, displacement must be based on the corresponding farthest point. 
![](https://main.qcloudimg.com/raw/53a143451229b4fbdd74935afe3832d5.png)

>
- When the gravity parameter is set to center, the dx and dy parameters are invalid.
- When the gravity parameter is set to north or south, the dx parameter is invalid, and the watermark is centered horizontally.
- When the gravity parameter is set to west or east, the dy parameter is invalid, and the watermark is centered vertically.



## Examples

#### Regular cropping

This example shows you how to crop an image to a target 600 x 600 size by horizontally moving it rightward by 100 pixels relative to the upper-left vertex and vertically downward by 10 pixels:

```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/cut/600x600x100x10
```

The original image:
![](https://main.qcloudimg.com/raw/becc02d71fb703c2e87ad15e19808bb1.jpeg)

The final image:
![](https://main.qcloudimg.com/raw/e28696af6be355cc678284b621a7c97b.jpeg)


<span id="scaling and cropping"></span>

#### Scaling and cropping

This example shows you how to scale and crop an image to 300 x 400 by using the center as the reference point:

```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/crop/300x400/gravity/center 
```

The final image:
![](https://main.qcloudimg.com/raw/b9adeff300df483c22765b7d746d6690.jpeg)

#### Inscribed circle cropping
This example shows you how to crop an image into an inscribed circle with a radius of 300:

```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/iradius/300
```

The final image:
![](https://main.qcloudimg.com/raw/f38ead869790236879a229f2d5f1bafc.jpeg)

#### Rounded corner cropping
This example shows you how to crop an image with rounded corners with a radius of 100.
```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/rradius/100 
```

The final image:
![](https://main.qcloudimg.com/raw/795e0a3254137a5815b9f9f23cecbb91.jpeg)


#### Smart cropping
This example shows you how to scale and crop an image to 100 x 600 based on the face position in the image:

```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/scrop/100x600
```

> If no face is recognized in the image, the original image is returned.
