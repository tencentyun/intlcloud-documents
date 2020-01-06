## Description
Tencent Cloud CI uses the **imageInfo** API to query the basic information of an image, such as the format, length, and width. Currently, this API is applicable to images with a size no greater than 20 MB and a length and width both less than 9,999 pixels.

## API Format

```
download_url?imageInfo
```

### Parameter description

**Operation**: imageInfo

| Parameter | Description |
| ------------ | ------------------------------------------------------------ |
| download_url | The file access URL in the format of `<BucketName-APPID>.<picture region>.<domain>.com/<picture name>`, <br>for example, `examplebucket-1250000000.picsh.myqcloud.com/picture.jpeg`. |

## Example

**Request**
```
http://examples-1251000004.picsh.myqcloud.com/sample.jpeg?imageInfo
```


**Response**
```
{"format": "jpeg", "width": "960", "height": "540", "size": "158421", "md5": "77a16fa70e2eba652fb42e8a639c52f2", "photo_rgb": "0x736246"}
```