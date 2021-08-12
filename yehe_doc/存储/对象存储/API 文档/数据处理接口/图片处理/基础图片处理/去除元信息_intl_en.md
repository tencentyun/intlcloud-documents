## Overview

COS uses the **imageMogr2** API provided by CI to remove image metadata, including EXIF data.

>! Image Processing is charged by CI. For detailed pricing, please see CI′s [Billing and Pricing](https://intl.cloud.tencent.com/document/product/1045/33431).
>

## API Format
```plaintext
download_url?imageMogr2/strip
```

## Parameters

Operation: strip

| Parameter | Description |
| ------------ | ------------------------------------------------------------ |
| download_url | URL of the input image, formatted as `<BucketName-APPID>.cos.<picture region>.<domain>.com/<picture name>`<br>Example: `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg` |
| /ignore-error/1 | If this parameter is carried and the image failed to be processed because it is too large, the input image will be returned with no error reported. |

## Examples

#### Sample request 1: public-read
```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/strip
```

#### Sample request 2: private-read with a signature carried

This example processes the image in the same way as in the example above except that a signature is added. The signature is joined with other processing parameters using an ampersand (&):

```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?q-sign-algorithm=<signature>&imageMogr2/strip
```

>? You can obtain the value of `<signature>` by referring to [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).
>
