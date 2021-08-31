## Overview

This API is used to sharpen images in Tencent Cloud CI.

> This API is only applicable to **jpg** and **webp** images.

## API Form

```shell
download_url?imageMogr2/quality/<Quality>
                       /rquality/<quality>
                       /lquality/<quality>						
```

## Parameter Description

Operation name: quality.

| Parameter | Description |
| ------------------- | ------------------------------------------------------------ |
| download_url | URL that is used to access a file. The URL form is `<BucketName-APPID>.cos.<picture region>.<domain>.com/<picture name>`, <br>for example, `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg`. |
| /quality/&lt;Quality> | Image quality. Value range: 0 - 100. The default value is the original image quality. Obtain the minimum value from the original image quality and the specified quality. If &lt;Quality&gt; is followed by an exclamation mark (!”), a specified value is used forcibly, for example, `90!`. |
| /rquality/&lt;quality> | Indicates the relative image quality. Value range: 0 - 100. The value is based on the original image quality. For example, assume that the original image quality is 80. If you set rquality to 80, the resulted image quality is 64 (80x80%). |
| /lquality/&lt;quality> | Indicates the lowest image quality. Value range: 0 - 100. The value is set to the minimum value of the quality parameter for the resulted image. <br><li>For example, assume that the original image quality is 85. If you set lquality to 80, the resulted image quality is 85. <br><li>For example, assume that the original image quality is 60. If you set lquality to 80, the resulted image quality is improved to 80. |


## Example

The **absolute quality** is set to 60 in the following example.
```
http://examples-1251000004.picsh.myqcloud.com/sample.jpeg?imageMogr2/quality/60
```

The effect is as follows:
![](https://main.qcloudimg.com/raw/499501182b2989899116d958f94368a5.jpeg)

The **relative quality** is set to 60 in the following example.

```
http://examples-1251000004.cos.ap-shanghai..myqcloud.com/sample.jpeg?imageMogr2/rquality/60
```

The effect is as follows:
![](https://main.qcloudimg.com/raw/7b111c90aca02d94d0f11991d92e64cb.jpeg)
