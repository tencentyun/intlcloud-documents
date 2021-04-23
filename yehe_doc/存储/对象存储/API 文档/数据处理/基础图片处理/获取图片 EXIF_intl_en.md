## Feature
Exchangeable Image File (EXIF) records the shooting parameters, thumbnails, and other attributes of digital pictures. COS can obtain EXIF data on images by using the **exif** API in Tencent Cloud CI. Currently, supported images are smaller than 20 MB in size and smaller than 9,999 pixels in length and width.


>
>-Image processing is a paid service, the fees of which are charged by Cloud Infinite. For detailed billing instructions, see Cloud Infinite’s [Billing and Pricing](https://intl.cloud.tencent.com/document/product/1045/33431).
>- If an image has no EXIF data, `{"error" : "no exif data"}` will be returned.

## API Form

```plaintext
download_url?exif
```

## Parameter Description

**Operation name**: exif.

| Parameter         | Description                                                         |
| ------------ | ------------------------------------------------------------ |
| download_url | URL that is used to access a file. Format: `<BucketName-APPID>.cos.<picture region>.<domain>.com/<picture name>`, <br>for example, `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg`. |


## Examples
```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?exif
```

