## Feature Overview
CI uses the **imageMogr2** API to scale images. The input image cannot be larger than 32 MB, with its width and height not exceeding 30,000 pixels, and the total number of pixels not exceeding 250 million. The width and height of the output image cannot exceed 9,999 pixels. For an input animated image, the total number of pixels (Width x Height x Number of frames) cannot exceed 250 million pixels.

An image can be processed:

- Upon download
- Upon upload
- In cloud


## API Format

#### 1. Processing upon download


```plaintext
GET /<ObjectKey>?imageMogr2/thumbnail/<imageSizeAndOffsetGeometry> HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>
```

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
      "rule": "imageMogr2/thumbnail/<imageSizeAndOffsetGeometry>"
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
      "rule": "imageMogr2/thumbnail/<imageSizeAndOffsetGeometry>"
  }]
}
```


## Parameters

Operation: thumbnail

| Parameter | Description |
| ----------------------------- | ------------------------------------------------------------ |
| ObjectKey  | Object name, such as `folder/sample.jpg`.                           | 
| /thumbnail/!&lt;Scale>p | The percentage to scale the width and height of the input image |
| /thumbnail/!&lt;Scale>px | The percentage to scale the width of the input image, without changing the height |
| /thumbnail/!x&lt;Scale>p | The percentage to scale the height of the input image, without changing the width |
| /thumbnail/&lt;Width>x | The width of the output image, with the height scaled automatically |
| /thumbnail/x&lt;Height> | The height of the output image, with the width scaled automatically |
| /thumbnail/&lt;Width>x&lt;Height> | The maximum width and height of the thumbnail for scaling |
|  /thumbnail/&lt;Width>x&lt;Height>**>**  |  Specifies the maximum width and height of a thumbnail as `Width` and `Height` respectively for proportional scaling down. The smaller value between the width scale ratio and height scale ratio will be used as the scale ratio. If both the output width and height are greater than the input width and height, the image will not be scaled. |
|  /thumbnail/&lt;Width>x&lt;Height>**<**  |   Specifies the maximum width and height of a thumbnail as `Width` and `Height` respectively for proportional scaling up. The smaller value between the width scale ratio and height scale ratio will be used as the scale ratio. If both the output width and height are less than the input width and height, the image will not be scaled. |
| /thumbnail/!&lt;Width>x&lt;Height>r | The minimum width and height of the thumbnail for scaling |
| /thumbnail/&lt;Width>x&lt;Height>! | The output width and height with the aspect ratio of the input image ignored. Note that the output image may be distorted. |
| /thumbnail/&lt;Area>@ | The maximum number of pixels of the output image |
| /pad/ | Whether to pad the blank area with the color specified by `color` after the input image is scaled as large as possible in a rectangle with the specified width and height, with the image centered. Valid values: `0` (not to pad), `1` (to pad) |
| /color/ | Fill color. The value must be in hexadecimal format, such as `#FF0000`. For format conversion, see [RGB Color Codes Chart](https://www.rapidtables.com/web/color/RGB_Color.html). The value must be URL-safe Base64-encoded as described in [FAQs](https://intl.cloud.tencent.com/document/product/1045/33430). Default value: #FFFFFF (white). |
| /ignore-error/1 | If this parameter is carried and the image failed to be processed because the image size or the parameter value is too large, the input image will be returned with no error reported. |

## Examples

>? **Processing upon download** is used as an example here, which does not store the output image in a bucket. If you need to store the output image, see [Persistent Image Processing](https://intl.cloud.tencent.com/document/product/1045/33695) and use **Processing upon upload** or **Processing in-cloud data**.
>


Input image:
![](https://main.qcloudimg.com/raw/3d4682ff8e622425ebd29913810a5c38.jpeg)

#### Example 1: scaling the width and height

This example scales down the input image by 50% in width and height:
```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/thumbnail/!50p
```

Output image:
![](https://main.qcloudimg.com/raw/2b64595a4a7046dc03f43a2a578764de.jpeg)

#### Example 2: scaling the width without changing the height

This example scales down the width of the input image by 50% without changing its height:
```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/thumbnail/!50px
```

Output image:
![](https://main.qcloudimg.com/raw/988ad350c611a662156e34c28aa5f8a2.jpeg)

#### Example 3: scaling in padding mode

This example scales the input image as large as possible in a 600 x 600 rectangle and pads the blank area with a specified color:
```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/thumbnail/600x600/pad/1/color/IzNEM0QzRA
```

Output image:
![](https://main.qcloudimg.com/raw/5f1d9423eaa73e2115fa969667738dee.jpg)

#### Example 4: scaling in padding mode with a signature carried

This example processes the image in the same way as in the example above except that a signature is carried. The signature is joined with other processing parameters using an ampersand (&).

```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?q-sign-algorithm=<signature>&imageMogr2/thumbnail/!50px
```

>? You can obtain the value of `<signature>` by referring to [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).
>

## Notes

To prevent unauthorized users from accessing or downloading the input image by using a URL that does not contain any processing parameter, you can add the processing parameters to the request signature, making the processing parameters the key of the parameter with the value left empty. The following is a simple example for your reference (it might have expired or become inaccessible). For more information, see [Upload via Pre-Signed URL](https://intl.cloud.tencent.com/document/product/436/14114).


```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?q-sign-algorithm=sha1&q-ak=AKID********************&q-sign-time=1593342360;1593342720&q-key-time=1593342360;1593342720&q-header-list=&q-url-param-list=watermark%252f1%252fimage%252fahr0cdovl2v4yw1wbgvzlteyntewmdawmdqucgljc2gubxlxy2xvdwquy29tl3nodwl5aw4uanbn%252fgravity%252fsoutheast&q-signature=26a429871963375c88081ef60247c5746e834a98&watermark/1/image/aHR0cDovL2V4YW1wbGVzLTEyNTEwMDAwMDQucGljc2gubXlxY2xvdWQuY29tL3NodWl5aW4uanBn/gravity/southeast
```



