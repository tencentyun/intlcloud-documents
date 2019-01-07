## Overview
CI supports real-time text watermarking, i.e., adding a text watermark in real time to the image by placing a specific parameter after the image's URL. Currently, this supports processing images with a size of less than 20 MB and a length x width of less than 9,999 pixels.
## API Form
download_url?watermark
>**Note:**
Please ignore the line breaks in the following API.

```
  download_url?watermark/2
                        /text/
                        /font/
                        /fontsize/
                        /fill/
                        /dissolve/
                        /gravity/
                        /dx/
                        /dy/
```

## Parameter Descriptions

| Parameter                                      | Meaning                                       |
| --------------------------------------- | ---------------------------------------- |
| download_url | Access link of the file which is structured as &lt;bucket id&gt;-&lt;appid&gt;.&lt;picture region&gt;.&lt;domain&gt;.com/&lt;picture name&gt;, for example, examples-1251000004.picsh.myqcloud.com/sample.jpeg |
| /text/      | Watermark content; URL-safe Base64 encoding is necessary                  |
| /font/ | Watermark font; URL-safe Base64 encoding is necessary; tahoma.ttf by default. For the watermark font list, see [List of Supported Fonts](https://cloud.tencent.com/document/product/460/19568) |
| /fontsize/ | Watermark text font size in pt, 13 by default |
| /fill/ | Font color (gray by default); this needs to be set to hexadecimal RGB format (such as #FF0000); for details, see [RGB Color Codes Chart](http://www.rapidtables.com/web/color/RGB_Color.htm); URL-safe Base64 encoding is necessary; #3D3D3D by default |
| /dissolve/ | Text transparency, value range: 1-100, 100 by default (completely opaque) |
| /gravity/ | Text watermark position in the grid (see the [grid position diagram](#1)), Southeast by default |
| /dx/ | Horizontal (horizontal axis) margin in pixels, 0 by default |
| /dy/ | Vertical (vertical axis) margin in pixels, 0 by default |

## Example

```
http://examples-1251000004.picsh.myqcloud.com/sample.jpeg?watermark/2/text/6IW-6K6v5LqRwrfkuIfosaHkvJjlm74=/fill/d2hpdGU=/fontsize/100/dissolve/50/gravity/northeast/dx/20/dy/20
```

<span id="1"></span>
## Grid Position Diagram
The grid position diagram provides a location reference for various operations on the image. The red dots are the origins of each zone position (if the gravity parameter is set to select the zones, the offsetting operation will use the corresponding origins as reference).
![](https://main.qcloudimg.com/raw/25596a911919e464d5edf4c84b829fbe.png)
