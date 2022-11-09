## Feature Overview
CI uses the **imageMogr2** API to perform format conversion, GIF optimization, and progressive display.

An image can be processed:

- During download
- During upload
- In the cloud

## Restrictions

- Animated image formats such as GIF, WebP, and TPG can be interconverted.
- Static image formats such as JPG, PNG, BMP, TPG, and HEIF can be interconverted.


## API Format

#### 1. Processing during download

```plaintext
GET /<ObjectKey>?imageMogr2/format/<Format>
			   /cgif/<FrameNumber>
			   /interlace/<Mode> HTTP/1.1
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
      "rule": "imageMogr2/format/<Format>
					   /cgif/<FrameNumber>
					   /interlace/<Mode>"
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
      "rule": "imageMogr2/format/<Format>
					   /cgif/<FrameNumber>
					   /interlace/<Mode>"
  }]
}
```


>? 
> - Authorization: Auth String (for more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).
> - When this feature is used by a sub-account, relevant permissions must be granted. For more information, see [Authorization Granularity Details](https://intl.cloud.tencent.com/document/product/1045/49896).
> 


## Parameters

| Parameter | Description |
| -------------------- | ------------------------------------------------------------ |
| ObjectKey  | Object name, such as `folder/sample.jpg`.                           | 
| /format/&lt;Format>  | Converts the image format. The target format can be JPG, BMP, GIF, PNG, WebP, or YJPEG (which is optimized based on JPEG and is essentially JPG). The default format is the format of the input image. |
| /cgif/&lt;FrameNumber&gt;  | Optimizes images in the GIF format by reducing frames and colors of images. There are two cases: <li>FrameNumber=1: Cut the input GIF to the default number of frames (30). If the original number of frames is greater than 30, excessive frames will be cut. </li><li>FrameNumber=(1,100]: Compress the image to the specified number of frames (`FrameNumber`).</li> |
| /interlace/&lt;Mode> | Progressive mode of the output JPG image. Valid values: <br>`0` (default value): Disables the progressive mode. <br>`1`: Enables the progressive mode. <br>This parameter takes effect only when the output image is in JPG format. |
| /ignore-error/1 | If this parameter is carried and the image fails to be processed because the image is too large or a parameter value exceeds the limit, the input image will be returned with no error reported. |


## Samples

>? **Processing during download** is used as an example here, which does not store the output image in a bucket. If you need to store the output image, see [Persistent Image Processing](https://intl.cloud.tencent.com/document/product/1045/33695) and use the **processing during upload** or **processing in-cloud data** feature.
>


#### Sample 1: Converting a JPEG image to PNG format

```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/format/png
```

#### Sample 2: Converting a JPEG image to PNG format with a signature carried

This example processes the image in the same way as in the example above, except that a signature is carried. The signature is concatenated with other processing parameters by an ampersand (&).

```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?q-sign-algorithm=<signature>&imageMogr2/format/png
```

>? You can get the value of `<signature>` as instructed in [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).
>

## Notes

To prevent unauthorized users from accessing or downloading the input image by using a URL that does not contain any processing parameter, you can add the processing parameters to the request signature, making the processing parameters the key of the parameter with the value left empty. The following is a simple sample for your reference (it might have expired or become inaccessible). For more information, see [Upload via Pre-Signed URL](https://intl.cloud.tencent.com/document/product/436/14114).


```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?q-sign-algorithm=sha1&q-ak=AKID********************&q-sign-time=1593342360;1593342720&q-key-time=1593342360;1593342720&q-header-list=&q-url-param-list=watermark%252f1%252fimage%252fahr0cdovl2v4yw1wbgvzlteyntewmdawmdqucgljc2gubxlxy2xvdwquy29tl3nodwl5aw4uanbn%252fgravity%252fsoutheast&q-signature=26a429871963375c88081ef60247c5746e834a98&watermark/1/image/aHR0cDovL2V4YW1wbGVzLTEyNTEwMDAwMDQucGljc2gubXlxY2xvdWQuY29tL3NodWl5aW4uanBn/gravity/southeast
```


	
