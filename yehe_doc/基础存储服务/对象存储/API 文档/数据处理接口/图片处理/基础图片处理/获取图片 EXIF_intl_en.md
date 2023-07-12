## Feature Overview
Exchangeable Image File (EXIF) records the camera settings, thumbnails, and other attributes of digital images. COS uses the **exif** API provided by CI to get EXIF data. An input image cannot be larger than 32 MB, with its width and height not exceeding 30,000 pixels and the total number of pixels not exceeding 250 million. The width and height of the output image cannot exceed 9,999 pixels. For an input animated image, its total number of pixels (width x height x number of frames) cannot exceed 250 million.

>!
> - Image processing is charged by CI. For detailed pricing, see [Image Processing Fees](https://intl.cloud.tencent.com/document/product/1045/45582).
> - If the image does not have EXIF data, `{"error" : "no exif data"}` will be returned.
> 

## API Sample

```plaintext
GET /<ObjectKey>?exif HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>
```

>? 
> - Authorization: Auth String (for more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).
> - When this feature is used by a sub-account, relevant permissions must be granted. For more information, see [Authorization Granularity Details](https://intl.cloud.tencent.com/document/product/1045/49896).
> 

## Parameters

**Operation name**: exif.

| Parameter | Description |
| ------------ | ------------------------------------------------------------ |
| ObjectKey  | Object name, such as `folder/sample.jpg`.                           | 


## Samples

#### Sample 1: Public-read
```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?exif
```

#### Sample 2: Private-read with a signature carried

This example processes the image in the same way as in the example above, except that a signature is carried. The signature is concatenated with other parameters by an ampersand (&).

```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?q-sign-algorithm=<signature>&exif
```

>? You can get the value of `<signature>` as instructed in [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).
>


## Notes

To prevent unauthorized users from accessing or downloading the input image by using a URL that does not contain any processing parameter, you can add the processing parameters to the request signature, making the processing parameters the key of the parameter with the value left empty. The following is a simple sample for your reference (it might have expired or become inaccessible). For more information, see [Upload via Pre-Signed URL](https://intl.cloud.tencent.com/document/product/436/14114).


```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?q-sign-algorithm=sha1&q-ak=AKID********************&q-sign-time=1593342360;1593342720&q-key-time=1593342360;1593342720&q-header-list=&q-url-param-list=watermark%252f1%252fimage%252fahr0cdovl2v4yw1wbgvzlteyntewmdawmdqucgljc2gubxlxy2xvdwquy29tl3nodwl5aw4uanbn%252fgravity%252fsoutheast&q-signature=26a429871963375c88081ef60247c5746e834a98&watermark/1/image/aHR0cDovL2V4YW1wbGVzLTEyNTEwMDAwMDQucGljc2gubXlxY2xvdWQuY29tL3NodWl5aW4uanBn/gravity/southeast
```
