## Feature
This API **imageInfo** from Tencent Cloud CI is used to query the basic information about an image in COS, including format, length, and width. Currently, supported images are smaller than 20 MB in size and smaller than 9,999 pixels in length and width.

>Image processing is a paid service, the fees of which are charged by Cloud Infinite. For detailed billing instructions, see Cloud Infinite’s [Billing and Pricing](https://intl.cloud.tencent.com/document/product/1045/33431).
## API Form

```plaintext
download_url?imageInfo
```

## Parameter Description

**Operation name**: imageInfo

| Parameter         | Description                                                         |
| ------------ | ------------------------------------------------------------ |
| download_url | URL that is used to access a file. Format: `<BucketName-APPID>.cos.<picture region>.<domain>.com/<picture name>`, <br>for example, `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg`. |

## Examples

**Request**
```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageInfo
```


**Response**
```plaintext
{"format": "jpeg", "width": "960", "height": "540", "size": "158421", "md5": "77a16fa70e2eba652fb42e8a639c52f2", "photo_rgb": "0x736246"}
```
