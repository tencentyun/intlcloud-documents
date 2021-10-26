## Overview
COS uses the **imageMogr2** API provided by CI to crop images, such as regular cropping, scaling and cropping, inscribed circle cropping, rounded corner cropping, and smart cropping.

An image can be processed:

- Upon download
- Upon upload
- In cloud

>! Image processing is charged by CI. For detailed pricing, please see the image processing prices of CI.

## Restrictions

- Format: Currently, JPG, BMP, GIF, PNG, and WebP images can be processed, and HEIF images can be decoded and processed.
- Size: The input image cannot be larger than 32 MB, with its width and height not exceeding 30,000 pixels, and the total number of pixels not exceeding 250 million. The width and height of the output image cannot exceed 9,999 pixels. For an input animated image, the total number of pixels (Width x Height x Number of frames) cannot exceed 250 million pixels.
- Number of frames (for animated images): For GIF, the number of frames cannot exceed 300.


## API Format

#### 1. Processing upon download

```plaintext
download_url?imageMogr2/cut/<width>x<height>x<dx>x<dy>
                       /crop/<imageSizeAndOffsetGeometry>
                       /iradius/<radius>
                       /rradius/<radius>
                       /scrop/<Width>x<Height>
```

>? Spaces and line breaks above are for readability only and can be ignored.

#### 2. Processing upon upload

```plaintext
PUT /<ObjectKey> HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
Pic-Operations: 
{
  "is_pic_info": 1,
  "rules": [{
      "fileid": "exampleobject",
      "rule": "imageMogr2/cut/<width>x<height>x<dx>x<dy>
                       /crop/<imageSizeAndOffsetGeometry>
                       /iradius/<radius>
                       /rradius/<radius>
                       /scrop/<Width>x<Height>"
  }]
}
```

#### 3. Processing in-cloud data

```plaintext
POST /<ObjectKey>?image_process HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Content-length: Size
Authorization: Auth String
Pic-Operations: 
{
  "is_pic_info": 1,
  "rules": [{
      "fileid": "exampleobject",
      "rule": "imageMogr2/cut/<width>x<height>x<dx>x<dy>
                       /crop/<imageSizeAndOffsetGeometry>
                       /iradius/<radius>
                       /rradius/<radius>
                       /scrop/<Width>x<Height>"
  }]
}
```

>? Authorization: Auth String (For more information, please see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).)
>


## Parameters

| Parameter | Description |
| ------------ | ------------------------------------------------------------ |
| download_url | URL of the input image, formatted as `&lt;BucketName-APPID>.cos.&lt;Region>.myqcloud.com/&lt;picture name>`<br>Example: `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg` |
| /ignore-error/1 | If this parameter is carried and the image failed to be processed because it is too large, the input image will be returned with no error reported. |

#### Parameters for regular cropping

Operation name: cut.

| Parameter | Description |
| ----------- | ----------------------------------- |
| &lt;width> | Width of the output image |
| &lt;height> | Height of the output image |
| &lt;dx> | Horizontal offset relative to the upper-left vertex |
| &lt;dy> | Vertical offset relative to the upper-left vertex |


>? The values should be greater than 0 and smaller than the width/height of the input image.
>


#### Parameters for scaling and cropping

Operation name: crop.

| Parameter | Description |
| ---------------------------- | ------------------------------------------------------------ |
| /crop/&lt;Width>x  | Width of the output image with the height unchanged. The value must be greater than 0 and smaller than the width of the input image. |
| /crop/x&lt;Height> | Height of the output image with the width unchanged. The value must be greater than 0 and smaller than the height of the input image. |
| /crop/&lt;Width>x&lt;Height> | Width and height of the output image. The values of width and height should be greater than 0 and smaller than those of the input image, respectively. |

When performing scaling and cropping, you can also use the `gravity` parameter to specify the start position of the operation. For more information, see [Scaling and Cropping](#Scaling and cropping).

<span id="1"></span>

#### Parameters for inscribed circle cropping

Operation name: iradius.

| Parameter | Description |
| -------------------- | ------------------------------------------------------------ |
| /iradius/&lt;radius> | Refers to the inscribed circle cropping feature, where `radius` specifies the radius of the inscribed circle. The value of `radius` is an integer that is greater than 0 and less than half the length of the shorter side of the original image. The center of the inscribed circle is the center of the original image. This parameter is not supported if the image format is GIF. |

#### Parameters for rounded corner cropping

Operation: rradius

| Parameter | Description |
| -------------------- | ------------------------------------------------------------ |
| /rradius/&lt;radius&gt; | Refers to the rounded corner cropping feature, where `radius` specifies the radius of the rounded corner of the image. The value of `radius` is an integer that is greater than 0 and less than half the length of the shorter side of the original image. The rounded corner is tangent to the edge of the original image. This parameter is not supported if the image format is GIF. |



#### Parameters for smart cropping

Operation name: scrop.

| Parameter | Description |
| ----------------------------- | ------------------------------------------------------------ |
| /scrop/&lt;Width>x&lt;Height> | Refers to scaling and cropping based on the location of the human face in the image. `Width` and `Height` respectively specify the width and the height of the target image. |

## 3x3 Grid Position Diagram

The 3x3 grid position diagram is as follows. Once you specify the `gravity` parameter for an operation, the corresponding red dot becomes the reference point, and offsets will be relative to this point. 
![](https://main.qcloudimg.com/raw/53a143451229b4fbdd74935afe3832d5.png)

>!
> - If `gravity` is set to `center`, `dx` and `dy` are invalid.
> - If `gravity` is set to `north` or `south`, `dx` is invalid.
> - If `gravity` is set to `west` or `east`, `dy` is invalid.
> 


## Examples

>? **Processing upon download** is used as an example here, which does not store the output image in a bucket. If you need to store the output image, please see [Persistent Image Processing](https://intl.cloud.tencent.com/document/product/436/40592) and use **Processing upon upload** or **Processing in-cloud data**.


#### Example 1: regular cropping

This example shows how to translate by 100 pixels horizontally to the right and 10 pixels vertically to the bottom relative to the top-left vertex of the image. It also shows how to crop the image according to the specified target image resolution of 600 × 600 pixels:

```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/cut/600x600x100x10
```

Input image:
![](https://main.qcloudimg.com/raw/becc02d71fb703c2e87ad15e19808bb1.jpeg)

Output image:
![](https://main.qcloudimg.com/raw/e28696af6be355cc678284b621a7c97b.jpeg)


<span id="scaling and cropping"></span>

#### Example 2: scaling and cropping

This example shows you how to scale and crop an image to 300x400 by using the center as the reference point.

```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/crop/300x400/gravity/center 
```

Output image:
![](https://main.qcloudimg.com/raw/b9adeff300df483c22765b7d746d6690.jpeg)

#### Example 3: inscribed circle cropping

This example shows you how to perform inscribed circle cropping when the radius is 200.

```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/iradius/200
```

Output image:
![](https://main.qcloudimg.com/raw/1e449274ea00eebc87454168e7056abc.jpeg)

#### Example 4: rounded corner cropping
This example shows you how to perform rounded corner cropping when the radius is 100.
```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/rradius/100 
```

Output image:
![](https://main.qcloudimg.com/raw/795e0a3254137a5815b9f9f23cecbb91.jpeg)


#### Example 5: smart cropping
This example shows how to crop an image to the specified resolution of 100 × 600 pixels based on the location of the human face in the image:

```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/scrop/100x600
```

>?If no face is recognized, the input image will be returned.

#### Example 6: smart cropping with a signature carried

This example processes the image in the same way as in the example above except that a signature is carried. The signature is joined with other processing parameters using an ampersand (&):

```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?q-sign-algorithm=<signature>&imageMogr2/scrop/100x600
```

> ? You can obtain the value of `<signature>` by referring to [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).

## Notes

To prevent unauthorized users from accessing or downloading the input image by using a URL that does not contain any processing parameter, you can add the processing parameters to the request signature, making the processing parameters the key of the parameter with the value left empty. The following is a simple example for your reference (it might have expired or become inaccessible). For more information, please see [Request Signature](https://intl.cloud.tencent.com/document/product/436/14114).


```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?q-sign-algorithm=sha1&q-ak=AKID********************&q-sign-time=1593342360;1593342720&q-key-time=1593342360;1593342720&q-header-list=&q-url-param-list=watermark%252f1%252fimage%252fahr0cdovl2v4yw1wbgvzlteyntewmdawmdqucgljc2gubxlxy2xvdwquy29tl3nodwl5aw4uanbn%252fgravity%252fsoutheast&q-signature=26a429871963375c88081ef60247c5746e834a98&watermark/1/image/aHR0cDovL2V4YW1wbGVzLTEyNTEwMDAwMDQucGljc2gubXlxY2xvdWQuY29tL3NodWl5aW4uanBn/gravity/southeast
```


