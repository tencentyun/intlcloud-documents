## Overview
COS uses the **imageMogr2** API provided by CI to adjust an image’s contrast, which is the difference in luminance between the brightest and darkest points in an image (i.e., the contrast in grayscale).

## API Format

```shell
download_url?imageMogr2/contrast/<value>
```

## Parameters

Operation: contrast

| Parameter | Description |
| ---------------- | ------------------------------------------------------------ |
| download_url | URL of the input image, formatted as `&lt;BucketName-APPID>.cos.&lt;Region>.myqcloud.com/&lt;picture name>`<br>Example: `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg` |
| /contrast/&lt;value> | Adjusts the contrast of an image. The value must be an integer in the range of [−100, 100].<br><li>`value` < 0: reduces the contrast.<br><li>`value` = 0: does not adjust the contrast.<br><li>`value` > 0: increases the contrast. </li>|
| /ignore-error/1 | If this parameter is carried and the image failed to be processed because it is too large, the input image will be returned with no error reported. |

## Examples

#### Sample request 1: adjusting contrast

This example reduces the contrast of an image by 50:
```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/contrast/-50
```

Output image:
![](https://main.qcloudimg.com/raw/555a3a42dff976c0f4ef382de70eae79.jpg)

#### Sample request 2: adjusting contrast with a signature carried

This example processes the image in the same way as in the example above except that a signature is added. The signature is joined with other processing parameters using an ampersand (&):

```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?q-sign-algorithm=<signature>&imageMogr2/contrast/-50
```

>?  You can obtain the value of `<signature>` by referring to [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).
>
