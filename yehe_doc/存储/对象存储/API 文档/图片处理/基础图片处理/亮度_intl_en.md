## Feature Overview
CI uses the **imageMogr2** API to adjust the brightness of an image.

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
GET /<ObjectKey>?imageMogr2/bright/<value> HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>
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
      "rule": "imageMogr2/bright/<value>"
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
      "rule": "imageMogr2/bright/<value>"
  }]
}
```


>? 
> - Authorization: Auth String (for more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).
> - When this feature is used by a sub-account, relevant permissions must be granted. For more information, see [Authorization Granularity Details](https://intl.cloud.tencent.com/document/product/1045/49896).
> 


## Parameters

Operation name: bright.

| Parameter | Description |
| ---------------- | ------------------------------------------------------------ |
| ObjectKey  | Object name, such as `folder/sample.jpg`.                           | 
| bright/&lt;value> | Adjusts the brightness of an image. The value must be an integer in the range of [-100, 100]. <br><li>`value` < 0: Reduces the image brightness. </li><li>`value` = 0: Does not adjust the image brightness. </li><li>`value` > 0: Increases the image brightness. </li> |
| /ignore-error/1 | If this parameter is carried and the image fails to be processed because the image is too large or a parameter value exceeds the limit, the input image will be returned with no error reported. |

## Samples

>? **Processing during download** is used as an example here, which does not store the output image in a bucket. If you need to store the output image, see [Persistent Image Processing](https://intl.cloud.tencent.com/document/product/1045/33695) and use the **processing during upload** or **processing in-cloud data** feature.
>


#### Sample 1: Adjusting the brightness

This example increases the brightness of an image by 70:

```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/bright/70
```

Output image:

![](https://main.qcloudimg.com/raw/f0fac36084c6d6709ad832c91752ee28.jpg)	
  
#### Sample 2: Adjusting the brightness with a signature carried

This example processes the image in the same way as in the example above, except that a signature is carried. The signature is concatenated with other processing parameters by an ampersand (&).

```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?q-sign-algorithm=<signature>&imageMogr2/bright/70
```

>? You can get the value of `<signature>` as instructed in [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).
>

## Notes

To prevent unauthorized users from accessing or downloading the input image by using a URL that does not contain any processing parameter, you can add the processing parameters to the request signature, making the processing parameters the key of the parameter with the value left empty. The following is a simple sample for your reference (it might have expired or become inaccessible). For more information, see [Upload via Pre-Signed URL](https://intl.cloud.tencent.com/document/product/436/14114).

```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?q-sign-algorithm=sha1&q-ak=AKID********************&q-sign-time=1593342360;1593342720&q-key-time=1593342360;1593342720&q-header-list=&q-url-param-list=watermark%252f1%252fimage%252fahr0cdovl2v4yw1wbgvzlteyntewmdawmdqucgljc2gubxlxy2xvdwquy29tl3nodwl5aw4uanbn%252fgravity%252fsoutheast&q-signature=26a429871963375c88081ef60247c5746e834a98&watermark/1/image/aHR0cDovL2V4YW1wbGVzLTEyNTEwMDAwMDQucGljc2gubXlxY2xvdWQuY29tL3NodWl5aW4uanBn/gravity/southeast
```



