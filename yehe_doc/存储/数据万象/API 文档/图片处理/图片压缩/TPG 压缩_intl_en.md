## Overview

Image compression is the process of downsizing an image as much as possible without sacrificing quality so that it can be stored at a lower cost and accessed more quickly.

[CI](https://intl.cloud.tencent.com/document/product/1045/33422) launched the TPG compression feature. It converts images to the .tpg format, which is a proprietary image format launched by Tencent and supports animated images. Currently, QQ Browser, Qzone, and other Tencent products support .tpg by default. A .tpg image is over 90% or 50% smaller than a .gif or .png image with the same quality, respectively.

## Restrictions

- Format: Images in JPG, PNG, BMP, GIF, WebP, HEIF, or AVIF format can be converted to TPG format.
- Size: The input image cannot be larger than 32 MB, with its width and height not exceeding 30,000 pixels respectively, and the total number of pixels not exceeding 250 million. The width and height of the output image cannot exceed 9,999 pixels respectively. For an animated input image, the total number of pixels (width * height * number of frames) cannot exceed 250 million.
- Frames (for animated images): For GIF images, the number of frames cannot exceed 300.

## Prerequisites

- To use TPG compression, enable the image advanced compression feature for your bucket on its configuration page. For more information, see [Setting Image Advanced Compression](https://intl.cloud.tencent.com/document/product/436/40117).
- TPG is Tencent's proprietary image format. To use it, ensure that **the environment where images are loaded supports TPG decoding**. CI provides the TPG decoder-integrated SDKs for [iOS](https://intl.cloud.tencent.com/document/product/1045/47707), [Android](https://intl.cloud.tencent.com/document/product/1045/45575), and [Windows](https://main.qcloudimg.com/raw/851dd252378813d250eeca5ed55ffd36/TPG_win_SDK.zip) to facilitate quick integration with TPG.

## Directions

CI uses the `imageMogr2` API to provide the TPG compression feature.

This feature supports processing:

- During download
- During upload
- In the cloud

>? TPG compression is billed at image advanced compression prices by CI. For detailed pricing, see Image Processing Fees.
>

## API Sample

#### 1. Processing during download

```plaintext
download_url?imageMogr2/format/tpg
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
    "rule": "imageMogr2/format/tpg"
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
    "rule": "imageMogr2/format/tpg"
}]
}
```

>? Authorization: Auth String (for more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).
>

## Parameters

| Parameter | Description |
| :--------------- | :----------------------------------------------------------- |
| download_url | URL of the input image in the format of &lt;BucketName-APPID>.cos.&lt;Region>.myqcloud.com/&lt;picture name>; for example, `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg`. |
| /format/&lt;Format> | Compression format, which is `tpg` here.                             |

## Use Cases

>? **Processing during download** is used as a use case here, which does not store the output image in a bucket. If you need to store the output image, use **processing during upload** or **processing in-cloud data** instead.
>

Assume the input image is a 1,335.2 KB image in PNG format as shown below:
![img](https://example-1258125638.cos.ap-shanghai.myqcloud.com/sample.png)

You can convert the image to TPG format by using the following request URL:

```plaintext
http://example-1258125638.cos.ap-shanghai.myqcloud.com/sample.png?imageMogr2/format/tpg
```

**Compression ratio comparison**

| Format | Image Size |
| :---------- | :--------------------- |
| PNG (input image) | 1,335.2 KB |
| TPG | 36.67 KB (compression ratio: 97.3%) |

