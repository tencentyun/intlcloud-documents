## Feature Overview
COS implements image watermarking using the **watermark** API provided by CI, and thus only images stored in CI-bound buckets can be processed.

An image can be processed:

- Upon download
- Upon upload
- In cloud

## Restrictions

- Format: JPG, BMP, GIF, PNG, and WebP images can be processed, and HEIF images can be decoded and processed.
- Static image size: The input image cannot be larger than 32 MB. Its dimensions cannot exceed 50,000 pixels and its resolution cannot exceed 250 million pixels. The dimensions of the output image cannot exceed 50,000 pixels.
- WebP image size: The input image cannot be larger than 32 MB. Its dimensions cannot exceed 16,383 pixels and its resolution cannot exceed 250 million pixels. The dimensions of the output image cannot exceed 16,383 pixels.
- Animated image size: For the input or output image, the total number of pixels (width x height x number of frames) cannot exceed 250 million pixels.
- Number of frames (for animated images): For GIF, the number of frames cannot exceed 300.



>? 
> - Image Processing is charged by CI. For detailed pricing, see [Image Processing Fees](https://www.tencentcloud.com/document/product/1045/45582).
> - You can overlay up to 10 image watermarks over a single image.
> - An animated image cannot be used as a watermark.
> 

## API Format

#### 1. Processing upon download

```plaintext
GET /<ObjectKey>?watermark/1/image/<encodedURL>
           		 	/gravity/<gravity>
           		 	/dx/<dx>
           		 	/dy/<dy>
           		 	/blogo/<type> HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>
```

> ? Spaces and line breaks above are for readability only and can be ignored.

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
      "rule": "watermark/1/image/<encodedURL>
           		 	/gravity/<gravity>
           		 	/dx/<dx>
           		 	/dy/<dy>
           		 	/blogo/<type>"
  }]
}
```

>? `Pic-Operations` is a JSON string. Its parameters are as described in [Persistent Image Processing](https://www.tencentcloud.com/document/product/1045/33695).
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
      "rule": "watermark/1/image/<encodedURL>
           		 	/gravity/<gravity>
           		 	/dx/<dx>
           		 	/dy/<dy>
           		 	/blogo/<type>"
  }]
}
```

>? 
> - Authorization: Auth String (see [Request Signature](https://www.tencentcloud.com/document/product/436/7778) for more information)
> - When this feature is used by a sub-account, relevant permissions must be granted as instructed in [Authorization Granularity Details](https://www.tencentcloud.com/document/product/1045/49896).
> 

## Parameters

In the code above, `watermark` is the operation name and the number `1` indicates that the watermark is an image.

| Parameter       | Description                                                                                                                                        |
| ------------ | ------------------------------------------------------------ |
| ObjectKey  | Object name, such as `folder/sample.jpg`.                           |
| /image/ | [Base64 URL-safe encoded](https://www.tencentcloud.com/document/product/1045/54397) URL of the image watermark. For example, if the image watermark URL is `http://examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/shuiyin_2.png`, you should set this parameter to `aHR0cDovL2V4YW1wbGVidWNrZXQtMTI1MDAwMDAwMC5jb3MuYXAtc2hhbmdoYWkubXlxY2xvdWQuY29tL3NodWl5aW5fMi5wbmc`. |
| /gravity/    | Position of the image watermark, which is a square in a [3x3 grid](#1). Default value: `SouthEast` |
| /dx/ | Horizontal offset in pixels. Default value: `0` |
| /dy/ | Vertical offset in pixels. Default value: `0` |
| /blogo/ | Adaptation mode for an image watermark that is larger than the input image. Valid values: <br><li>`1`: scales the image watermark to the size of the input image. <br><li>`2`: crops the image watermark to the size of the input image. |
| /scatype/    | Scaling mode for the image watermark (relative to the input image). This parameter must be used together with `/spcent/`. Valid values: <br><li>`1`: scales by width.<br><li>`2`: scales by height.<br><li>`3`: scales by area. </li> |
| /spcent/ | Scale ratio of the image watermark, in permillage. This parameter must be used together with `/scatype/`. Value range: <li>1−1000 (if `/scatype/` is set to `1`) </li><li>1−1000 (if `/scatype/` is set to `2`)</li><li>1−250 (if `/scatype/` is set to `3`) <br>Example: `http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?watermark/1/image/xxxxxxx/scatype/3/spcent/250`</li> |
| /dissolve/ | Opacity of the image watermark. Value range: 1−100. Default value: `90` (meaning 90% opacity) |
| /batch/ | Whether to tile the image watermark. If this parameter is set to `1`, the image watermark will be tiled across the input image. |
| /degree/ | Angle to rotate the image watermark. This parameter is valid only when `/batch/` is set to `1`. Value range: 0−360. Default value: `0` |

>! An image watermark must:  
> - Be stored in the same bucket as the input image.
> - Have a URL containing a COS domain name (a CDN acceleration domain name such as `examplebucket-1250000000.file.myqcloud.com/shuiyin_2.png` is unsupported) and be accessible (if the image watermark is set to private-read, it must carry a signature).
> - Have a URL starting with `http://`. Note that “http://” cannot be omitted or changed to “https://”. For example, `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/shuiyin_2.png` and `https://examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/shuiyin_2.png` are invalid watermark URLs.


<span id="1"></span>
## 3x3 Grid Position Diagram

The 3x3 grid position diagram is as follows. Once you specify the `gravity` parameter for an operation, the corresponding red dot becomes the reference point, and offsets will be relative to this point. 
![](https://main.qcloudimg.com/raw/53a143451229b4fbdd74935afe3832d5.png)

>?
> - If `gravity` is set to `center`, `dx` and `dy` are invalid.
> - If `gravity` is set to `north` or `south`, `dx` is invalid.
> - If `gravity` is set to `west` or `east`, `dy` is invalid.
> 

## Examples

>? **Processing upon download** is used as an example here, which does not store the output image in a bucket. If you need to store the output image, see [Persistent Image Processing](https://www.tencentcloud.com/document/product/436/40592) and use **Processing upon upload** or **Processing in-cloud data**.
>


#### Example 1: Adding an image watermark

```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?watermark/1/image/aHR0cDovL2V4YW1wbGVzLTEyNTEwMDAwMDQucGljc2gubXlxY2xvdWQuY29tL3NodWl5aW4uanBn/gravity/southeast
```

After an image watermark is added:
![](https://main.qcloudimg.com/raw/6412c0d6eaaadc5c193515f40d736dad.jpeg)

#### Example 2: Adding an image watermark with the tile mode and opacity specified

```plaintext
https://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?watermark/1/image/aHR0cDovL2V4YW1wbGVzLTEyNTEwMDAwMDQucGljc2gubXlxY2xvdWQuY29tL3NodWl5aW4uanBn/gravity/southeast/batch/1/degree/45/dissolve/40/
```

The effect of an added image watermark rotated by 45 degrees and tiled with 40% opacity is as follows:
![](https://qcloudimg.tencent-cloud.cn/raw/d7e49b9cf7ea1dcc0459b2a5e3b2af8d.jpg)

#### Example 3: Adding an image watermark with a signature carried

This example processes the image in the same way as in the example above except that a signature is carried. The signature is joined with other processing parameters using an ampersand (&).

```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?q-sign-algorithm=<signature>&watermark/1/image/aHR0cDovL2V4YW1wbGVzLTEyNTEwMDAwMDQucGljc2gubXlxY2xvdWQuY29tL3NodWl5aW4uanBn/gravity/southeast
```

>? You can obtain the value of `<signature>` by referring to [Request Signature](https://www.tencentcloud.com/document/product/436/7778).
>

## Notes

To prevent unauthorized users from accessing or downloading the input image by using a URL that does not contain any processing parameter, you can add the processing parameters to the request signature, making the processing parameters the key of the parameter with the value left empty. The following is a simple example for your reference (it might not be valid or accessible anymore). For more information, please see [Request Signature](https://www.tencentcloud.com/document/product/436/14114).


```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?q-sign-algorithm=sha1&q-ak=AKID********************&q-sign-time=1593342360;1593342720&q-key-time=1593342360;1593342720&q-header-list=&q-url-param-list=watermark%252f1%252fimage%252fahr0cdovl2v4yw1wbgvzlteyntewmdawmdqucgljc2gubxlxy2xvdwquy29tl3nodwl5aw4uanbn%252fgravity%252fsoutheast&q-signature=26a429871963375c88081ef60247c5746e834a98&watermark/1/image/aHR0cDovL2V4YW1wbGVzLTEyNTEwMDAwMDQucGljc2gubXlxY2xvdWQuY29tL3NodWl5aW4uanBn/gravity/southeast
```

