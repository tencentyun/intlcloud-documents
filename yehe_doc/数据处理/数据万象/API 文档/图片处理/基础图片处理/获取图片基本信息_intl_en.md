## Overview
CI uses the **imageInfo** API to query an image’s basic information, such as its format, width, and height. The input image cannot be larger than 32 MB, with its width and height not exceeding 30,000 pixels, and the total number of pixels not exceeding 250 million. The width and height of the output image cannot exceed 9,999 pixels. For an input animated image, the total number of pixels (Width x Height x Number of frames) cannot exceed 250 million pixels.


## API Format

```
download_url?imageInfo
```

## Parameters

**Operation**: imageInfo

| Parameter | Description |
| ------------ | ------------------------------------------------------------ |
| download_url | URL of the input image, formatted as `<BucketName-APPID>.cos.<picture region>.<domain>.com/<picture name>`<br>Example: `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg` |
| /ignore-error/1 | If this parameter is carried and the image failed to be processed because it is too large, the input image will be returned with no error reported. |

## Example

**Request**
```
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageInfo
```


**Response**
```
{"format": "jpeg", "width": "960", "height": "540", "size": "158421", "md5": "77a16fa70e2eba652fb42e8a639c52f2", "photo_rgb": "0x736246"}
```
