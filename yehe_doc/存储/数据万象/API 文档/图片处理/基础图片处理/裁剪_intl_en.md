## Overview
CI uses the `imageMogr2` API to crop images, such as regular cropping, scaling and cropping, inscribed circle cropping, rounded corner cropping, and smart cropping.

## API Format

```plaintext
download_url?imageMogr2/cut/<width>x<height>x<dx>x<dy>
                       /crop/<imageSizeAndOffsetGeometry>
                       /iradius/<radius>
                       /rradius/<radius>
                       /scrop/<Width>x<Height>
```

>? Spaces and line breaks above are for readability only and can be ignored.
>


## Parameters

| Parameter | Description |
| ------------ | ------------------------------------------------------------ |
| download_url | URL of the input image, formatted as `<BucketName-APPID>.cos.<picture region>.<domain>.com/<picture name>`<br>Example: `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg` |
| /ignore-error/1 | If this parameter is carried and the image failed to be processed because it is too large, the input image will be returned with no error reported. |

#### Regular cropping

Operation name: cut.

| Parameter | Description |
| ----------- | ----------------------------------- |
| &lt;width> | Width of the output image |
| &lt;height> | Height of the output image |
| &lt;dx> | Horizontal offset with respect to the upper-left vertex |
| &lt;dy> | Vertical offset with respect to the upper-left vertex |


>? The values should be greater than 0 and smaller than the width/height of the input image.
>


#### Scaling and cropping

Operation name: crop.

| Parameter | Description |
| ---------------------------- | ------------------------------------------------------------ |
| /crop/&lt;Width>x  | Width of the output image with the height unchanged. The value must be greater than 0 and smaller than the width of the input image. |
| /crop/x&lt;Height> | Height of the output image with the width unchanged. The value must be greater than 0 and smaller than the height of the input image. |
| /crop/&lt;Width>x&lt;Height> | Width and height of the output image. The values of width and height should be greater than 0 and smaller than that of the input image, respectively. |

During the crop operation, you can also use the `gravity` parameter to specify the location of the start point. For more information, see the [example of the scaling and cropping](#Crop).

<span id="1"></span>

#### Inscribed circle cropping

Operation name: iradius.

| Parameter | Description |
| -------------------- | ------------------------------------------------------------ |
| /iradius/&lt;radius> | Inscribed circle cropping. radius indicates the radius of the inscribed circle. The value is an integer that is greater than 0 and smaller than half of the smallest edge of the input image. The center of the inscribed circle is the center of the image. This parameter is not supported when the image format is GIF. |

#### Rounded corner cropping

Operation name: rradius

| Parameter | Description |
| -------------------- | ------------------------------------------------------------ |
|/rradius/<radius>| Rounded corner cropping. radius indicates the rounded corner edge radius of the image. The value is an integer that is greater than 0 and smaller than half of the smallest edge of the original image. The rounded corner is tangent to the edge of the original image. This parameter is not supported when the image format is gif. |



#### Smart cropping

Operation name: scrop.

| Parameter | Description |
| ----------------------------- | ------------------------------------------------------------ |
| /scrop/<Width>x<Height> | Scales and crops an image based on the face position in the image. The width and height of the target image are Width and Height. |

## 3x3 Grid Position Diagram

The 3x3 grid position diagram is as follows. Once you specify the `gravity` parameter to position your watermark, the corresponding red dot becomes the reference point of the square, and offsets will be relative to this point. 
![](https://main.qcloudimg.com/raw/53a143451229b4fbdd74935afe3832d5.png)

>!
> - If `gravity` is set to `center`, `dx` and `dy` are invalid.
> - If `gravity` is set to `north` or `south`, `dx` is invalid and the watermark will be centered horizontally.
> - If `gravity` is set to `west` or `east`, `dy` is invalid and the watermark will be centered vertically.
> 



## Example

#### Regular cropping

This example shows you how to horizontally move rightward by 100 pixels and vertically move downward by 10 pixels relative to the upper-left vertex of the image and specify the size of the target image as 600x600 for cropping.

```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/cut/600x600x100x10
```

Input image:
![](https://main.qcloudimg.com/raw/becc02d71fb703c2e87ad15e19808bb1.jpeg)

Output image:
![](https://main.qcloudimg.com/raw/e28696af6be355cc678284b621a7c97b.jpeg)


<span id="scaling and cropping"></span>

#### Scaling and cropping

This example shows you how to scale and crop an image to 300x400 by using the center as the reference point.

```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/crop/300x400/gravity/center 
```

Output image:
![](https://main.qcloudimg.com/raw/b9adeff300df483c22765b7d746d6690.jpeg)

#### Inscribed circle cropping

This example shows you how to perform inscribed circle cropping when the radius is 200.

```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/iradius/200
```

Output image:
![](https://main.qcloudimg.com/raw/1e449274ea00eebc87454168e7056abc.jpeg)

#### Rounded corner cropping
This example shows you how to perform rounded corner cropping when the radius is 100.
```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/rradius/100 
```

Output image:
![](https://main.qcloudimg.com/raw/795e0a3254137a5815b9f9f23cecbb91.jpeg)


#### Smart cropping
This example shows you how to scale and crop an image to 100x600 based on the face position in the image.

```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/scrop/100x600
```

>?If no face is recognized, the input image will be returned.

#### Smart cropping with a signature carried

This example processes the image as the example above but also adds a signature, which is joined with other processing parameters using an ampersand (&):

```
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?q-sign-algorithm=<signature>&imageMogr2/scrop/100x600
```

> ? You can obtain the value of `<signature>` by referring to [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).

