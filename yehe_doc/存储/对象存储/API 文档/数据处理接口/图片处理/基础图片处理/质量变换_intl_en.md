## Overview

COS uses the **imageMogr2** API provided by CI to adjust the quality of an image.

>!
> - Image Processing is a paid service, the fees of which are charged by Cloud Infinite. For detailed billing instructions, see Cloud Infinite’s [Billing and Pricing](https://intl.cloud.tencent.com/document/product/1045/33431).
> - This API applies only to images in **JPG** or **WebP** formats.
> 

## API Format

```plaintext
download_url?imageMogr2/quality/<Quality>
                       /rquality/<quality>
                       /lquality/<quality>						
```

## Parameters

Operation: quality

| Parameter | Description |
| ------------------- | ------------------------------------------------------------ |
| download_url | URL of the input image, formatted as `<BucketName-APPID>.cos.<picture region>.<domain>.com/<picture name>`<br>Example: `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg` |
| /quality/&lt;Quality>  | Absolute quality of the image. Value range: 0−100. Default value: quality of the input image. The smaller value between the input image quality and the specified quality is used. If there is an exclamation mark (!) after `&lt;Quality&gt;` (for example, `90!`), the specified quality is used. |
| /rquality/&lt;quality> | Relative quality of the image, relative to that of the input image. Value range: 0−100. For example, if the input image quality is 80 and `rquality` is set to `80`, the quality of the output image is 64 (that is, 80 x 80%). |
| /lquality/&lt;quality> | The lowest quality of the output image. Value range: 0−100. <br><li>If the input image quality is 85 and `lquality` is set to `80`, the quality of the output image is 85.<br><li>If the input image quality is 60 and `lquality` is set to `80`, the quality of the output image will be improved to 80. </li> |
| /ignore-error/1 | If this parameter is carried and the image failed to be processed because it is too large, the input image will be returned with no error reported. |


## Examples

**Sample request 1: setting absolute quality**
This example sets the **absolute quality** of an image to `60`:
```plaintext
http://examples-1251000004.picsh.myqcloud.com/sample.jpeg?imageMogr2/quality/60
```

Output image:
![](https://main.qcloudimg.com/raw/499501182b2989899116d958f94368a5.jpeg)


**Sample request 2: setting relative quality**

This example sets the **relative quality** of an image to `60`:

```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/rquality/60
```

Output image:
![](https://main.qcloudimg.com/raw/7b111c90aca02d94d0f11991d92e64cb.jpeg)

**Sample request 3: setting relative quality with a signature carried**

This example processes the image in the same way as in the example above except that a signature is added. The signature is joined with other processing parameters using an ampersand (&):

```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?q-sign-algorithm=<signature>&imageMogr2/rquality/60
```

>? You can obtain the value of `<signature>` by referring to [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).
>
