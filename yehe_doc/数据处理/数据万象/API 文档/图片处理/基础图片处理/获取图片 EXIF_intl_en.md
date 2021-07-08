## Overview
Exchangeable Image File (EXIF) records the camera settings, thumbnails, and other attributes of digital images. CI uses the **exif** API to obtain EXIF data. An input image cannot be larger than 32 MB, with its width and height not exceeding 30,000 pixels and the total number of pixels not exceeding 100 million. The width and height of an output image cannot exceed 9,999 pixels. For an input animated image, the total number of pixels (Width x Height x Number of frames) cannot exceed 100 million.


>! If an image does not have EXIF data, `{"error" : "no exif data"}` will be returned.
>

## API Format

```
download_url?exif
```

## Parameters

**Operation**: exif

| Parameter | Description |
| ------------ | ------------------------------------------------------------ |
| download_url | URL of the input image, formatted as `<BucketName-APPID>.cos.<picture region>.<domain>.com/<picture name>`<br>Example: `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg` |
| /ignore-error/1 | If this parameter is carried and the image failed to be processed because it is too large, the input image will be returned with no error reported. |


## Examples
```
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?exif
```

