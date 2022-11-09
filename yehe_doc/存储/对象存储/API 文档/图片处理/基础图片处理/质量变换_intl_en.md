## Feature Overview

CI uses the **imageMogr2** API to adjust the quality of an image.

An image can be processed:

- During download
- During upload
- In the cloud

>? This API supports images in JPG, WebP, TPG, HEIF, or AVIF format.
>

## API Sample

#### 1. Processing during download

```plaintext
GET /<ObjectKey>?imageMogr2/quality/<Quality>
                           /rquality/<quality>
                           /lquality/<quality> HTTP/1.1
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
      "rule": "imageMogr2/quality/<Quality>
                       /rquality/<quality>
                       /lquality/<quality>"
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
      "rule": "imageMogr2/quality/<Quality>
                       /rquality/<quality>
                       /lquality/<quality>"
  }]
}
```


>? 
> - Authorization: Auth String (for more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).
> - When this feature is used by a sub-account, relevant permissions must be granted. For more information, see [Authorization Granularity Details](https://intl.cloud.tencent.com/document/product/1045/49896).
> 


## Parameters

Operation name: quality.

| Parameter | Description |
| ------------------- | ------------------------------------------------------------ |
| ObjectKey  | Object name, such as `folder/sample.jpg`.                           | 
| /quality/&lt;Quality>  | Absolute quality of the image. The value can be 0–100. Use the value of the original image quality (default) or the specified quality, whichever is smaller. If there is an exclamation mark (!) after &lt;Quality&gt; (such as `90!`), the specified quality value is forcibly used. |
| /rquality/&lt;quality> | Image quality relative to that of the input image. The value can be 0−100. For example, if the input image quality is 80 and `rquality` is set to `80`, the quality of the output image will be 64 (80 * 80%). |
| /lquality/&lt;quality> | Minimum quality of the image. Value range: 0−100. <br><li>If the input image quality is 85 and `lquality` is set to 80, the quality of the output image will be 85.</li><li>If the input image quality is 60 and `lquality` is set to 80, the quality of the output image will be improved to 80.</li> |
| /ignore-error/1 | If this parameter is carried and the image fails to be processed because the image is too large or a parameter value exceeds the limit, the input image will be returned with no error reported. |


## Samples

>? **Processing during download** is used as an example here, which does not store the output image in a bucket. If you need to store the output image, see [Persistent Image Processing](https://intl.cloud.tencent.com/document/product/1045/33695) and use the **processing during upload** or **processing in-cloud data** feature.
>
  

#### Sample 1: Setting an absolute quality

This example sets the **absolute quality** to 60:
```plaintext
http://examples-1251000004.picsh.myqcloud.com/sample.jpeg?imageMogr2/quality/60
```

Output:
![](https://main.qcloudimg.com/raw/499501182b2989899116d958f94368a5.jpeg)

#### Sample 2: Setting a relative quality

This example sets the **relative quality** to 60:

```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/rquality/60
```

Output:
![](https://main.qcloudimg.com/raw/7b111c90aca02d94d0f11991d92e64cb.jpeg)

#### Sample 3. Setting the relative quality to 60 with a signature carried

This example processes the image in the same way as in the example above, except that a signature is carried. The signature is concatenated with other processing parameters by an ampersand (&).

```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?q-sign-algorithm=<signature>&imageMogr2/rquality/60
```

>? You can get the value of `<signature>` as instructed in [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).
>


## Notes

To prevent unauthorized users from accessing or downloading the input image by using a URL that does not contain any processing parameter, you can add the processing parameters to the request signature, making the processing parameters the key of the parameter with the value left empty. The following is a simple sample for your reference (it might have expired or become inaccessible). For more information, see [Upload via Pre-Signed URL](https://intl.cloud.tencent.com/document/product/436/14114).


```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?q-sign-algorithm=sha1&q-ak=AKID********************&q-sign-time=1593342360;1593342720&q-key-time=1593342360;1593342720&q-header-list=&q-url-param-list=watermark%252f1%252fimage%252fahr0cdovl2v4yw1wbgvzlteyntewmdawmdqucgljc2gubxlxy2xvdwquy29tl3nodwl5aw4uanbn%252fgravity%252fsoutheast&q-signature=26a429871963375c88081ef60247c5746e834a98&watermark/1/image/aHR0cDovL2V4YW1wbGVzLTEyNTEwMDAwMDQucGljc2gubXlxY2xvdWQuY29tL3NodWl5aW4uanBn/gravity/southeast
```




