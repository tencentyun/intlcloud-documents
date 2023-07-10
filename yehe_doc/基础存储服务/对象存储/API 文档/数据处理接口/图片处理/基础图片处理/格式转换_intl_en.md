## Overview
COS uses the **imageMogr2** API provided by CI to perform format conversion, GIF optimization, and progressive display.

An image can be processed:

- Upon download
- Upon upload
- In cloud

>! Image processing is charged by CI. For detailed pricing, please see the image processing prices of CI.
>

## Restrictions

- Animated image formats such as GIF, WebP, and TPG can be interconverted.
- Static image formats such as JPG, PNG, BMP, TPG, and HEIF can be interconverted.



## API Format

#### 1. Processing upon download

```plaintext
download_url?imageMogr2/format/<Format>
					   /cgif/<FrameNumber>
					   /interlace/<Mode>
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
      "rule": "imageMogr2/format/<Format>
					   /cgif/<FrameNumber>
					   /interlace/<Mode>"
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
      "rule": "imageMogr2/format/<Format>
					   /cgif/<FrameNumber>
					   /interlace/<Mode>"
  }]
}
```

>? Authorization: Auth String (For more information, please see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).)
>

## Parameters

| Parameter | Description |
| -------------------- | ------------------------------------------------------------ |
| download_url | URL of the input image, formatted as `&lt;BucketName-APPID>.cos.&lt;Region>.myqcloud.com/&lt;picture name>`<br>Example: `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg` |
| /format/<Format> | Converts the image format. The target format can be JPG, BMP, GIF, PNG, WebP, or YJPEG (a JPEG-based format optimized by CI). Default format: format of the input image |
| /cgif/&lt;FrameNumber&gt; | Optimizes a GIF image by reducing the number of frames and colors. Valid values of `FrameNumber`: <li>`1`: cuts the input GIF to the default number of frames (30). If the original number of frames is greater than 30, the exceeded frames will be cut. <li>(1,100]: compresses the image to the specified number of frames. |
| /interlace/&lt;Mode> | Progressive mode of the output JPG image. Valid values of `Mode`: <br>`0` (default): disables the progressive mode. <br>`1`: enables the progressive mode. <br>This parameter takes effect only when the output image is in JPG format. Otherwise, this parameter will be ignored. |
| /ignore-error/1 | If this parameter is carried and the image failed to be processed because it is too large, the input image will be returned with no error reported. |


## Examples

>? **Processing upon download** is used as an example here, which does not store the output image in a bucket. If you need to store the output image, please see [Persistent Image Processing](https://intl.cloud.tencent.com/document/product/436/40592) and use **Processing upon upload** or **Processing in-cloud data**.


#### Example 1: converting a JPEG image into PNG format

```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/format/png
```

#### Example 2: converting a JPEG image into PNG format with a signature carried

This example processes the image in the same way as in the example above except that a signature is carried. The signature is joined with other processing parameters using an ampersand (&):

```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?q-sign-algorithm=<signature>&imageMogr2/format/png
```

>? You can obtain the value of `<signature>` by referring to [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).
>

## Notes

To prevent unauthorized users from accessing or downloading the input image by using a URL that does not contain any processing parameter, you can add the processing parameters to the request signature, making the processing parameters the key of the parameter with the value left empty. The following is a simple example for your reference (it might have expired or become inaccessible). For more information, please see [Request Signature](https://intl.cloud.tencent.com/document/product/436/14114).


```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?q-sign-algorithm=sha1&q-ak=AKID********************&q-sign-time=1593342360;1593342720&q-key-time=1593342360;1593342720&q-header-list=&q-url-param-list=watermark%252f1%252fimage%252fahr0cdovl2v4yw1wbgvzlteyntewmdawmdqucgljc2gubxlxy2xvdwquy29tl3nodwl5aw4uanbn%252fgravity%252fsoutheast&q-signature=26a429871963375c88081ef60247c5746e834a98&watermark/1/image/aHR0cDovL2V4YW1wbGVzLTEyNTEwMDAwMDQucGljc2gubXlxY2xvdWQuY29tL3NodWl5aW4uanBn/gravity/southeast
```


​	
