## Feature
This API **imageMogr2** from Tencent Cloud CI is used to provide format conversion, GIF optimization, and progressive display in COS.

>Image processing is a paid service, the fees of which are charged by Cloud Infinite. For detailed billing instructions, see Cloud Infinite’s [Billing and Pricing](https://intl.cloud.tencent.com/document/product/1045/33431).

## API Form

```plaintext
download_url?imageMogr2/format/<Format>
					   /cgif/<FrameNumber>
					   /interlace/<Mode>
```

>Please ignore the preceding spaces and line breaks.
## Parameter Description

| Parameter                         | Description                                                         |
| -------------------- | ------------------------------------------------------------ |
| download_url | URL that is used to access a file. Format: `<BucketName-APPID>.cos.<picture region>.<domain>.com/<picture name>`, <br>for example, `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg`. |
| /format/&lt;Format> | Format conversion, which can be used to convert images into target thumbnails in the following formats: jpg, bmp, gif, png, webp, and yjpeg. Where, yjpeg is optimized based on jpeg by CI and is actually the jpg format. The default format is that of an original image. |
| /cgif/&lt;FrameNumber&gt; | GIF optimization, which is used to optimize only images whose original images are in the gif format. It can reduce frames and colors of images. There are two situations:<li>If the value of FrameNumber is 1, the default number (30) of frames is used. If the number of frames exceeds this value, the extra frames will be captured.<li>If the value of FrameNumber is in (1,100], the image will be compressed to the specified number of frames (FrameNumber). |
| /interlace/&lt;Mode> | The output is in the progressive jpg format. The value of Mode can be 0 or 1. 0: indicates the progressive mode is not enabled. 1: indicates the progressive mode is enabled. This parameter is valid only when the output image is in the jpg format. If the output image is not in the jpg format, this parameter will be ignored. The default value is 0. |


## Examples

This example shows you how to convert an image from jpeg to png format.

```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/format/png
```

