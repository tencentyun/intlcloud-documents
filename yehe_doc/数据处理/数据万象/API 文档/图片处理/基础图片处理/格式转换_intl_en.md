## Overview
CI uses the **imageMogr2** API to perform format conversion, GIF optimization, and progressive display.

## API Format

```shell
download_url?imageMogr2/format/<Format>
					   /cgif/<FrameNumber>
					   /interlace/<Mode>
```

## Parameters

| Parameter | Description |
| -------------------- | ------------------------------------------------------------ |
| download_url | URL of the input image, formatted as `<BucketName-APPID>.cos.<picture region>.<domain>.com/<picture name>`<br>Example: `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg` |
| /format/<Format> | Converts the image format. The target format can be JPG, BMP, GIF, PNG, WebP, or YJPEG (a JPEG-based format optimized by CI). Default format: format of the input image |
| /cgif/&lt;FrameNumber&gt; | Optimizes a GIF image by reducing the number of frames and colors. Valid values of `FrameNumber`: <li>`1`: cuts the input GIF to the default number of frames (30). If the original number of frames is greater than 30, the exceeded frames will be cut. <li>(1,100]: compresses the image to the specified number of frames. </li>|
| /interlace/&lt;Mode> | Progressive mode of the output JPG image. Valid values of `Mode`: <br>`0` (default): disables the progressive mode. <br>`1`: enables the progressive mode. <br>This parameter takes effect only when the output image is in JPG format. Otherwise, this parameter will be ignored. |
| /ignore-error/1 | If this parameter is carried and the image failed to be processed because it is too large, the input image will be returned with no error reported. |


## Examples

#### Converting a JPEG image into PNG format

```
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/format/png
```

#### Converting a JPEG image into PNG format with a signature carried

This example processes the image in the same way as in the example above except that a signature is carried. The signature is joined with other processing parameters using an ampersand (&):

```
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?q-sign-algorithm=<signature>&imageMogr2/format/png
```

>? You can obtain the value of `<signature>` by referring to [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).
>
	
