## Feature
This API **watermark** from Tencent Cloud CI is used to provide image watermarking in COS. Currently, watermark images must be those stored in buckets associated with CI. Supported original images must be smaller than 20 MB in size and smaller than 9,999 pixels in length and width.


>Image processing is a paid service, the fees of which are charged by Cloud Infinite. For detailed billing instructions, see Cloud Infinite’s [Billing and Pricing](https://intl.cloud.tencent.com/document/product/1045/33431).

## API Form

```plaintext
download_url?watermark/1/image/<encodedURL>
           		 	/gravity/<gravity>
           		 	/dx/<dx>
           		 	/dy/<dy>
           		 	/blogo/<type>
```

>Please ignore the preceding spaces and line breaks.



## Parameter Description

**Operation name**: watermark. 1 indicates that the watermark is an image watermark.


| Parameter         | Description                                                         |
| ------------ | ------------------------------------------------------------ |
| download_url | URL that is used to access a file. Format: `<BucketName-APPID>.cos.<picture region>.<domain>.com/<picture name>`,<br>such as `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg` |
| /image/      | The URL of the watermark image, which must be [URL-safe Base64 encoded](https://intl.cloud.tencent.com/document/product/1045/33430). For example, the watermark image is `http://examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/shuiyin_2.png`, and the encoded string is `aHR0cDovL2V4YW1wbGVidWNrZXQtMTI1MDAwMDAwMC5jb3MuYXAtc2hhbmdoYWkubXlxY2xvdWQuY29tL3NodWl5aW5fMi5wbmc`.           |
| /gravity/ | Text watermark position, which is shown in a 3 x 3 grid ([See the 3 x 3 positioning grid](#1)). The default value is SouthEast. |
| /dx/ | Horizontal margin in pixels. The default value is 0. |
| /dy/ | Vertical margin in pixels. The default value is 0. |
| /blogo/ | The watermark image adaptation feature, which is applicable to scenarios in which the watermark image size is too large, for example, a watermark wall. There are two options:<br><li>When `blogo` is set to 1,  the watermark image is scaled to a size similar to that of the original image and then added.<br><li>When `blogo` is set to 2, the watermark image is directly cropped to a size similar to that of the original image and then added. |

>A specified watermark image must meet the following conditions:  
- The watermark image and the source image must be located in the same bucket.
- The URL must be a domain name of the CI origin server (and cannot be a CDN acceleration or COS origin server domain name). For example, `examplebucket-1250000000.image.myqcloud.com` is a CDN acceleration domain name, and therefore cannot be used as a watermark URL.
- The URL must start with `http://`. The HTTP header cannot be omitted or replaced by an HTTPS header. For example, `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/shuiyin_2.png` and `https://examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/shuiyin_2.png` are invalid watermark URLs.

<span id="1"></span>

## 3 x 3 Positioning Grid

A 3 x 3 positioning grid provides position reference for multiple image operations. Red dots show the origin points of each region. After you use the gravity parameter to select a region, displacement must be based on the corresponding farthest point. 
![](https://main.qcloudimg.com/raw/53a143451229b4fbdd74935afe3832d5.png)


>
>- When `gravity` is set to center, the `dx` and `dy` parameters are invalid.
>- When `gravity` is set to north or south, the `dx` parameter is invalid (in which case the watermark is horizontally centered).
>- When `gravity` is set to west or east, the `dy` parameter is invalid (in which case the watermark is vertically centered).


## Examples

This example shows you how to **add an image watermark**.

```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?watermark/1/image/aHR0cDovL2V4YW1wbGVzLTEyNTEwMDAwMDQucGljc2gubXlxY2xvdWQuY29tL3NodWl5aW4uanBn/gravity/southeast
```

Final image:
![](https://main.qcloudimg.com/raw/6412c0d6eaaadc5c193515f40d736dad.jpeg)


