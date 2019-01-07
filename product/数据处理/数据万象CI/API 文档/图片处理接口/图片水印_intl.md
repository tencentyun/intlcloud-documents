## Overview
CI supports real-time image watermarking. Currently, the watermark image must be specified as an image stored in CI. This supports processing images with a size of less than 20 MB and a length x width of less than 9,999 pixels.
## API Form
download_url?watermark
>**Note:**
Please ignore the line breaks in the following API.


```
  download_url?watermark/1
                        /image/
						/blogo/
                        /gravity/
                        /dx/
                        /dy/
```
## Parameter Descriptions
| Parameter                                      | Meaning                                       |
| --------------------------------------- | ---------------------------------------- |
| download_url | Access link of the file which is structured as &lt;bucket id&gt;-&lt;appid&gt;.&lt;picture region&gt;.&lt;domain&gt;.com/&lt;picture name&gt;, for example, examples-1251000004.picsh.myqcloud.com/sample.jpeg |
| /image/ | Source watermark image address; URL-safe Base64 encoding is necessary. The specified watermark image must satisfy all the following three conditions: </br>1. The watermark image and the source image must be in the same object bucket; </br>2. The URL needs to use CI's real server domain name (CDN's and COS' real server domain names are not supported), for example, `v2test-10000812.image.myqcloud.com` is a CDN domain name and thus cannot be used as the watermark URL; </br>3. The URL must start with `http://` (the HTTP header cannot be omitted, and the HTTPS header is not supported), for example, `tengxunyun-10004486.picsh.myqcloud.com/shuiyin_2.png` and `https://tengxunyun-10004486.picsh.myqcloud.com/shuiyin_2.png` are invalid watermark URLs. |
| /gravity/ | Text watermark position in the grid (see the [grid position diagram](#1)), Southeast by default |
| /dx/ | Horizontal (horizontal axis) margin in pixels, 0 by default |
| /dy/ | Vertical (vertical axis) margin in pixels, 0 by default |
| /blogo/&lt;type&gt; | Watermark image fitting function, suitable for scenarios with large watermark size (such as watermark wall). There are two options: if blogo is set to 1, the watermark image will be scaled to a size similar to that of the original image; if it is 2, the watermark image will be directly cropped to a size similar to that of the original image before adding.

## Example

```
http://examples-1251000004.picsh.myqcloud.com/sample.jpeg?watermark/1/image/aHR0cDovL2V4YW1wbGVzLTEyNTEwMDAwMDQucGljc2gubXlxY2xvdWQuY29tL3NodWl5aW4uanBn/gravity/southeast
```
<span id="1"></span>

## Grid Position Diagram
The grid position diagram provides a location reference for various operations on the image. The red dots are the origins of each zone position (if the gravity parameter is set to select the zones, the offsetting operation will use the corresponding origins as reference).
![](https://main.qcloudimg.com/raw/25596a911919e464d5edf4c84b829fbe.png)
