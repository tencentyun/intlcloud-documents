## Description
Tencent Cloud CI uses the **imageAve** API to obtain information about the average hue of the image. Currently, this API is applicable to images with a size no greater than 20 MB and a length and width both less than 9,999 pixels.


## API Format
```
download_url?imageAve       				
```

### Parameter description

**Operation**: imageAve

| Parameter | Description |
| ------------ | ------------------------------------------------------------ |
| download_url | The file access URL in the format of `<BucketName-APPID>.<picture region>.<domain>.com/<picture name>`, <br>for example, `examplebucket-1250000000.picsh.myqcloud.com/picture.jpeg`. |


## Example

**Request**
```
http://examples-1251000004.picsh.myqcloud.com/sample.jpeg?imageAve
```

**Response**
```
{"RGB": "0x736246"}
```