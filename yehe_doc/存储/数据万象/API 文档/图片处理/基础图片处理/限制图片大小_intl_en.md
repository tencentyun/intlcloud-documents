## Overview

CI uses the **imageMogr2/size-limit** API to limit the size of an image processed (e.g., scaled or compressed).

## API Format

```
download_url?imageMogr2/size-limit
```

## Parameters

Operation: size-limit

| Parameter | Description |
| :-------------- | :----------------------------------------------------------- |
| download_url | URL of the input image, formatted as `<BucketName-APPID>.cos.<Region>.myqcloud.com/<picture name>`<br>Example: `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg` |
| size-limit | Limits the size of an output image. The unit can be `k` (KB) or `m` (MB). <br>1. Only JPG images are supported. <br>2. Appending an exclamation mark (!) means to compare the sizes of the input and output images. If the output image is smaller than the input image, the output image will be returned. Otherwise, the input image will be returned. Example: examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpg?imageMogr2/size-limit/15k!<br>3. You are advised to use this parameter together with `strip` to remove redundant image metadata. Example: examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpg?imageMogr2/strip/format/png/size-limit/15k! |
| /ignore-error/1 | If this parameter is carried and the image failed to be processed because it is too large, the input image will be returned with no error reported. |

## Examples
#### Converting image format and limiting the output file size

This example converts a JPG image into PNG format and limits the output image size to 15 KB:

```
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/strip/format/png/size-limit/15k!
```

#### Converting image format and limiting the output file size with a signature carried

This example processes the image in the same way as in the example above except that a signature is carried. The signature is joined with other processing parameters using an ampersand (&):

```
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?q-sign-algorithm=<signature>&imageMogr2/strip/format/png/size-limit/15k!
```

>? You can obtain the value of `<signature>` by referring to [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).
>
