## Feature Overview

COS uses the **imageMogr2** API provided by CI to remove image metadata, including EXIF data.

An image can be processed:

- Upon download
- Upon upload
- In cloud

>! Image Processing is charged by CI. For detailed pricing, see **Basic image processing fee** in [Billing and Pricing](https://www.tencentcloud.com/document/product/1045/45582).
>

## Restrictions

- Format: JPG, BMP, GIF, PNG, and WebP images can be processed, and HEIF images can be decoded and processed.
- Static image size: The input image cannot be larger than 32 MB. Its dimensions cannot exceed 50,000 pixels and its resolution cannot exceed 250 million pixels. The dimensions of the output image cannot exceed 50,000 pixels.
- WebP image size: The input image cannot be larger than 32 MB. Its dimensions cannot exceed 16,383 pixels and its resolution cannot exceed 250 million pixels. The dimensions of the output image cannot exceed 16,383 pixels.
- Animated image size: For the input or output image, the total number of pixels (width x height x number of frames) cannot exceed 250 million pixels.
- Number of frames (for animated images): For GIF, the number of frames cannot exceed 300.




## API Format

#### 1. Processing upon download

```plaintext
GET /<ObjectKey>?imageMogr2/strip HTTP/1.1
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
      "rule": "imageMogr2/strip"
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
      "rule": "imageMogr2/strip"
  }]
}
```

>? 
> - Authorization: Auth String (see [Request Signature](https://www.tencentcloud.com/document/product/436/7778) for more information)
> - When this feature is used by a sub-account, relevant permissions must be granted as instructed in [Authorization Granularity Details](https://www.tencentcloud.com/document/product/1045/49896).
> 


## Parameters

Operation: strip

| Parameter       | Description                                                                                                                                        |
| ------------ | ------------------------------------------------------------ |
| ObjectKey  | Object name, such as `folder/sample.jpg`.                           | 
| /ignore-error/1 | If this parameter is carried and the image failed to be processed because it is too large, the input image will be returned with no error reported. |

## Examples


>? **Processing upon download** is used as an example here, which does not store the output image in a bucket. If you need to store the output image, see [Persistent Image Processing](https://www.tencentcloud.com/document/product/436/40592) and use **Processing upon upload** or **Processing in-cloud data**.


#### Example 1: Public-read

```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/strip	
```

#### Example 2: Private-read with a signature carried

This example processes the image in the same way as in the example above except that a signature is carried. The signature is joined with other processing parameters using an ampersand (&).

```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?q-sign-algorithm=<signature>&imageMogr2/strip
```

>? You can obtain the value of `<signature>` by referring to [Request Signature](https://www.tencentcloud.com/document/product/436/7778).
>

## Notes

To prevent unauthorized users from accessing or downloading the input image by using a URL that does not contain any processing parameter, you can add the processing parameters to the request signature, making the processing parameters the key of the parameter with the value left empty. The following is a simple example for your reference (it might not be valid or accessible anymore). For more information, please see [Request Signature](https://www.tencentcloud.com/document/product/436/14114).

```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?q-sign-algorithm=sha1&q-ak=AKID********************&q-sign-time=1593342360;1593342720&q-key-time=1593342360;1593342720&q-header-list=&q-url-param-list=watermark%252f1%252fimage%252fahr0cdovl2v4yw1wbgvzlteyntewmdawmdqucgljc2gubxlxy2xvdwquy29tl3nodwl5aw4uanbn%252fgravity%252fsoutheast&q-signature=26a429871963375c88081ef60247c5746e834a98&watermark/1/image/aHR0cDovL2V4YW1wbGVzLTEyNTEwMDAwMDQucGljc2gubXlxY2xvdWQuY29tL3NodWl5aW4uanBn/gravity/southeast
```


