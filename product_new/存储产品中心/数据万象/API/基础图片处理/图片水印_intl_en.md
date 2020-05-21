## Feature
This API is used to provide image watermarking in Tencent Cloud CI. Currently, watermark images must be those stored in CI. Original images smaller than 20 MB in size and smaller than 9,999 pixels in length and width are supported.

## API Form

```shell
download_url?watermark/1/image/<encodedURL>
           		 	/gravity/<gravity>
           		 	/dx/<dx>
           		 	/dy/<dy>
           		 	/blogo/<type>
```

> Ignore the preceding spaces and line breaks.



## Parameter Description

**Operation name**: watermark. The number 1 indicates the watermark type is image watermark.


| Parameter | Description |
| ------------ | ------------------------------------------------------------ |
| download_url | URL that is used to access a file. The URL form is `<BucketName-APPID>.cos.<picture region>.<domain>.com/<picture name>`, <br>for example, `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg`. |
| /image/ | Watermark image address, which is encoded with Base64 that is safe to the URL. For example, if the watermark image URL is `http://examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/shuiyin_2.png`, the encoded string is `aHR0cCUzQS8vZXhhbXBsZWJ1Y2tldC0xMjUwMDAwMDAwLnBpY3NoLm15cWNsb3VkLmNvbS9zaHVpeWluXzIucG5n`. |
| /gravity/ | Text watermark position, which is a 3x3 grid position ([See the 3x3 grid position diagram](#1)). The default value is SouthEast. |
| /dx/ | Horizontal margin in pixels. The default value is 0. |
| /dy/ | Vertical margin in pixels. The default value is 0. |
| /blogo/ | Watermark image adaptation, which is applicable to scenarios with oversized watermark images (such as a watermark wall). This feature is classified into two types: <br><li>when blogo is set to 1, a watermark image will be added after it is scaled to a size similar to the original image. <br><li>When blogo is set to 2, a watermark image will be added after it is directly cropped to a size similar to the original image. |

> A specified watermark image must meet the following conditions:  
- The watermark image must be in the same bucket as the original image.
- The URL must be an origin server domain name of CI, instead of a CDN acceleration domain name or a COS origin server domain name. For example, `examplebucket-1250000000.image.myqcloud.com` is a CDN acceleration domain name, and cannot be used in the watermark URL.
- The URL must start with `http://`. The HTTP header cannot be omitted or replaced by the HTTPS header. For example, `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/shuiyin_2.png` and `https://examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/shuiyin_2.png` are invalid watermark URLs.

<span id="1"></span>

## 3x3 Grid Position Diagram

A 3x3 grid position diagram provides position reference for multiple image operations. Red dots show the origin points of each region. After you use the gravity parameter to select a region, displacement must be based on the corresponding origin point. 
![](https://main.qcloudimg.com/raw/53a143451229b4fbdd74935afe3832d5.png)


>
>- When the gravity parameter is set to center, the dx and dy parameters are invalid.
>- When the gravity parameter is set to north or south, the dx parameter is invalid, and the watermark is centered horizontally.
>- When the gravity parameter is set to west or east, the dy parameter is invalid, and the watermark is centered vertically.


## Example

This example shows you how to **add an image watermark**.

```
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?watermark/1/image/aHR0cDovL2V4YW1wbGVzLTEyNTEwMDAwMDQucGljc2gubXlxY2xvdWQuY29tL3NodWl5aW4uanBn/gravity/southeast
```

After the image watermark is added, the effect is as follows:
![](https://main.qcloudimg.com/raw/6412c0d6eaaadc5c193515f40d736dad.jpeg)


