## Description
Through the **imageMogr2** API, Tencent Cloud CI provides the format conversion, gif format optimization, and progressive display features.

## API Format

```
download_url?imageMogr2/format/<Format>
					   /cgif/<FrameNumber>
					   /interlace/<Mode>
```

## Parameter Description

| Parameter | Description |
| -------------------- | ------------------------------------------------------------ |
| download_url | The file access URL in the format of `<BucketName-APPID>.<picture region>.<domain>.com/<picture name>`, <br>for example, `examplebucket-1250000000.picsh.myqcloud.com/picture.jpeg`. |
| /format/&lt;Format> | Format conversion. The image format of the target thumbnail can be jpg, bmp, gif, png, webp, or yjpeg, where yjpeg is essentially a jpeg format optimized by CI. The default value is the format of the original image. |
| /cgif/&lt;FrameNumber&gt; | Gif format optimization, which is applicable only to original images in gif format. The gif format is optimized to reduce the number of frames and colors. There are two cases for this parameter: <li>If FrameNumber=1, the image is processed according to the default number of frames, which is 30. If FrameNumber is greater than 30, the image is cut. <li>If FrameNumber falls within the range of (1,100], the image is compressed according to the specified FrameNumber value. |
| /interlace/&lt;Mode> | The image is output in progressive jpg format. Mode can be set to 0 or 1. 0: the progressive mode is disabled. 1: the progressive mode is enabled. This parameter is valid only when the output image format is jpg. If the image is not output in jpg format, this parameter is ignored. The default value is 0. |

## Example
This example shows how to convert an original image in jpeg format into the png format:

```
http://examples-1251000004.picsh.myqcloud.com/sample.jpeg?imageMogr2/format/png
```