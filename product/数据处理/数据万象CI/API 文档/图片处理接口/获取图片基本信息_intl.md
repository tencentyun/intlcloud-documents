## Overview
This gets the basic information of the image, including the format, length and width. Currently, this supports processing images with a size of less than 20 MB and a length x width of less than 9,999 pixels.
## API Form
download_url?imageInfo
## Parameter Descriptions
| Parameter | Meaning |
| --------------------------------------- | ---------------------------------------- |
| download_url | Access link of the file which is structured as &lt;bucket id&gt;-&lt;appid&gt;.&lt;picture region&gt;.&lt;domain&gt;.com/&lt;picture name&gt;, for example, examples-1251000004.picsh.myqcloud.com/sample.jpeg |

## Example

### Without Signature

```
http://examples-1251000004.picsh.myqcloud.com/sample.jpeg?imageInfo
```

### With Signature
For the generation method of the signature field "sign", see [Signature and Authentication](https://cloud.tencent.com/document/product/460/6968).

```
http://examples-1251000004.picsh.myqcloud.com/sample.jpeg?imageInfo&sign=xxx
```
