## Overview

COS uses the **imageAve** API provided by CI to obtain the average hue of an image. The input image cannot be larger than 32 MB, with its width and height not exceeding 30,000 pixels, and the total number of pixels not exceeding 250 million. The width and height of the output image cannot exceed 9,999 pixels. For an input animated image, the total number of pixels (Width x Height x Number of frames) cannot exceed 250 million pixels.

>! Image Processing is charged by CI. For detailed pricing, please see **Basic image processing fee** in [Billing and Pricing](https://intl.cloud.tencent.com/document/product/1045/33431).
>

## API Format
```plaintext
download_url?imageAve
```

## Parameters

**Operation**: imageAve

| Parameter | Description |
| ------------ | ------------------------------------------------------------ |
| download_url | URL of the input image, formatted as `&lt;BucketName-APPID>.cos.&lt;Region>.myqcloud.com/&lt;picture name>`<br>Example: `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg` |


## Examples

#### Sample request 1: public-read

```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageAve
```

#### Response
```plaintext
{"RGB": "0x736246"}
```

#### Sample request 2: private-read with a signature carried

This example obtains the average hue in the same way as in the example above except that a signature is carried. The signature is joined with other parameters using an ampersand (&):

```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?q-sign-algorithm=<signature>&imageAve
```

>? You can obtain the value of `<signature>` by referring to [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).
>
