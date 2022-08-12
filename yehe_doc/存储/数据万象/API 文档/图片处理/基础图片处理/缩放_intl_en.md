## Feature Overview
CI uses the **imageMogr2** API to scale images. The input image cannot be larger than 32 MB, with its width and height not exceeding 30,000 pixels respectively, and the total number of pixels not exceeding 250 million. The width and height of the output image cannot exceed 9,999 pixels respectively. For an animated input image, the total number of pixels (width * height * number of frames) cannot exceed 250 million.

An image can be processed:

- During download
- During upload
- In the cloud


## API Sample

#### 1. Processing during download

```plaintext
download_url?imageMogr2/thumbnail/<imageSizeAndOffsetGeometry>
```

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

Operation name: thumbnail.

| Parameter | Description |
| ----------------------------- | ------------------------------------------------------------ |
| download_url | URL of the input image in the format of &lt;BucketName-APPID>.cos.&lt;Region>.myqcloud.com/&lt;picture name>; for example, `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg`. |
| /thumbnail/!&lt;Scale>p          | Scales an image to `Scale%` of its original width and height.                             |
| /thumbnail/!&lt;Scale>px         | Scales an image to `Scale%` of its original width while keeping the height unchanged.                     |
| /thumbnail/!x&lt;Scale>p         | Scales an image to `Scale%` of its original height while keeping the width unchanged.                     |
| /thumbnail/&lt;Width>x           | Specifies the target image width as `Width`, with the height proportionally scaled.                    |
| /thumbnail/x&lt;Height>          | Specifies the target image height as `Height`, with the width proportionally scaled.                   |
| /thumbnail/&lt;Width>x&lt;Height>   | Specifies the maximum width and height of a thumbnail as `Width` and `Height` respectively for proportional scaling. |
|  /thumbnail/&lt;Width>x&lt;Height>**>**  |  Specifies the maximum width and height of a thumbnail as `Width` and `Height` respectively for proportional scaling down. The smaller value between the width scale ratio and height scale ratio will be used as the scale ratio. If both the output width and height are greater than the input width and height, the image will not be scaled. |
|  /thumbnail/&lt;Width>x&lt;Height>**<**  |   Specifies the maximum width and height of a thumbnail as `Width` and `Height` respectively for proportional scaling up. The smaller value between the width scale ratio and height scale ratio will be used as the scale ratio. If both the output width and height are less than the input width and height, the image will not be scaled. |
| /thumbnail/!&lt;Width>x&lt;Height>r | Specifies the minimum width and height of a thumbnail as `Width` and `Height` respectively for proportional scaling. |
| /thumbnail/&lt;Width>x&lt;Height>!  | Forces image scaling with the specified `Width` and `Height`, which may cause deformation of the target image. |
| /thumbnail/&lt;Area>@ | Proportionally scales an image so that the total number of its pixels does not exceed `Area`. |
| /pad/ | Pads the blank area with the color specified by `color` after the input image is scaled as large as possible in a rectangle with the specified `Width` and `Height`, with the image centered. Valid values: `0` (not to pad), `1` (to pad). |
| /color/ | Fill color. The value must be in hexadecimal format, such as `#FF0000`. For format conversion, see [RGB Color Codes Chart](https://www.rapidtables.com/web/color/RGB_Color.html). The value must be URL-safe Base64-encoded as described in [FAQs](https://intl.cloud.tencent.com/document/product/1045/33430). Default value: #FFFFFF (white). |
| /ignore-error/1 | If this parameter is carried and the image fails to be processed because the image is too large or a parameter value exceeds the limit, the input image will be returned with no error reported. |

## Samples

>? **Processing during download** is used as an example here, which does not store the output image in a bucket. If you need to store the output image, see [Persistent Image Processing](https://intl.cloud.tencent.com/document/product/1045/33695) and use the **processing during upload** or **processing in-cloud data** feature.
>


Input image:
![](https://main.qcloudimg.com/raw/3d4682ff8e622425ebd29913810a5c38.jpeg)

#### Sample 1: Scaling the width and height

This example scales down the input image by 50% in width and height:
```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/thumbnail/!50p
```

Output image:
![](https://main.qcloudimg.com/raw/2b64595a4a7046dc03f43a2a578764de.jpeg)

#### Sample 2: Scaling the width without changing the height

This example scales down the width of the input image by 50% without changing its height:
```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/thumbnail/!50px
```

Output image:
![](https://main.qcloudimg.com/raw/988ad350c611a662156e34c28aa5f8a2.jpeg)

#### Sample 3: Scaling in padding mode

This example scales the input image as large as possible in a 600x600 rectangle and pads the blank area with a specified color:
```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/thumbnail/600x600/pad/1/color/IzNEM0QzRA
```

Output image:
![](https://main.qcloudimg.com/raw/5f1d9423eaa73e2115fa969667738dee.jpg)

#### Sample 4: Scaling in padding mode with a signature carried

This example processes the image in the same way as in the example above, except that a signature is carried. The signature is concatenated with other processing parameters by an ampersand (&).

```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?q-sign-algorithm=<signature>&imageMogr2/thumbnail/!50px
```

>? You can get the value of `<signature>` as instructed in [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).
>

## Notes

To prevent unauthorized users from accessing or downloading the input image by using a URL that does not contain any processing parameter, you can add the processing parameters to the request signature, making the processing parameters the key of the parameter with the value left empty. The following is a simple sample for your reference (it might have expired or become inaccessible). For more information, see [Upload via Pre-Signed URL](https://intl.cloud.tencent.com/document/product/436/14114).


```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?q-sign-algorithm=sha1&q-ak=AKID********************&q-sign-time=1593342360;1593342720&q-key-time=1593342360;1593342720&q-header-list=&q-url-param-list=watermark%252f1%252fimage%252fahr0cdovl2v4yw1wbgvzlteyntewmdawmdqucgljc2gubxlxy2xvdwquy29tl3nodwl5aw4uanbn%252fgravity%252fsoutheast&q-signature=26a429871963375c88081ef60247c5746e834a98&watermark/1/image/aHR0cDovL2V4YW1wbGVzLTEyNTEwMDAwMDQucGljc2gubXlxY2xvdWQuY29tL3NodWl5aW4uanBn/gravity/southeast
```



