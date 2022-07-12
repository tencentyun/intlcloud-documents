## Overview

Image compression is the process of downsizing an image as much as possible without sacrificing quality so that it can be stored at a lower cost and accessed more quickly.

[CI](https://intl.cloud.tencent.com/document/product/1045/33422) launched the AVIF compression feature. It converts images to the .avif format, which is a new image format launched by Netflix based on AV1 in February 2020 and currently is supported by browsers such as Chrome and Firefox.

## Restrictions

- Format: Images in JPG, PNG, BMP, GIF, WebP, TPG, or HEIF format can be converted to AVIF format.
- Size: The input image cannot be larger than 32 MB, with its width and height not exceeding 30,000 pixels respectively, and the total number of pixels not exceeding 250 million. The width and height of the output image cannot exceed 9,999 pixels respectively. For an animated input image, the total number of pixels (width * height * number of frames) cannot exceed 250 million.
- Frames (for animated images): For GIF images, the number of frames cannot exceed 300.


## Prerequisites

To use AVIF compression, enable the image advanced compression feature for your bucket on the bucket's configuration page. For more information, see [Image Advanced Compression](https://intl.cloud.tencent.com/document/product/1045/40106).

## Directions

CI uses the `imageMogr2` API to provide the AVIF compression feature.

This feature supports processing:

- During download
- During upload
- In the cloud

>?AVIF compression is billed at image advanced compression prices. For detailed pricing, see Image Processing Fees.

## API Sample

#### 1. Processing during download

```plaintext
download_url?imageMogr2/format/avif
```

#### 2. Processing during upload

```http
PUT /<ObjectKey> HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
Pic-Operations: 
{
"is_pic_info": 1,
"rules": [{
    "fileid": "exampleobject",
    "rule": "imageMogr2/format/avif"
}]
}
```

>? `Pic-Operations` is a JSON string. Its parameters are as described in [Persistent Image Processing](https://intl.cloud.tencent.com/document/product/1045/33695).
>


#### 3. Processing in-cloud data

```http
POST /<ObjectKey>?image_process HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Content-length: Size
Authorization: Auth String
Pic-Operations: 
{
"is_pic_info": 1,
"rules": [{
    "fileid": "exampleobject",
    "rule": "imageMogr2/format/avif"
}]
}
```

>? Authorization: Auth String (for more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).
>


## Parameters

| Parameter | Description |
| :--------------- | :----------------------------------------------------------- |
| download_url | URL of the input image in the format of &lt;BucketName-APPID>.cos.&lt;Region>.myqcloud.com/&lt;picture name>; for example, `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg`. |
| /format/&lt;Format> | Compression format, which is `avif` here.    |

## Use Cases

>? **Processing during download** is used as a use case here, which does not store the output image in a bucket. If you need to store the output image, use **processing during upload** or **processing in-cloud data** instead.
>

Assume the input image is a 1,335.2 KB image in PNG format as shown below:
![img](https://example-1258125638.cos.ap-shanghai.myqcloud.com/sample.png)

You can convert the image to AVIF format by using the following request URL:

```plaintext
http://example-1258125638.cos.ap-shanghai.myqcloud.com/sample.png?imageMogr2/format/avif
```

**Compression ratio comparison**

| Format | Image Size |
| :---------- | :-------------------- |
| PNG (input image) | 1,335.2 KB |
| AVIF | 62.8 KB (compression ratio: 95.3%) |

