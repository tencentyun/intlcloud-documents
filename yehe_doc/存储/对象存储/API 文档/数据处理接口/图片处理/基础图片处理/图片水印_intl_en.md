## Overview
COS′s Image Watermarking is implemented using the **watermark** API of Cloud Infinite (CI) and thus only images stored in CI-bound buckets can be processed. For the restrictions on Basic Image Processing (including watermarking), please see [Rules and Limits](https://intl.cloud.tencent.com/document/product/1045/33425).


>! Image Processing is charged by CI. For detailed pricing, please see CI′s [Billing and Pricing](https://intl.cloud.tencent.com/document/product/1045/33431).
>

## API Format

```plaintext
download_url?watermark/1/image/<encodedURL>
           		 	/gravity/<gravity>
           		 	/dx/<dx>
           		 	/dy/<dy>
           		 	/blogo/<type>
```

>? Spaces and line breaks above are for readability only and thus can be ignored.
>



## Parameters

In the code above, `watermark` is the operation name and the number `1` indicates that the watermark is an image.


| Parameter | Description |
| ------------ | ------------------------------------------------------------ |
| download_url | URL of the input image, formatted as `<BucketName-APPID>.cos.<picture region>.<domain>.com/<picture name>`<br>Example: `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg` |
| /image/ | [Base64 URL-safe encoded](https://intl.cloud.tencent.com/document/product/1045/33430) URL of the image watermark. For example, if the image watermark URL is `http://examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/shuiyin_2.png`, you should set this parameter to `aHR0cDovL2V4YW1wbGVidWNrZXQtMTI1MDAwMDAwMC5jb3MuYXAtc2hhbmdoYWkubXlxY2xvdWQuY29tL3NodWl5aW5fMi5wbmc`. |
| /gravity/ | Position of the image watermark, which is a square in a [3x3 grid](#1). Default value: southeast |
| /dx/ | Horizontal offset in pixels. Default value: 0 |
| /dy/ | Vertical offset in pixels. Default value: 0 |
| /blogo/ | Adaptation mode for an image watermark that is larger than the input image. Valid values: <br><li>`1`: scales the image watermark to the size of the input image. <br><li>`2`: crops the image watermark to the size of the input image. |
| /scatype/ | Scaling mode for the image watermark (relative to the input image). This parameter must be used together with `/spcent/`. Valid values:<br><li>`1`: scales by width.<br><li>`2`: scales by height.<br><li>`3`: scales by area. |
| /spcent/ | Scale ratio of the image watermark (relative to the input image), in permillage. This parameter must be used together with `/scatype/`. Value range: [1,1000]. By default, the image watermark is not scaled. |
| /ignore-error/1 | If this parameter is carried and the image failed to be processed because it is too large, the input image will be returned with no error reported. |

>! An image watermark must:  
> - Be stored in the same bucket as the input image.
> - Have a URL containing a COS domain name (a CDN acceleration domain name such as `examplebucket-1250000000.file.myqcloud.com/shuiyin_2.png` is unsupported) and be accessible (if the image watermark is set to private-read, it must carry a signature).
> - Have a URL starting with `http://`. Note that “http://” cannot be omitted or changed to “https://”. For example, `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/shuiyin_2.png` and `https://examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/shuiyin_2.png` are invalid watermark URLs.
> 

<span id="1"></span>

>? You can add up to 10 image watermarks to a single image.
>

## 3x3 Grid Position Diagram

The 3x3 grid position diagram is as follows. Once you specify the `gravity` parameter to position your watermark, the corresponding red dot becomes the reference point of the square, and offsets will be relative to this point. 
![](https://main.qcloudimg.com/raw/53a143451229b4fbdd74935afe3832d5.png)


>?
>- If `gravity` is set to `center`, `dx` and `dy` are invalid.
>- If `gravity` is set to `north` or `south`, `dx` is invalid and the watermark will be centered horizontally.
>- If `gravity` is set to `west` or `east`, `dy` is invalid and the watermark will be centered vertically.


## Sample

**Adding an image watermark**

```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?watermark/1/image/aHR0cDovL2V4YW1wbGVzLTEyNTEwMDAwMDQucGljc2gubXlxY2xvdWQuY29tL3NodWl5aW4uanBn/gravity/southeast
```

The effect of an added image watermark is as follows:
![](https://main.qcloudimg.com/raw/6412c0d6eaaadc5c193515f40d736dad.jpeg)

