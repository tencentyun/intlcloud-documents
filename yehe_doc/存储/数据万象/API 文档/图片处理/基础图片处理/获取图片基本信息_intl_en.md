## Overview
CI uses the **imageInfo** API to query an image’s basic information such as its format, width, and height.

## Use Limits

- The input image cannot be larger than 32 MB.
- The width and height of the input image cannot exceed 30,000 pixels and the total number of pixels cannot exceed 250 million. The width and height of the output image cannot exceed 9,999 pixels.
- For an input animated image, the total number of pixels (Width x Height x Number of frames) cannot exceed 250 million pixels.

## API Format

```plaintext
download_url?imageInfo
```

## Parameters

#### Request parameters

**Operation**: imageInfo

| Parameter | Description |
| ------------ | ------------------------------------------------------------ |
| download_url | URL of the input image, formatted as `&lt;BucketName-APPID>.cos.&lt;Region>.myqcloud.com/&lt;picture name>`<br>Example: `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg` |

#### Response parameters

| Parameter | Description |
| ----------- | ----------------------------------------- |
| format      | Image format such as `png` or `gif`      |
| width       | Width of the image, in pixels |
| height      | Height of the image, in pixels   |
| size        | Image size, in bytes |
| md5         | MD5 checksum of the image                    |
| frame_count | Number of frames. For static images, this value is `1`. |

## Examples

#### Example 1: public-read

#### Request
```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageInfo
```

#### Response
```plaintext
{"format": "jpeg", "width": "960", "height": "540", "size": "158421", "md5": "77a16fa70e2eba652fb42e8a639c52f2", "photo_rgb": "0x736246"}
```

#### Example 2: private-read with a signature carried

This example obtains the average hue in the same way as in the example above except that a signature is carried. The signature is joined with other parameters using an ampersand (&):

```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?q-sign-algorithm=<signature>&imageInfo
```

>? You can obtain the value of `<signature>` by referring to [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).
>

## Notes

To prevent unauthorized users from accessing or downloading the input image by using a URL that does not contain any processing parameter, you can add the processing parameters to the request signature, making the processing parameters the key of the parameter with the value left empty. The following is a simple example for your reference (it might have expired or become inaccessible). For more information, please see [Request Signature](https://intl.cloud.tencent.com/document/product/436/14114).


```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?q-sign-algorithm=sha1&q-ak=AKID********************&q-sign-time=1593342360;1593342720&q-key-time=1593342360;1593342720&q-header-list=&q-url-param-list=watermark%252f1%252fimage%252fahr0cdovl2v4yw1wbgvzlteyntewmdawmdqucgljc2gubxlxy2xvdwquy29tl3nodwl5aw4uanbn%252fgravity%252fsoutheast&q-signature=26a429871963375c88081ef60247c5746e834a98&watermark/1/image/aHR0cDovL2V4YW1wbGVzLTEyNTEwMDAwMDQucGljc2gubXlxY2xvdWQuY29tL3NodWl5aW4uanBn/gravity/southeast
```
