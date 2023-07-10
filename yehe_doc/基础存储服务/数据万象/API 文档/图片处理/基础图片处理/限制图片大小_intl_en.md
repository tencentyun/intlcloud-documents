## Feature Overview

CI uses the **imageMogr2/size-limit** API to limit the size of an image processed (e.g., scaled or compressed).


## Restrictions

- Format: The API for limiting the image size is supported only for JPG images.
- Size: The original image cannot be larger than 32 MB. Its dimensions cannot exceed 50000 pixels and its resolution cannot exceed 250 million pixels. The dimensions of the output image cannot exceed 50000 pixels.



## API Format

```plaintext
GET /<ObjectKey>?imageMogr2/size-limit HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>
```

>? 
> - Authorization: Auth String (See [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details.)
> - When this feature is used by a sub-account, relevant permissions must be granted as instructed in [Authorization Granularity Details](https://intl.cloud.tencent.com/document/product/1045/49896).


## Parameters

Operation: size-limit

| Parameter | Description |
| :-------------- | :----------------------------------------------------------- |
| ObjectKey  | Object name, such as `folder/sample.jpg`.                           |
| size-limit | Limits the size of the output image. The unit can be `k` (KB) or `m` (MB). <br><li> Only JPG images are supported. <br><li> Appending an exclamation mark (!) means to compare the sizes of the input and output images. If the output image is smaller, the output image will be returned; otherwise, the input image will be returned; for example,  `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpg?imageMogr2/size-limit/15k!`. <br><li> We recommend you use this parameter together with `strip` to remove redundant image metadata, for example, `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.png?imageMogr2/strip/format/jpg/size-limit/15k! `. |
| /ignore-error/1 | If this parameter is carried and the image fails to be processed because the image is too large or a parameter value exceeds the limit, the input image will be returned with no error reported. |

## Examples

#### Example 1: converting image format and limiting the output image size

This example converts a PNG image into JPG format and limits the output image size to 15 KB:

```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.png?imageMogr2/strip/format/jpg/size-limit/15k!
```

#### Example 2: converting image format and limiting the output image size with a signature carried

This example processes the image in the same way as in the example above except that a signature is carried. The signature is joined with other processing parameters using an ampersand (&):

```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.png?q-sign-algorithm=<signature>&imageMogr2/strip/format/jpg/size-limit/15k!
```

>? You can obtain the value of `<signature>` by referring to [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).
>

## Notes

To prevent unauthorized users from accessing or downloading the input image by using a URL that does not contain any processing parameter, you can add the processing parameters to the request signature, making the processing parameters the key of the parameter with the value left empty. The following is a simple example for your reference (it might have expired or become inaccessible). For more information, see [Upload via Pre-Signed URL](https://intl.cloud.tencent.com/document/product/436/14114).


```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?q-sign-algorithm=sha1&q-ak=AKID********************&q-sign-time=1593342360;1593342720&q-key-time=1593342360;1593342720&q-header-list=&q-url-param-list=watermark%252f1%252fimage%252fahr0cdovl2v4yw1wbgvzlteyntewmdawmdqucgljc2gubxlxy2xvdwquy29tl3nodwl5aw4uanbn%252fgravity%252fsoutheast&q-signature=26a429871963375c88081ef60247c5746e834a98&watermark/1/image/aHR0cDovL2V4YW1wbGVzLTEyNTEwMDAwMDQucGljc2gubXlxY2xvdWQuY29tL3NodWl5aW4uanBn/gravity/southeast
```


