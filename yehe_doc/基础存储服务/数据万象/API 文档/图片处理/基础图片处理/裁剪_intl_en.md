## Feature Overview
CI uses the **imageMogr2** API to crop images, including regular cropping, scaling and cropping, cropping to circle, rounded corner cropping, and smart face cropping.

An image can be processed:
- During download
- During upload
- In the cloud


## Restrictions

- Format: Currently, JPG, BMP, GIF, PNG, and WebP images can be processed, and HEIF images can be decoded and processed.
- Size: The input image cannot be larger than 32 MB, with its width and height not exceeding 30,000 pixels respectively, and the total number of pixels not exceeding 250 million. The width and height of the output image cannot exceed 9,999 pixels respectively. For an animated input image, the total number of pixels (width * height * number of frames) cannot exceed 250 million.
- Frames (for animated images): For GIF images, the number of frames cannot exceed 300.


## API Sample

#### 1. Processing during download


```plaintext
GET /<ObjectKey>?imageMogr2/cut/<width>x<height>x<dx>x<dy>
                           /crop/<imageSizeAndOffsetGeometry>
                           /iradius/<radius>
                           /rradius/<radius>
                           /scrop/<Width>x<Height> HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>
```

>? Spaces and line breaks above are for readability only and can be ignored.
>

#### 2. Processing during upload

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

>? `Pic-Operations` is a JSON string. Its parameters are as described in [Persistent Image Processing](https://intl.cloud.tencent.com/document/product/1045/33695).
>


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


>? 
> - Authorization: Auth String (for more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).
> - When this feature is used by a sub-account, relevant permissions must be granted. For more information, see [Authorization Granularity Details](https://intl.cloud.tencent.com/document/product/1045/49896).
> 



## Parameters

| Parameter | Description |
| ------------ | ------------------------------------------------------------ |
| ObjectKey  | Object name, such as `folder/sample.jpg`.                           | 
| /ignore-error/1 | If this parameter is carried and the image fails to be processed because the image is too large or a parameter value exceeds the limit, the input image will be returned with no error reported. |

#### Parameters for regular cropping

Operation name: cut.

| Parameter | Description |
| ----------- | ----------------------------------- |
| &lt;width> | Width of the output image |
| &lt;height> | Height of the output image |
| &lt;dx> | Horizontal offset relative to the top-left vertex |
| &lt;dy> | Vertical offset relative to the top-left vertex |


>? The values should be greater than 0 and smaller than the width/height of the input image.
>


#### Parameters for scaling and cropping

Operation name: crop.

| Parameter | Description |
| ---------------------------- | ------------------------------------------------------------ |
| /crop/&lt;Width>x  | Width of the output image with the height unchanged. The value must be greater than 0 and smaller than the width of the input image. |
| /crop/x&lt;Height> | Height of the output image with the width unchanged. The value must be greater than 0 and smaller than the height of the input image. |
| /crop/&lt;Width>x&lt;Height> | Width and height of the output image. The values of width and height should be greater than 0 and smaller than those of the input image, respectively. |

When performing scaling and cropping, you can also use the `gravity` parameter to specify the start position of the operation. For more information, see [Scaling and cropping](#Scaling and cropping).

<span id="1"></span>

#### Parameters for cropping to circle

Operation name: iradius.

| Parameter | Description |
| -------------------- | ------------------------------------------------------------ |
| /iradius/&lt;radius> | Crops to a circle. `radius` specifies the radius of the inscribed circle, which should be an integer greater than zero and less than half of the shorter side of the input image. The center of the inscribed circle is the center of the image. This operation is not supported for GIF images. |

#### Parameters for rounded corner cropping

Operation name: rradius.

| Parameter | Description |
| -------------------- | ------------------------------------------------------------ |
|/rradius/&lt;radius&gt;|  Crops with round corners. `radius` specifies the radius of the rounded corner of the image, which should be an integer greater than zero and less than half of the shorter side of the input image. The two sides of the image are the tangent lines of the rounded corner. This operation is not supported for GIF images. |



#### Parameters for smart face cropping

Operation name: scrop.

| Parameter | Description |
| ----------------------------- | ------------------------------------------------------------ |
| /scrop/&lt;Width>x&lt;Height> | Scales and crops an image based on the face position in the image. The width and height of the target image are specified by `Width` and `Height` respectively. |

## 3x3 Grid Position Diagram

The 3x3 grid position diagram is as follows. Once you specify the `gravity` parameter for an operation, the corresponding red dot becomes the reference point, and offsets will be relative to this point. 
![](https://main.qcloudimg.com/raw/53a143451229b4fbdd74935afe3832d5.png)

>!
> - If `gravity` is set to `center`, `dx` and `dy` are invalid.
> - If `gravity` is set to `north` or `south`, `dx` is invalid.
> - If `gravity` is set to `west` or `east`, `dy` is invalid.
> 


## Samples

>? **Processing during download** is used as an example here, which does not store the output image in a bucket. If you need to store the output image, see [Persistent Image Processing](https://intl.cloud.tencent.com/document/product/1045/33695) and use the **processing during upload** or **processing in-cloud data** feature.


#### Sample 1: Regular cropping

This example shows how to translate by 100 px horizontally to the right and 10 px vertically to the bottom relative to the top-left vertex of the input image and then crop it according to the specified target image resolution of 600x600 px.

```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/cut/600x600x100x10
```

Input image:
![](https://main.qcloudimg.com/raw/becc02d71fb703c2e87ad15e19808bb1.jpeg)

Output image:
![](https://main.qcloudimg.com/raw/e28696af6be355cc678284b621a7c97b.jpeg)


<span id="Scaling and cropping"></span>

#### Sample 2: Scaling and cropping

This example shows how to scale and crop an image to 300x400 px by using the center as the reference point.

```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/crop/300x400/gravity/center 
```

Output image:
![](https://main.qcloudimg.com/raw/b9adeff300df483c22765b7d746d6690.jpeg)

#### Sample 3: Cropping to circle

This example shows how to crop the input image to a circle with the radius of 200.

```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/iradius/200
```

Output image:
![](https://main.qcloudimg.com/raw/1e449274ea00eebc87454168e7056abc.jpeg)

#### Sample 4: Rounded corner cropping
This example shows how to crop the input image to rounded corners with the radius of 100.
```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/rradius/100 
```

Output image:
![](https://main.qcloudimg.com/raw/795e0a3254137a5815b9f9f23cecbb91.jpeg)


#### Sample 5: Smart face cropping
This example shows how to crop the input image to the specified resolution of 100x600 px based on the face position in the image.

```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/scrop/100x600
```

>?If no face is recognized, the input image will be returned.

#### Sample 6: Smart face cropping with a signature carried

This example processes the image in the same way as in the example above, except that a signature is carried. The signature is concatenated with other processing parameters by an ampersand (&).

```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?q-sign-algorithm=<signature>&imageMogr2/scrop/100x600
```

>? You can get the value of `<signature>` as instructed in [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).

## Notes

To prevent unauthorized users from accessing or downloading the input image by using a URL that does not contain any processing parameter, you can add the processing parameters to the request signature, making the processing parameters the key of the parameter with the value left empty. The following is a simple sample for your reference (it might have expired or become inaccessible). For more information, see [Upload via Pre-Signed URL](https://intl.cloud.tencent.com/document/product/436/14114).


```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?q-sign-algorithm=sha1&q-ak=AKID********************&q-sign-time=1593342360;1593342720&q-key-time=1593342360;1593342720&q-header-list=&q-url-param-list=watermark%252f1%252fimage%252fahr0cdovl2v4yw1wbgvzlteyntewmdawmdqucgljc2gubxlxy2xvdwquy29tl3nodwl5aw4uanbn%252fgravity%252fsoutheast&q-signature=26a429871963375c88081ef60247c5746e834a98&watermark/1/image/aHR0cDovL2V4YW1wbGVzLTEyNTEwMDAwMDQucGljc2gubXlxY2xvdWQuY29tL3NodWl5aW4uanBn/gravity/southeast
```


