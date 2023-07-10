## Overview
COS uses the **imageMogr2** API provided by CI to rotate an image by a specified angle or automatically.

An image can be processed:

- Upon download
- Upon upload
- In cloud

>! Image processing is charged by CI. For detailed pricing, please see the image processing prices of CI.
>


## Restrictions

- Format: Currently, JPG, BMP, GIF, PNG, and WebP images can be processed, and HEIF images can be decoded and processed.
- Size: The input image cannot be larger than 32 MB, with its width and height not exceeding 30,000 pixels, and the total number of pixels not exceeding 250 million. The width and height of the output image cannot exceed 9,999 pixels. For an input animated image, the total number of pixels (Width x Height x Number of frames) cannot exceed 250 million pixels.
- Number of frames (for animated images): For GIF, the number of frames cannot exceed 300.



## API Format

#### 1. Processing upon download

```plaintext
download_url?imageMogr2/rotate/<rotateDegree>
					   /auto-orient
```

>! Spaces and line breaks above are for readability only and can be ignored.

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
      "rule": "imageMogr2/rotate/<rotateDegree>
					   /auto-orient"
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
      "rule": "imageMogr2/rotate/<rotateDegree>
					   /auto-orient"
  }]
}
```

>? Authorization: Auth String (For more information, please see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).)
>


## Parameters

| Parameter | Description |
| ------------------------- | ------------------------------------------------------------ |
| download_url | URL of the input image, formatted as `&lt;BucketName-APPID>.cos.&lt;Region>.myqcloud.com/&lt;picture name>`<br>Example: `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg` |
| /rotate/&lt;rotateDegree> | Rotates an image clockwise by a specified angle. Value range: 0−360. By default, the image is not rotated. |
| /auto-orient | Auto-rotates an image based on its EXIF orientation tag. |
| /flip/&lt;flip&gt; | Flips an image. Valid values: `vertical`, `horizontal` |
| /ignore-error/1 | If this parameter is carried and the image failed to be processed because it is too large, the input image will be returned with no error reported. |

## Examples

>? **Processing upon download** is used as an example here, which does not store the output image in a bucket. If you need to store the output image, please see [Persistent Image Processing](https://intl.cloud.tencent.com/document/product/436/40592) and use **Processing upon upload** or **Processing in-cloud data**.


#### Example 1: rotating an image by a specified angle
This example rotates an image clockwise by 90 degrees:

```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/rotate/90
```

Output image:
![](https://main.qcloudimg.com/raw/2d47c4f47b8f9c8eca85a3590a106e14.jpeg)

#### Example 2: rotating an image by a specified angle with a signature carried

This example processes the image in the same way as in the example above except that a signature is carried. The signature is joined with other processing parameters using an ampersand (&):

```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?q-sign-algorithm=<signature>&imageMogr2/rotate/90
```

>? You can obtain the value of `<signature>` by referring to [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).
>


## Notes

To prevent unauthorized users from accessing or downloading the input image by using a URL that does not contain any processing parameter, you can add the processing parameters to the request signature, making the processing parameters the key of the parameter with the value left empty. The following is a simple example for your reference (it might have expired or become inaccessible). For more information, please see [Request Signature](https://intl.cloud.tencent.com/document/product/436/14114).

```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?q-sign-algorithm=sha1&q-ak=AKID********************&q-sign-time=1593342360;1593342720&q-key-time=1593342360;1593342720&q-header-list=&q-url-param-list=watermark%252f1%252fimage%252fahr0cdovl2v4yw1wbgvzlteyntewmdawmdqucgljc2gubxlxy2xvdwquy29tl3nodwl5aw4uanbn%252fgravity%252fsoutheast&q-signature=26a429871963375c88081ef60247c5746e834a98&watermark/1/image/aHR0cDovL2V4YW1wbGVzLTEyNTEwMDAwMDQucGljc2gubXlxY2xvdWQuY29tL3NodWl5aW4uanBn/gravity/southeast
```

