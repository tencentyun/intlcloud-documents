## Description
The **imageMogr2** API is used to sharpen an image.

## API Format
```
download_url?imageMogr2/sharpen/<value>
```

## Parameter Description

Operation: sharpen

| Parameter | Description |
| ---------------- | ------------------------------------------------------------ |
| download_url | The file acccess URL in the format of `<BucketName-APPID>.<picture region>.<domain>.com/<picture name>`, <br>for example, `examplebucket-1250000000.picsh.myqcloud.com/picture.jpeg`. |
| /sharpen/&lt;value> | This parameter refers to the image sharpening feature, where `value` specifies the sharpening value. Value range: an integer between 10 and 300. A larger value produces greater sharpness. The recommended value is 70. |

## Example
**Sharpening an image**
This example shows how to sharpen an image by setting the sharpening parameter to 70:
```
http://examples-1251000004.picsh.myqcloud.com/sample.jpeg?imageMogr2/sharpen/70
```

Final effect:
![](https://main.qcloudimg.com/raw/b599b8cc198d9682d2f6316aa0e44a9d.jpeg)