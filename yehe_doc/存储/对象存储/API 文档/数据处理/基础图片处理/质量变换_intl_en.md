## Feature

This API **imageMogr2** from Tencent Cloud CI is used to convert image quality in COS.

>
>- Image processing is a paid service, the fees of which are charged by Cloud Infinite. For detailed billing instructions, see Cloud Infinite’s [Billing and Pricing](https://intl.cloud.tencent.com/document/product/1045/33431).
>- This API is only applicable to **jpg** and **webp** images.

## API Form

```plaintext
download_url?imageMogr2/quality/<Quality>
                       /rquality/<quality>
                       /lquality/<quality>						
```

## Parameter Description

Operation name: quality.

| Parameter                         | Description                                                         |
| ------------------- | ------------------------------------------------------------ |
| download_url | URL that is used to access a file. Format: `<BucketName-APPID>.cos.<picture region>.<domain>.com/<picture name>`, <br>for example, `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg`. |
| /quality/&lt;Quality>  | Absolute image quality. Value range: 0 - 100; Use the value of original image quality (default) or specified quality, whichever is smaller. If &lt;Quality&gt; is followed by an English exclamation mark (!), a specified value must be used, e.g., `90!`. |
| /rquality/&lt;quality> | Indicates the relative image quality. Value range: 0 - 100. The value is subject to the original image quality. For example, assume that the original image quality is 80. If you set `rquality` to 80, the resulting image quality is 64 (80 x 80%). |
| /lquality/&lt;quality> | Indicates the lowest image quality. Value range: 0 - 100. This value is the quality threshold for the resulting image. <br>For example, assume that the original image quality is 85. If you set `lquality` to 80, the resulting image quality is 85.<br>Assume that the original image quality is 60. If you set `lquality` to 80, the resulting image quality is improved to 80. |


## Examples

**Example 1. Set absolute quality**
The **absolute quality** is set to 60 in the following example.
```plaintext
http://examples-1251000004.picsh.myqcloud.com/sample.jpeg?imageMogr2/quality/60
```

The effect is as follows:
![](https://main.qcloudimg.com/raw/499501182b2989899116d958f94368a5.jpeg)


**Example 2. Set relative quality**

The **relative quality** is set to 60 in the following example.

```plaintext
http://examples-1251000004.cos.ap-shanghai..myqcloud.com/sample.jpeg?imageMogr2/rquality/60
```

The effect is as follows:
![](https://main.qcloudimg.com/raw/7b111c90aca02d94d0f11991d92e64cb.jpeg)
