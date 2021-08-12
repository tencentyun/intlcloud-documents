## Overview
COS uses the **imageInfo** API provided by CI to query an image’s basic information, such as its format, width, and height. The input image cannot be larger than 32 MB, with its width and height not exceeding 30,000 pixels, and the total number of pixels not exceeding 250 million. The width and height of the output image cannot exceed 9,999 pixels. For an input animated image, the total number of pixels (Width x Height x Number of frames) cannot exceed 250 million pixels.

>! Image Processing is charged by CI. For detailed pricing, please see **Basic image processing fee** in [Billing and Pricing](https://intl.cloud.tencent.com/document/product/1045/33431).
>

## API Format

```plaintext
download_url?imageInfo
```

## Parameters

**Operation**: imageInfo

| Parameter | Description |
| ------------ | ------------------------------------------------------------ |
| download_url | URL of the input image, formatted as `&lt;BucketName-APPID>.cos.&lt;Region>.myqcloud.com/&lt;picture name>`<br>Example: `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg` |

## Examples

#### Sample request 1: public-read
```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageInfo
```
#### Response
```plaintext
{"format": "jpeg", "width": "960", "height": "540", "size": "158421", "md5": "77a16fa70e2eba652fb42e8a639c52f2", "photo_rgb": "0x736246"}
```

#### Sample request 2: private-read with a signature carried

This example obtains the image information in the same way as in the example above except that a signature is carried. The signature is joined with other parameters using an ampersand (&):

```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?q-sign-algorithm=<signature>&imageInfo
```

>? You can obtain the value of `<signature>` by referring to [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).
>
