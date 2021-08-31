## Feature Overview
CI provides the image watermark processing feature through the **watermark** API. Currently, a watermark image must be specified as an image stored in CI. The size of the input image to be processed cannot exceed 20 MB, its width and height cannot exceed 30,000 pixels respectively, and its total pixels cannot exceed 250 million. The width and height of the output image cannot exceed 9,999 pixels respectively. For animated images, the input image's Width x Height x Number of frames cannot exceed 250 million pixels.

## API Format

```shell
download_url?watermark/1/image/<encodedURL>
           		 	/gravity/<gravity>
           		 	/dx/<dx>
           		 	/dy/<dy>
           		 	/blogo/<type>
```

>?Ignore the spaces and line breaks above.



## Parameter Description

**Operation name**: watermark. 1 indicates that the watermark is an image watermark.


| Parameter | Description |
| ------------ | ------------------------------------------------------------ |
| download_url | File access URL in the format of `<BucketName-APPID>.cos.<picture region>.<domain>.com/<picture name>`, <br>such as `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg` |
| /image/ | Watermark image address, which should be [Base64-encoded in a URL-safe way](https://intl.cloud.tencent.com/document/product/1045/33430#.E4.BB.80.E4.B9.88.E6.98.AF-url-.E5.AE.89.E5.85.A8.E7.9A.84-base64-.E7.BC.96.E7.A0.81.EF.BC.9F). For example, if the watermark image is `http://examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/shuiyin_2.png`, then the encoded string is `aHR0cDovL2V4YW1wbGVidWNrZXQtMTI1MDAwMDAwMC5jb3MuYXAtc2hhbmdoYWkubXlxY2xvdWQuY29tL3NodWl5aW5fMi5wbmc` |
| /gravity/ | Text watermark position in the nine-part grid (please see [Nine-Part Grid](#1)). The default value is `SouthEast`. |
| /dx/ | Horizontal margin in pixels. Default value: 0 |
| /dy/ | Vertical margin in pixels. Default value: 0 |
| /blogo/ | Watermark image adaptation feature, which is applicable to scenarios where the watermark image size is too large, for example, a watermark wall. There are two options: <br><li>When `blogo` is set to 1, the watermark image is scaled to a size similar to that of the original image and then added. <br><li>When `blogo` is set to 2, the watermark image is directly cropped to a size similar to that of the original image and then added. |
| /scatype/    | Scales watermark image based on original image size.<br><li>When `scatype` is set to 1, the size is scaled by width.<br><li>When `scatype` is set to 2, the size is scaled by height.<br><li>When `scatype` is set to 3, the size is scaled by area.                      |
| /spcent/     | Permillage of watermark image in original image. Value range: [1,1000]. The original image size is used by default.                      |

>!The specified watermark image must meet all the following three conditions:  
>- The watermark image and the original image must be located in the same bucket.
>- The URL needs to be a COS domain name (CDN acceleration domain names such as `examplebucket-1250000000.file.myqcloud.com/shuiyin_2.png` cannot be used), and the watermark image must be accessible (if it is private read, a valid signature must be carried).
>- The URL must start with `http://`. The HTTP header cannot be omitted or replaced by the HTTPS header. For example, `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/shuiyin_2.png` and `https://examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/shuiyin_2.png` are invalid watermark URLs.

<span id="1"></span>

>?Up to 10 different image watermarks can be added to one image.

## Nine-Part Grid

A nine-part grid can provide a location reference for various operations performed on an image. The red dot is the origin of each region (after each region is selected by using the `gravity` parameter, the displacement operation is performed by taking the corresponding far point as the reference.) 
![](https://main.qcloudimg.com/raw/53a143451229b4fbdd74935afe3832d5.png)


>?
>- When `gravity` is set to `center`, the `dx` and `dy` parameters won't take effect.
>- When `gravity` is set to `north` or `south`, the `dx` parameter won't take effect (in which case the watermark is horizontally centered).
>- When `gravity` is set to `west` or `east`, the `dy` parameter won't take effect (in which case the watermark is vertically centered).


## Sample

**Adding an image watermark**

```
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?watermark/1/image/aHR0cDovL2V4YW1wbGVzLTEyNTEwMDAwMDQucGljc2gubXlxY2xvdWQuY29tL3NodWl5aW4uanBn/gravity/southeast
```

After the image watermark is added, the effect is as follows:
![](https://main.qcloudimg.com/raw/6412c0d6eaaadc5c193515f40d736dad.jpeg)


