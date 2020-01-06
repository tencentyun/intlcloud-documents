## Description
The **watermark** API is used to process image watermarks. The watermark image must be an image that has already been stored in CI. Currently, this API is applicable to images with a size no greater than 20 MB and a length and width both less than 9,999 pixels.

## API Format

```
download_url?watermark/1/image/<encodedURL>
           		 	/gravity/<gravity>
           		 	/dx/<dx>
           		 	/dy/<dy>
           		 	/blogo/<type>
```

> Ignore the preceding spaces and line breaks.



### Parameter description

**Operation**: watermark. 1 indicates that the watermark is an image watermark.


| Parameter | Description |
| ------------ | ------------------------------------------------------------ |
| download_url | The aile URL in the format of `<BucketName-APPID>.<picture region>.<domain>.com/<picture name>`, <br>for example, `examplebucket-1250000000.picsh.myqcloud.com/picture.jpeg`. |
| /image/ | The address of the watermark source image, which must be Base64-encoded for URL security. |
| /gravity/ | The position of the text watermark in the Sudoku orientation chart (see the [Sudoku Orientation Chart](#1)). The default value is SouthEast. |
| /dx/ | The horizontal margin in pixels. The default value is 0. |
| /dy/ | The vertical margin in pixels. The default value is 0. |
| /blogo/ | The watermark image adaptation feature, which is applicable to scenarios in which the watermark image size is too large, for example, a watermark wall. There are two options: When `blogo` is set to 1, the watermark image is scaled to a size similar to that of the original image and then added. When blogo is set to 2, the watermark image is directly cropped to a size similar to that of the original image and then added. |

> The specified watermark image must meet all the following conditions:  
- The watermark image and the source image must be located in the same bucket.
- The URL must be a domain name of the CI origin server (and cannot be a CDN acceleration or COS origin server domain name). For example, `v2test-10000812.image.myqcloud.com` is a CDN acceleration domain name, and therefore cannot be used as a watermark URL.
- The URL must start with `http://`. The HTTP header cannot be omitted or replaced by an HTTPS header. For example, `examplebucket-1250000000.picsh.myqcloud.com/shuiyin_2.png` and `https://examplebucket-1250000000.picsh.myqcloud.com/shuiyin_2.png` are invalid watermark URLs.

<span id="1"></span>
### Sudoku orientation chart

A Sudoku orientation chart can provide a position reference for various operations performed on an image. The red dot indicates the origin of each region (after each region is selected by using the `gravity` parameter, the displacement operation is performed by using the corresponding far point as the reference.) 
![](https://main.qcloudimg.com/raw/53a143451229b4fbdd74935afe3832d5.png)


>
- When `gravity` is set to center, the `dx` and `dy` parameters are invalid.
- When `gravity` is set to north or south, the `dx` parameter is invalid (in which case the watermark is centered horizontally).
- When `gravity` is set to west or east, the `dy` parameter is invalid (in which case the watermark is centered vertically).


## Example
**Adding an image watermark**

```
http://examples-1251000004.picsh.myqcloud.com/sample.jpeg?watermark/1/image/aHR0cDovL2V4YW1wbGVzLTEyNTEwMDAwMDQucGljc2gubXlxY2xvdWQuY29tL3NodWl5aW4uanBn/gravity/southeast
```

After the image watermark is added, the effect is as follows:
![](https://main.qcloudimg.com/raw/6412c0d6eaaadc5c193515f40d736dad.jpeg)