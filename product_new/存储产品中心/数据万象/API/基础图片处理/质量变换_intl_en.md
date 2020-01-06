## Description

The **imageMogr2** API is used to adjust the quality of an image.

> This API is applicable only to images in **jpg** and **webp** formats.

## API Format

```
download_url?imageMogr2/quality/<Quality>
                       /rquality/<quality>
                       /lquality/<quality>						
```

## Parameter Description
Operation: quality

| Parameter | Description |
| ------------------- | ------------------------------------------------------------ |
| download_url | The file URL in the format of `<BucketName-APPID>.<picture region>.<domain>.com/<picture name>`, <br>for example, `examplebucket-1250000000.picsh.myqcloud.com/picture.jpeg`. |
| /quality/&lt;Quality>  | The image quality. Value range: 0-100. The default value is the quality of the original image. The smaller value of the original image quality and the specified quality will be used. If &lt;Quality&gt; is followed by an exclamation mark (**!**), the specified value must be used, for example, `90!`. |
| /rquality/&lt;quality> | The relative quality of the image. Value range: 0-100. The value is subject to the original image quality. If the original image quality is 80 and `rquality` is set to 80, the quality of the processed image is 64 (that is, 80 x 80%). |
| /lquality/&lt;quality> | The lowest quality of the image. Value range: 0-100. This parameter specifies the lowest quality of the final image. <li>If the original image quality is 85 and `lquality` is set to 80, the quality of the processed image is 85.<li> If the original image quality is 60 and `lquality` is set to 80, the quality of the final image will be improved to 80. |


## Example
This example sets **absolute quality** to 60:
```
http://examples-1251000004.picsh.myqcloud.com/sample.jpeg?imageMogr2/quality/60
```

The effect is as follows:
![](https://main.qcloudimg.com/raw/499501182b2989899116d958f94368a5.jpeg)

This example sets **relative quality** to 60:

```
http://examples-1251000004.picsh.myqcloud.com/sample.jpeg?imageMogr2/rquality/60
```

The effect is as follows:
![](https://main.qcloudimg.com/raw/7b111c90aca02d94d0f11991d92e64cb.jpeg)